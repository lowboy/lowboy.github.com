title: '完美解决 Linux 下 Sublime Text 中文输入'
date: 2014-05-06 19:36:59
categories:
tags: [fcitx,linux,sublime,开源软件]
---
<!--more-->
<em>*声明：此文非原创，而是综合了若干人的工作而成*
*参考文章见文末*</em>

---
##测试环境：##
```
OS:linuxmint16_x64(xfce)
Fcitx:4.2.8.3
sublime_text:3059
```
###第一步###
- 将下列代码保存为`subsublime-imfix.c`
```c
/*
sublime-imfix.c
Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
By Cjacker Huang

gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
LD_PRELOAD=./libsublime-imfix.so subl
*/
#include <gtk/gtk.h>
#include <gdk/gdkx.h>
typedef GdkSegment GdkRegionBox;

struct _GdkRegion
{
  long size;
  long numRects;
  GdkRegionBox *rects;
  GdkRegionBox extents;
};

GtkIMContext *local_context;

void
gdk_region_get_clipbox (const GdkRegion *region,
            GdkRectangle    *rectangle)
{
  g_return_if_fail (region != NULL);
  g_return_if_fail (rectangle != NULL);

  rectangle->x = region->extents.x1;
  rectangle->y = region->extents.y1;
  rectangle->width = region->extents.x2 - region->extents.x1;
  rectangle->height = region->extents.y2 - region->extents.y1;
  GdkRectangle rect;
  rect.x = rectangle->x;
  rect.y = rectangle->y;
  rect.width = 0;
  rect.height = rectangle->height;
  //The caret width is 2;
  //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
  if(rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
        gtk_im_context_set_cursor_location(local_context, rectangle);
  }
}

//this is needed, for example, if you input something in file dialog and return back the edit area
//context will lost, so here we set it again.

static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
{
    XEvent *xev = (XEvent *)xevent;
    if(xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
       GdkWindow * win = g_object_get_data(G_OBJECT(im_context),"window");
       if(GDK_IS_WINDOW(win))
         gtk_im_context_set_client_window(im_context, win);
    }
    return GDK_FILTER_CONTINUE;
}

void gtk_im_context_set_client_window (GtkIMContext *context,
          GdkWindow    *window)
{
  GtkIMContextClass *klass;
  g_return_if_fail (GTK_IS_IM_CONTEXT (context));
  klass = GTK_IM_CONTEXT_GET_CLASS (context);
  if (klass->set_client_window)
    klass->set_client_window (context, window);

  if(!GDK_IS_WINDOW (window))
    return;
  g_object_set_data(G_OBJECT(context),"window",window);
  int width = gdk_window_get_width(window);
  int height = gdk_window_get_height(window);
  if(width != 0 && height !=0) {
    gtk_im_context_focus_in(context);
    local_context = context;
  }
  gdk_window_add_filter (window, event_filter, context);
}
```
---
###第二步###
- 安装 `C/C++ 的编译环境`和 `gtk libgtk2.0-dev`

```
$sudo apt-get install build-essential libgtk2.0-dev
```
---
###第三步###
- 编译共享内~~<font size="3px" color="#ff0000">裤</font>~~库

```shell
$gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC```
---
###第四步###
- 设置 LD_PRELOAD 并启动 Sublime Text
```shell
$LD_PRELOAD=./libsublime-imfix.so subl
```
---
###第五步###
- <font color="#ff0000">*一定要记得*</font>把`libsublime-imfix.so`放到`/opt/sublime_text/`中

---
###第六步###
- 修改`/usr/share/applications/sublime_text.desktop`
修改前，文件示例：
```shell
[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
GenericName=Text Editor
Comment=Sophisticated text editor for code, markup and prose
Exec=/opt/sublime_text/sublime_text %F
Terminal=false
MimeType=text/plain;
Icon=sublime-text
Categories=TextEditor;Development;
StartupNotify=true
Actions=Window;Document;

[Desktop Action Window]
Name=New Window
Exec=/opt/sublime_text/sublime_text -n
OnlyShowIn=Unity;

[Desktop Action Document]
Name=New File
Exec=/opt/sublime_text/sublime_text --command new_file
OnlyShowIn=Unity;

```
然后在每一个`Exec=`后添加上这一句
>`env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so` 

修改后，应该是这个样子：
```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
GenericName=Text Editor
Comment=Sophisticated text editor for code, markup and prose
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text %F
Terminal=false
MimeType=text/plain;
Icon=sublime-text
Categories=TextEditor;Development;
StartupNotify=true
Actions=Window;Document;

[Desktop Action Window]
Name=New Window
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text -n
OnlyShowIn=Unity;

[Desktop Action Document]
Name=New File
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text --command new_file
OnlyShowIn=Unity;

```
---
###第七步###
修改`/usr/bin/subl`为
	#!/bin/sh
	export LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so
	exec /opt/sublime_text/sublime_text "$@"
---
Congratulations！
做完了以上这些，你就可以享受sublime和fcitx的无间配合啦！



---
参考文章:
[1. 完美解决 Linux 下 Sublime Text 中文输入  by  Jat][1]
[1]:https://www.sinosky.org/linux-sublime-text-fcitx.html
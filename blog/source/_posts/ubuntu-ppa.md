layout: post
title: 备份一些ppa以及开源软件地址
date: 2014-05-09 19:15:26
categories: 
tags: [PPA,开源软件]
---
<!--more-->
##什么是PPA？##

PPA是**`personal package archive`**的缩写,即个人包档案.使用PPA,软件制作者可以轻松地发布软件,并且能够准确地对用户进行升级.Ubuntu用户使用PPA源将更加方便的获得软件的最新版本。
关于PPA的详细情况,可以参考：https://help.launchpad.net/Packaging/PPA

##如何获得PPA？##

针对使用ubuntu的用户而言,访问这个网站  https://launchpad.net/  ,搜索需要的软件,就可以得到该软件的PPA源.

写这篇文章，主要是留着自己以后重装系统的时候方便取用。
下面罗列开始：
##优秀软件##

###<font color="#ff0000">Y PPA Manager</font>###
&emsp;&emsp;这货其实现在是我重(shou)装(jian)系(zhe)统(teng)的第一必装，有了它，下面的所有话其实都能够省了。
当然，本着不能出师未捷身先死的精神，我还是要把下面的话写完。

废话少说，上代码先
```shell
$sudo apt-get repository ppa:webupd8team/y-ppa-manager
$sudo apt-get update
$sudo apt-get install y-ppa-manager
```
</br>
###<font color="#ff0000">apt-fast</font>###
&emsp;&emsp;在我认识*`Y PPA Manager`*之前，*`apt-fast`*曾经一度是我对新系统的第一个改动，现在虽然落到了第二，但仍然是我最常用、心目中最好的程序，没有之一。
也以至于我在编辑上面一段代码的时候，*`apt-get`*敲的无比别扭，因为我的手指早就习惯*`apt-fast`*啦！

```shell
$sudo apt-get repository ppa:apt-fast/stable
$sudo apt-get update
$sudo apt-get install apt-fast
```
>为了**<font color="#ff0000" size="5px">表示尊敬</font>**，下面的代码，我就都用**`apt-fast`**代替了。

###<font color="#ff0000">ubuntu-tweak</font>###
&emsp;&emsp;身为一个tweak党，倘若不能tweak，那当真是浑身不舒服斯基。
&emsp;&emsp;ubuntu-tweak作为ubuntu系的linux里知名度最高也是最优秀的tweak软件之一，不需要我做太多的解释，超高的人气和装机量足以说明所有问题。
P.S.据说作者是国人，看着这软件在国外的高人气，想想就有些小激动呢～
```shell
$sudo apt-get repository ppa:tualatrix/ppa
$sudo apt-get update
$sudo apt-get install ubuntu-tweak
```
###<font color="#ff0000">深度音乐</font>###
&emsp;&emsp;终于有一个**国产**软件了！！！

&emsp;&emsp;对于一个不具备黑客精神的人来说，linux中的音乐播放器确实有些蛋疼。
&emsp;&emsp;首先，命令行界面不是我的菜，毕竟咱是在玩音乐吧，多多少少得配合一点视觉上美的享受才好。
&emsp;&emsp;然后问题就来了，因为我不是一个只听英文歌的人，总有一大堆中文歌，当我看见他们躺在列表里堆成一坨坨的乱码，整个人都不好了。
&emsp;&emsp;`Rhythmbox`,`Banshee` 都是这样的问题，`Clemetine`,`Exaile`倒没有这种事，但是界面实在太简略了Orz
而另外，曾经让我眼睛一亮的`Songbird`又开发停滞了。
&emsp;&emsp;`amarok`倒是足够华丽，虽然依旧乱码，但至少拥有了也让我为其转tag编码的冲动。可是呢，我不在KDE环境啊！`amarok`离开她生长的环境之后，适应新世界的能力实在太差，她只能再给自己搭建一个一样的小窝才活得下去。为了安装她，我还要忍受一大堆没有用处的软件包。都说爱情要忍受另一半的一切，我只能说，这让我好一阵心动的`amarok`原来并不是真爱。
&emsp;&emsp;最后，就如**《中国合伙人》**中**佟大为**饰演的的**王阳**在浪荡了一辈子后，最后竟选了一个年轻时绝对不会注意的那个她一样。
>而我，则选择了`deepinmusic`,也即`深度音乐`

虽然很被geek看不上，不过默认设置下，她已有该有的一切：没有乱码、无缝播放、桌面歌词、桌面OSD提示、支持豆瓣FM插件、还能焕肤！于是，我就这样被征服了，也许这也就是岁月在我身上留下的改变吧～
&emsp;&emsp;不得不说，深度在XP时代，对于推动中国系统发展，发挥了不可估量的作用，现在由于版权问题转混开源界，也是华丽转身。
```bash
$sudo add-apt-repository ppa:noobslab/deepin-sc
$sudo apt-fast update
$sudo apt-fast install deepin-music-player
```
<p>当然，出了问题请访问:</p>[深度官方wiki](http://wiki.linuxdeepin.com/index.php?title=Deepin_Music_Player&diff=cur&oldid=6031)
---


title: 'Notes About Bloging'
date: 2014-05-07 20:15:04
categories: [笔记]
tags: [积累]
---
<!--more-->
##一.插入视频##
>插入视频代码1



    <div class="video-container"><iframe width="420" height="315" src="" frameborder="0" allowfullscreen></iframe></div>

>插入视频代码2


    <video src="" width="320" height="240" controls="controls">
	Your browser does not support the video tag.
	</video>

>插入视频代码3


    <video id="Html5Video" width="640" height="360" preload controls>
    <source src="http://video4blog.qiniudn.com/03-04%20Detroit%20Champ.mp4" type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"' />
    <source src="video.ogv" type='video/ogg; codecs="theora, vorbis"' />
    <source src="video.webm" type='video/webm; codecs="vp8, vorbis"' />
    <p>Your user agent does not support the HTML5 Video element.</p>
    </video>

>插入视频代码5


    <video id="video" controls="" preload="none" poster="http://media.w3.org/2010/05/sintel/poster.png">
    <source id="mp4" src="http://media.w3.org/2010/05/sintel/trailer.mp4" type="video/mp4">
    <source id="webm" src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm">
    <source id="ogv" src="http://media.w3.org/2010/05/sintel/trailer.ogv" type="video/ogg">
    <p>Your user agent does not support the HTML5 Video element.</p>
    </video>

>插入音频代码1

	<audio controls="controls">
  	<source src="song.ogg" type="audio/ogg">
  	<source src="song.mp3" type="audio/mpeg">
	Your browser does not support the audio tag.
	</audio>


##二.插入空格##
- 半方大的空白`&ensp;`或`&#8194;`
- 全方大的空白`&emsp;`或`&#8195;`
- 不断行的空白格`&nbsp;`或`&#160;`



&emsp;&emsp;推荐全角空格，切换到全角模式下（一般的中文输入法都是按 shift + space）输入两个空格就行了。这个相对 `&nbsp;` 来说稍微干净一点，而且宽度是整整两个汉字，很整齐。
&emsp;&emsp;当然，填上***`&emsp;&emsp;`***其实就可以了～


##绘制表格
* 法一

```
<table class="table table-bordered table-striped table-condensed">
<tr>
  <td>First</td>
  <td>row</td>
  ﻿﻿<!--<li><input type="checkbox" checked/>使用html代码</li> <li><input type="checkbox" />不使用html代码</li>-->
</tr>
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>
```

* 法二

```
你好|Markdown|表格
---|---|---
我|不是|人
```
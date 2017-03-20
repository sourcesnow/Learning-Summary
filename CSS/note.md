# 2017-03-18
1 下面代码中，css中伪类的选择

>下面代码中，可以看出来伪类的优先级与class的优先级一致，将两者换个位置，会导致变换的效果
<style type="text/css">    
        #first li.list{color: green;}
        #first li:first-child{color: red;}
</style>
对比
><style type="text/css">    
        #first ul.list{color: green;}
        #first ul:first-child{color: red;}
</style>
> 其中,**注意first-child是li的，不是ul的，如果想使用ul的话，则使用ul>:first-child，
> 这个用法就是使用>的作用，具体用法见[css中各类选择符号的使用](http://yanhaijing.com
> /css/2014/01/04/the-30-css-selectors-you-must-memorize/)**
> <!DOCTYPE html>
> <html>
> <head>
> <title></title>
> </head>
> <body>
> <ul>
    <li class='list'>Hello</li>
    <li></li>
    <li></li>
</ul>
</body>
</html>
优先级依次减低
* 在属性后面使用 !important 会覆盖页面内任何位置定义的元素样式。
* 作为style属性写在元素内的样式
* id选择器
* 类选择器==伪类选择器
* 标签选择器
* 通配符选择器

2 html中文档的加载顺序是与标签的上下顺序有关，与其他东西无关，如果不设置css的话。

3 其中px的默认顺序是 1px 2px 3px 4px 其中顺序分别是上右下左，顺时针顺序。
  三个的话，则分别是上右下，两个的话则分别是上下共用，和左右共用。


4. @import 与link都可以引入css样式表,但前者是css中的样式，后者是html的标签。
 前者如果要在html中使用则是需要在<header></header>中引入<style type="text/css"></style>并将其放入其中，因为是css的表现形式 **css首行可以多考虑引入@charset "utf-8"**
 同时link作为html中的domcontent被加载，而后者则是需要等其他content加载完才加载。

5. bootstrap中使用的栅栏格式，xs，sm，md，lg 分别对应 <768,>=768,>=992,>=1200 
6. manifest中可以离线缓存网页内容，

> <html lang="en" manifest="index.manifest">这个是具体用法，几种manifest文件中定义
> 三个变量，cache，network，fallback，分别指定缓存文件，需要网络才能访问的文件和后备 
> 资源，当网络资源不可访问时，访问这里面的资源。其中使用window.applicationCache()
> 进行设置，而localStorage则是通过localStorage.函数名等来进行宁设置

7. 记得查看MDN中的空元素列表 [参考](https://developer.mozilla.org/zh-CN/docs/Glossary/%E7%A9%BA%E5%85%83%E7%B4%A0)
8. css中可继承类和不可继承的各种:
* 可继承的样式： font-size font-family color, UL LI DL DD DT;
* 不可继承的样式：border padding margin width height 
10. css中样式表优先级问题:
 
> 同权重: 内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中）
> important 比 内联优先级高

11. 多了解一下display:flex
12. 常用的hack技术:
 
> * png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.
> * 浏览器默认的margin和padding不同。解决方案是加一个全局的*   
> * {margin:0;padding:0;}来统一
> * 
> * IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比大
> * 浮动ie产生的双倍距离 #box{ float:left; width:10px; margin:0 0 0 100px;}
> * 渐进识别的方式，从总体中逐渐排除局部。
> * IE下,可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()
> 获取自定义属性;Firefox下,只能使用getAttribute()
> 取自定义属性。解决方法:统一通过getAttribute()获取自定义属性。
> * IE下,even对象有x,y属性,但是没有pageX,pageY属性;
> Firefox下,event对象有pageX,pageY属性,但是没有x,y属性。
> * Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,
   可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。
   超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
   L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}

9. visibility:collapse


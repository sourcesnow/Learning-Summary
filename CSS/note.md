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
>其中,**注意first-child是li的，不是ul的，如果想使用ul的话，则使用ul>:first-child，这个用法就是使用>的作用，具体用法见[css中各类选择符号的使用](http://yanhaijing.com/css/2014/01/04/the-30-css-selectors-you-must-memorize/)**
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<ul>
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


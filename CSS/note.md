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

5. js中concat函数，仅仅只是放回两个数组的副本，并不改变原数组
6. null==undefined 
7. 下面这个问题，注意+同时是字符连接运算

>var obj = {"key":"1","value":"2"};
var newObj = obj;
newObj.value += obj.key;
alert(obj.value);
最后的结果是“21”

8. 可以看看EcmaScript6 中的语法定义
9. 函数的多种声明方式

>var  showOne=function foo(){
    alert(typeof foo);
  };
  //下面这一行是错误的，会出现referenceerror,该类函数只能在自己内部被使用
  foo();
  //显示的是function
  showOne();
  * 也有形如 var func=new Function('x','y','return x*y');这样的函数声明。

10. 函数的引用顺序中，

>var f = function() {
  console.log('1');
}
function f() {
  console.log('2');
}
f() // 1
这个是因为变量声明法和函数声明在js中区别，
同时，将下面的语句换成函数声明的话，则不会报错
f();
var f = function (){};//会包undefined的错误

11. 函数的作用域

>var x = function () {
  console.log(a);
};
function y(f) {
  var a = 2;
  f();
}
y(x)//外部定义的函数无法直接使用函数内部的变量，所以这里是错误的*正确的使用是，声明var a=1的全局变量*。同时这个函数也被当做变量使用。

12. 如果函数参数是复合类型的值（数组、对象、其他函数），传递方式是传址传递（pass by reference）。也就是说，传入函数的原始值的地址，因此在函数内部修改参数，将会影响到原始值。*而数值、字符串、布尔值则不会*。 *注意，如果函数内部修改的，不是参数对象的某个属性，而是替换掉整个参数，这时不会影响到原始值*。

>var obj = {p: 1};
function f(o) {
  o.p = 2;
}
f(obj);
obj.p // 2
如果改变的是整体，而不是某个属性的时候，则不会影响原始值。
var obj = [1, 2, 3];
function f(o){
  o = [2, 3, 4];
}
f(obj);
obj // [1, 2, 3],这里是整体的改变了，而不是像上面那个一样,改变某个属性

13. 下面这段代码中，

>var a=0;
function change(){
     a=3;
}
change(a);//3但是如果函数改为下面
function change(a){
     a=3;
}
change(a);//a=0,因为change()函数中，声明了a变量，类似于var a；

14. 函数中默认自带arguments对象，指带的是函数中的参数数组，js中允许函数中声明形参，但使用实参。但arguments不是数组，因为一些数组的方法在他身上不能使用。

>var f = function(one) {
  console.log(arguments[0]);
  console.log(arguments[1]);
  console.log(arguments[2]);
}
f(1, 2, 3);

15. **闭包**的最大用处有两个，*一个*是可以读取函数内部的变量，*另一个*就是让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在。请看下面的例子，闭包使得内部变量记住上一次调用时的运算结果。*注意:*外层函数每次运行，都会生成一个新的闭包，而这个闭包又会保留外层函数的内部变量，所以内存消耗很大。
16. 立即调用函数需要深入理解一下。*作用:*它的目的有两个：一是不必为函数命名，避免了污染全局变量；二是IIFE内部形成了一个单独的作用域，可以封装一些外部无法读取的私有变量。
17. js中运算符两边的变量如果不是不是期待的变量,则将会将其自动转换成相应的变量，但是 *+*，这个运算符，有些特殊

>function stringCal(){
    var a='1';
    var b='2';
    var c=a-b;//结果是-1
    alert(c);
    var d=a+b;
    alert(d);//结果是12
}

18. js中的缺省显示

>function showDefault(mess){
   mess=mess||'默认值';
   return mess;
}
console.log(showDefault('A级'));//如果showDefault()中无值，则输出'默认值',有值则输出函数中的实参。

19. 代码中自增，++放在变量前和变量后是不一样的，放在变量前面，贼则等同于+=1。
20. JSON中的要求 
 * 字符串必须使用双引号表示，不能使用单引号
 *  同时键名必须是双引号
 *  复合类型的值只能是数组或对象，*不能*是函数、正则表达式对象、日期对象。
 *  简单类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和null（不能使用NaN, Infinity, -Infinity和undefined）

21. 认真看this的用法
22. js中constructor function的定义如下

>var showConstruct=function(p){
    this.p=p;
}
 var objContruct=new showConstruct('contructor function');
 console.log(objContruct.p);//输出contructor function

23. call方法的参数，应该是一个对象。如果参数为空、null和undefined，则默认传入全局对象。call方法改变的是this的指向。

>var name='Tony'
function showThisWindow(){
    return this.name;
}
objTransfer={name:'hello'};
alert(showThisWindow.call(window));//输出的是Tony，call中使用的实参是objTansfer的时候,则输出的是hello。

24. apply的方法与call类似，都是改变this的指向，但function.call(obj,argument1,argument2,...)将函数的参数是一个个输入，但function.apply(obj,[argument1,argument2,...]),则是将参数一数组的行事传给函数。bind 则是绑定对象，并返回函数，并不是像前面两个一样立即执行，如果bind需要立即执行的话，则需要()运算符。*可以根据英文含义来区分三者,bind只是绑定，前两者都是调用、应用*



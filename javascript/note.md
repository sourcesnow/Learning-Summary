# 2017-03-18   
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
25. js中的prototype只能使用在构造对象上，不能使用在实例上

>function showProto(name){
  this.name=name;
  //this.age=age;
  this.func=function(){
    console.log('Hello');
  }
}
showProto.prototype.age=35;
var instanceExam=new showProto('protoType');
var instanceTwo=new showProto('jason');
alert(showProto.prototype.constructor);//注意这里使用的是构造对象，不能将其改为instanceTwo
**注意构造函数自身没有构造函数，继承自prototype,可以使用hasOwnProperty()函数进行查看**

26. __proto__与prototype之间的区别，一个用于实例化的对象，一个用于构造函数本身。上面的代码如果想使用实例化的对象来获得prototype的构造函数的话，可以通过将showProto.prototype.constructor改为intanceExam.__proto__.constructor。prototype是函数对象专有的属性，而__proto__则是所有对象都有的，包括函数。

>具体之间的区别是，见下图
!['关于__proto__与prototype']("__proto__.jpg" '__proto__与proototype')

27. ajax事件,如下

>ajax的事件是： 
ajaxComplete(callback) 
ajaxError(callback) 
ajaxSend(callback) 
ajaxStart(callback) 
ajaxStop(callback) 
ajaxSuccess(callback)

28. label中的使用，结合其for属性能指定其为那个input服务，例如下面代码，点击label则可以获得input中的点击事件。

> <label for="nameone">Name:</label><input type="text" name="nameone" id="
>  nameone" onclick="label()">
>label标签来定义表单控制间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的 表单控件上。

29. js中的出来对象之外，所有类型都是不可变的（值本身无法被改变）。例如，与 C 语言不同，JavaScript 中字符串是不可变的（如，JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变）。我们称这些类型的值为“原始值”。
30. js中存储数据的内存格式
* 栈：原始数据类型（Undefined，Null，Boolean，Number、String）
* 堆：引用数据类型（对象、数组和函数）
  两种类型的区别是：存储位置不同；
  原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
  引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；*引用数据类型在栈中存储了指针*，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体

31. 区分null与undefined [参考](http://www.ruanyifeng.com/blog/2014/03/ undefined-vs-null.html) **null是一个对象**
32. 事件处理机制，冒泡和事件捕获机制
33. JavaScript的函数的调用有以下几种方式：作为对象方法调用，作为函数调用，作为构造函数调用，和使用 apply 或 call 调用。
34. this的一个总原则：this指永远都是，调用函数的那个对象。
35. **apply,call的作用就是改变函数的调用对象**
36. setTimeout(,)如果它里面调用的是某个函数的方法的话，则此时的this，指向的是window

> var one=1;
> var testOne={
> one:12,
> two:function(){alert(this.one);}};
> setTimeout(testOne.two,1000);//输出则会是1，不是2。










[参考](http://javascript.ruanyifeng.com)



# DOM的操作总结
## 操作函数汇总
  1. 选取element,使用document.getElementById('idname'),document.getElementsByTagName('tagname'),document.getElementsByClassName('classname')等，*（注意这里的element是复试）*使用各种不同类型的方法。以上是直接调取元素。也可以通过css样式来调取元素，document.querySelector('#idName')效果等同于document.getElementById('idname'),同时还有,parentNode.querySelectorAll(),选取parentNode中元素。
  2. 通过document.createElement(''),创建元素，里面放置是，标签的名称，例如div,table,p,ul,li等(此处注意使用的使用document而不是父节点的名称),创建好之后，就通过parentNode.appendChild()，将它们添加到父节点里面去。同时也可以通过parentNode.insertBefore('elementName',referNode(就是待插入元素想插入位置之后的元素))函数。
  3. 获取孩子节点的方法，通过parentNode.children[],或者parentNode.childNodes[]的方法来获得,*但两者之间有区别,同时两个返回的是类似于数组的对象*,通过后面的node与element之间的区别来进行了解。还有parentNode等,firstElementChild,lastElementChild,nextElementSibling,previousElementSibling等
  4. 同时可以移除孩子节点，removeChild,replaceChild等
  5. 属性:通过getAttribute获得属性,例如getAttribute('name')获得name的属性值，通过setAttribute来设置属性，例如setAttribute('name','helloId'),将name属性设置为helloId,*记住如何要改变样式属性的话，通过setAttribute('style','background:red')，来不能直接设置成setAttribute('background','red')，因为element的属性中没有background这个属性，这个类似于设置node.style.background='red,于第一个效果一致，也可以改变样式表*,removeAttribute()，移除属性。
  6. 可以操作innnerHTML,outterHTML,innerText,outterText之间的区别，前者设置html文件属性。同时修改text的内容使用的是，appendData()。
  * node.innnerHTML='<b>Hello</b>'与node.innerText='<b>Hello</b>',来具体查看差别。
  
## node与element之间的区别
 1. element是node中的一个类型，node还有好几种类型。node是一个中数据结构的概念,树的基本组成元素,element则是xml中的数据元素,元素是一个小范围的定义，必须是含有完整信息的结点才是一个元素，例如<div>...</div>但是一个结点不一定是一个元素，而一个元素一定是一个结点。
 2. node的类型
  *  Element
  *  Text
  *  Attribute
  *  RootElement
  *  Comment
  *  Namespace
 3. 通过nodeType查看一个element的node属性。
 

>可以通过[node与element之间的差别]('http://www.cnblogs.com/season-huang/p/4322451.html')来查看更详细。
  

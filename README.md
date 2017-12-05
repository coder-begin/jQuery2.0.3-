## jQuery内部方法（使用jQuery版本是2.0.3）【工具方法】
*  **$.parseHTML(要创建的标签,上下文,是否创建script) : 返回一个创建完的标签数组**
>($.parseHTML("<li></li><li></li><li></li><script></script>"),document,false)
>返回:["li元素对象","li元素对象"] (当第三个参数是true的时候就会创建script元素对象)

* **$.merge(arr1,arr2):这个方法对外提供的是合并两个数组,但是如果使用一个数组和一个对象进行合并就会形成一个对象** 
>$.merge([0,1,2],{0:6})会返回一个对象
{ 
  0:0,
  1:1,
  2:2,
  3:6,
  length:4
}
> 如果传入的对象属性名不是数字那么合并完过后属性名就是undefined
* **makeArray(类数组对象,特殊的对象):当传入两个参数的时候类将对象转成特殊对象,特殊对象是一个有length属性的对象**
>var oLi=document.getElementsByTagName("li");

> makeArray(oLi,{0:0,1:1,length:5})----->{0:0,1:1,2:li,3:li,4:lo,length:5}

* **pushStack():jQuery内部的入栈方法:将选中的元素新添加进去**
>$("div").pushStack( $("span") ).css()--->进行这样的操作那么操作的就是栈顶的元素span

* **jQuery中加载函数有三种方法其中内部调用顺序如下:$(function(){})--->$(document).ready(function(){})--->jQuery.ready.promise().done( fn )--->readyList.resolveWith( document, [ jQuery ] ),这是一个Promise执行的过程。**

### 1. $.extend()
* **$.extend()当传入多个对象自变量的时候是向第一个对象自变量身上扩展方法**
>var a={};

>$.extend(a,{name:"GodCoder"},{age:"22"})---->a={name:"GodCoder",age:"22"}
* **浅拷贝:就是上面的传入两个对象自变量的时候,浅拷贝在被拷贝的属性是对象的时候一旦拷贝完成的对象相应的属性发生更改,被拷贝元素的相应属性也会发生更改**
>var a={}

>var b={name:{age:12}}

>$.extend(a,b)

>a.name.age=13;

>console.log(b.name.age)----->13//就发生了更改

* **深拷贝:和浅拷贝不一样的是深拷贝就是完全的复制,拷贝元素和被拷贝元素之间在没任何关系**
>var a={}

>var b={name:{age:12}}

>$.extend(true,a,b)  //加上true这个参数

>a.name.age=13;

>console.log(b.name.age)----->12//没变

### 2. jQuery加载函数方法
* **$(function(){})**
* **$(document).ready(function(){})**
* **$(document).on("ready",function(){})**

### 3. holdReady:
>使用延迟加载,当要是用的内容需要之前的js文件加载完成才能执行的时候使用$.holdReady(true)来使得之后的jQuery内的代码无法先执行，只有等调用$.holdReady(false)的时候才会执行.

> 使用script引入文件$.getScript("a.js",function(){})

>然后需要在前面的js文件加载完才能执行之后的函数时

>先使用$.holdReady(true)来使得后面的$(function(){})里面的内容不会先执行,需要的等上面的js加载完成后在回调中释放$.holdReady(false)，才能执行。

### 4. ready:DOM加载完成后的加载函数
```
$.ready(function(){})效果和$(function(){})一样
```
### 5. isFunction判断是否是函数

### 6. isArray：判断是否是数组

### 7. isWindow:判断是否是Window对象

### 8. isNumeric:判断是否是number类型

### 9. type:判断数据类型,不是只有5中基本类型还有Date...都可以判断

### 10. isPlainObject判断是否是对象自变量，只有{}和new Object()这两种类型会返回true

### 11. isEmptyObject:判断是否是空对象

### 12. parseJSON：解析JSON的方法

### 13. noop:返回空函数

### 14. globalEval：将一个局部变量变成全局变量

### 15. camelCase:转驼峰函数
```
"-ms-transform"--->"msTransform"
"-webkit-transform"--->"WebkitTransform"
```
### 16. nodeName：判断node节点节点名
```
$.nodeName(document.body,"body")//返回true
因为document.body的节点名就是body
```
### 17. each:遍历函数,可以遍历所有类数组,不只是jQuery对象,数组，json...都可以遍历

### 18. 

### 参考[妙味课堂](http://2017.miaov.com)关于jQuery部分的视频(有兴趣的可以去看一下)
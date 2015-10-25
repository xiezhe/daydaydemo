###包装对象

### 基本类型都有包装对象：String Number Bollean

> 基本类型找到对应的包装对象类型，然后包装对象把所有的属性和方法都给了基本类型，然后包装对象消失。

### 原型链
### 实例对象和原型之间的链接叫原型链(\_proto\_)
> Object对象类型是原型链的最外层（Obeject.prototype）
[例子](demo4.html)

###面向对象的一些属性和方法

* hasOwnProperty查看对象是否自身独有的属性 [例子](demo5.html)

<pre>
	var arr = [];
	arr.num = 1;
	Array.prototype.num2 = 2;
	alert(arr.hasOwnProperty('num'))//true;

</pre>

*constructor:查看对象的构造函数
** 每个对象都会自动添加constructor属性 
** for in 时有些属性找不到
** 避免修改constructor属性
[例子](demo6.html)
<pre>
	function Aaa(){}
	var a = new Aaa();
	alert(a.constructor)//function Aaa(){}
</pre>
[例子](demo7.html)

<pre>
	//做数组的判断
	var a = []
	alert(a.constructor == Array)//true;
</pre>
> constructor改写

	function Aaa(){}
	//此时prototype被改写
	Aaa.prototype = {
		//修正constructor则解决了这个问题
		constructor: Aaa,
		name: '111'
	};
	var a1 = new Aaa();
	alert(a1.constructor)//输出的是json对应的constructor

- instanceof

> 判断实例对象与构造函数在原型链上是否有关系
<pre>
    function Aaa(){};
    var a = new Aaa();
    console.log(a instanceof Aaa)//true;
    console.log(a instanceof Object)//true;
    console.log(a instanceof Array)//false;
</pre>

### toString

- object的方法
系统对象的toString都是自己的，自己写的对象都是通过原型链找到Object下的toString方法

<pre>
	function Aaa(){}
	var a = new Aaa();
	alert(a.toString == Object.toString);//true
	var arr = [];
	alert(arr.toString == Object.toString);//false
</pre>
	toString():把对象转换成字符串
	//进制转换
	var num = 222;
	num.toString(16);
	- 作类型判断
	var arr = [];
	console.log(Array.prototype.toString.call(arr))//arr 很准确的哈哈哈

> iframe里判断属于什么类型
 
	window.onload = function(){
		var oF = document.createElement('iframe');
		document.body.appendChlid(oF);
		var ifArray = window.frames[0].Array;
		var arr = new ifArray();
		alert(arr.constructor == Array)//false 判断错误
		alert(arr instanceof Array)//false同样是判断错误
		alert(arr.prototype.toString.call(arr)=='[object Array]')//true 
	}
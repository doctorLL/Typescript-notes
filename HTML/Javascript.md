#### 防抖节流

```js
防抖： 每次点击重新开始计时；
场景： 按钮提交，搜索框联想场景。
function debounce(func,wait){
	let timeOut;
	return function (){
		let that = this;
		let args = arguments
		cleatTimeout(timeOut);
		timeOUt = setTimeout(()=>{
			func.apply(that,args);
		},wait)
	}
}
节流: 多次点击一定时间内只触发一次；
场景： 拖拽、缩放
时间戳：
function throttle(func,wait){
    let that,args;
    let time = 0;
    return function(){
        that = this;
        args = arguments;
        let day = +new Date();
        if(day - time > wait){
            func.apply(that,args);
            time = day;
        }
    }
}
定时器：
function throttle(func,wait){
    let that, args;
    let time = null;
    if(!time){
        that = this;
        args = arguments;
	 	time = setTimeout(()=>{
			clearTimeout(time);
            func.apply(that,args)
        },wait)
    }
}
```

#### 闭包：

​	函数执行后返回一个内部函数，内部函数持有被执行函数作用域的变量，即形成了闭包；

闭包可以读取到函数中的变量，可以把变量存储在内存中，所有要慎用闭包。

##### 原理：

​	预编译阶段，如果检测到内部函数使用了外部函数变量，会在内存中创建一个“闭包”对象用来保存对应的变量值； 执行完后，函数执行上下文被销毁，函数对“闭包”对象的引用也会被销毁，但是因为内部函数还持有“闭包”的引用，内部韩式可以继续使用外部函数的变量。

##### 优点：

​	内部访问外部函数作用域中的变量，避免变量全局污染，把变量存在独立作用域，作为私有成员。

##### 缺点： 

​	内存消耗，无法进行垃圾回收。

##### 场景：

​	场景一： 模块封装（之前的操作）

```
var Bibao = (function(){
	var foo = {};
	function Bibao(){};
	Bibao.prototype.bar = function bar(){
		return foo;
	};
	return Bibao;
})
```

#### 伪类，伪元素

##### 伪类：

​	用来选择一些DOM树之外的信息，不能被选择器选择的元素；

比如： :hover :active

##### 伪元素：

​	DOM树没有定义的虚拟元素，核心：需要创建通常不存在于文档中的元素，

比如：::before  :: after

二者都不存在于DOM树中。

伪类基于DOM元素而产生的不同状态，伪元素能够创建在DOM树中不存在的抽象对象。

#### 封装对象

使用new 声明的一个对象为：封装对象。

#### （原型）继承：

````
son.prototype = object.create(fa.prototype);
object.setPrototypeOf(son.prototype, fa.prototype;

function Fun(){}
var a = new Fun();
a instanceof Fun; // a的原型链上是否有指向Fun.prototype的对象
````


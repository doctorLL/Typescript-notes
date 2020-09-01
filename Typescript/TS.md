### 基本类型：

```
boolean、number、string、symbol
Array：let list: number[] = [12,3];
元组(Tuple)： let x: [string,number];
枚举(enum)：enum Color {red,green,blue}
		let c:Color = Color.red;
Any: let list:any[] = [1,true,'free'];
void:表示没有任何类型
	function  fun():void{}
	当给一个变量声明为void类型时，只能赋值为undefined和null；
Null和Undefined默认情况下是所有类型的子类型。
Never：永不存在值得类型。
Object
```

#### 类型断言：

```
let value:any = "this";
let str:number = (<string>value).length;
另：let str:number = (value as string).length;
```

### 变量声明

```js
let [a,b] = [1,3];
[b,a] = [a,b];
let {name: newName} = {name:"a"};  //newName = "a"
```

### 接口

```typescript
interface LabelValue{
	label: string,
    width?: number,				//可选属性
}
funtion printLabel(labelObj: LabelValue):{color:string, width: number}

只读属性：
interface Point {
    readonly x:number,
    readonly y:number
}
只读属性的变量不可以被改变，也不可以赋值给其他变量。
但可以使用断言重写：
let arr: ReadyonlyArray<number> = [1,3];
let a = arr as number[];
如果传入的属性在接口中没有定义时可以使用 “字符串索引签名”：
interface SquareConfig{
    name?:string,
    [propName: string]: any
}
function createObj(config:SquareConfig):{name: string}{}
let mySquare = createObj({name:"小明",age:12})
```

###### 函数类型：

```
接口可以描述函数类型：
interface SearchFunc{
	(source: string, substring: string):boolean;
}
let mySearch:SearchFunc;
mySearch = function(src,sub):boolean{
	return 1;
}
```

###### 可索引的类型：

```
可索引类型具有一个 “索引签名”， 它描述了对象索引的类型
类似数组下标和对象的key
interface StringArr {
	readonly [index:number]: string	
}
let myArr:StringArr = ["小明"];
let name:string = myArr[0];			//name: "小明"
```

###### 类类型

```typescript
强制一个类去符合某种契约。
interface ClockInterface {
	currentTime: Date;
	setTime(d:Date);
}
class Clock implements ClockInterface{
	currentTime: Date,
	constructor(h: number, m: number){}
	setTime(d:Date){
		this.currentTime = d;
	}
}
类静态部分与实例部分的区别？？？？（待补充）
```

###### 继承接口

```typescript
interface Shape {
    color: string
}
interface Square extends Shape {
    length:number
}
let square = <Square> {};
square.color = "red";
一个接口可以继承多个接口
interface inter extends inter1,inter2...{}
```

###### 混合类型

```typescript
前面提到的所有的类型都可以在一个接口中实现
interface Counter{
	(state:number) : string,
	interval: number,
	reset(): void
}
function getCounter():Counter{
	let counter = <Counter>function (state:number){};
	counter.interval = 123;
	counter.reset = function() {};
	return counter;
}
let c = getCounter();
c(12);
c.reset();
c.interval = 121212;
```


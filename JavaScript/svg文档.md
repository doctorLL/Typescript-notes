## SVG.js 使用笔记

```
引入
<script src="https://cdn.jsdelivr.net/npm/@svgdotjs/svg.js@3.0/dist/svg.min.js"></script>

实例化：let draw = SVG().addto('body').size('100%', '100%');
```

##### 矩形

```js
let rect = draw.rect(100,100).attr({fill: '#F40',x:100,y:100});
rect.radius(10);  //圆角
```

##### 圆形

```js
let circle = draw.circle(100);
```

##### 椭圆

```js
var ellipse = draw.ellipse(100,200)  // ellipse(x,y)
```

##### 线

```js
let line = draw.line(0,0,400,150).stroke({width: 1,color:'#000'})
line.animate(2000).plot(50,100,400,100).stroke({width: 10}); 
// plot()方法更新线的位置
```

##### 折线

```js
let polyline = draw.polyline([[0,0],[120,120],[170,120],[170,200]]).stroke({width:2,color:'yellow'}).fill('none');
polyline.animate(3000).plot([[0,0],[20,20],[70,20],[70,100]])
```

##### 路径

```js
let path = draw.path('M0 0 H50 A20 20 0 1 0 100 50 v25 C50 125 0 85 0 85 z');
let length = path.length(); //长度
let point = path.pointAt(105); // 指定长度上的点
```

##### 文本

````js
let  text = draw.text('文本\n内容');
var text = draw.text(function(add) {
        add.tspan('Lorem ipsum dolor sit amet ').newLine()
        add.tspan('consectetur').fill('#f06')
        add.tspan('.')
        add.tspan('Cras sodales imperdiet auctor.').newLine().dx(20)
        add.tspan('Nunc ultrices lectus at erat').newLine()
        add.tspan('dictum pharetra elementum ante').newLine()
        })
tspan.plain('I do not have any expectations.')  //纯文本
text.length()			//长度
text.font({
    leading（与调用leading()setter的方法相同）
    anchor（将设置text-anchor属性）
    family（将设置font-family属性）
    size（将设置font-size属性）
    stretch（将设置font-stretch属性）
    style（将设置font-style属性）
    variant（将设置font-variant属性）
    weight（将设置font-weight属性）
})				// 设置字体样式
路径
text.path(path).font({});
获取文本路径
textPath = text.textPath().attr('starOffset','50%');

tspan
tspan.dx();  //left
tspan.dy:  //top

````

##### 文本路径

```js
var textpath = draw.textPath('Some Text along a path', 'M 100 200 C 200 100 300 0 400 100 C 500 200 600 300 700 200 C 800 100 900 100 900 100');
```

##### 渐变

```js
var gradient = draw.gradient('linear', function(add) {
  add.stop(0, '#333')
  add.stop(1, '#fff')
})
rect.attr({ fill: gradient }) // 使用

stop({ offset: 0, color: '#333', opacity: 1 })
from(0,0).to(0,1);
radius(0.5) // 半径
gradient.update(function(add){
    add.stop(0.1, '#333', 0.2)
  	add.stop(0.9, '#f03', 1)
})
```

##### 模式 Pattern()

```js
var pattern = draw.pattern(20, 20, function(add) {
  add.rect(20,20).fill('#f06')
  add.rect(10,10)
  add.rect(10,10).move(10,10)
})
rect.attr({ fill: pattern })
```

###### 创建/引用元素

```js
let rect = SVG('rect.my-class').fill('#F60') // 寻找相匹配的第一个元素；

选择子元素/元素
draw.children();
draw.clear();	//清除子元素
draw.each(()=>{});
draw.first();
draw.get(1);
draw.has();
draw.index(); // 返回子元素所在的位置，没有时返回-1
draw.last();
rect.root(); // 返回根元素

var draw   = SVG().addTo('#drawing')
var nested = draw.nested().addClass('test')
var group  = nested.group()
var rect   = group.rect(100, 100)

rect.parent()           //-> returns group
rect.parent(SVG.Svg)    //-> returns nested
nested.parent(SVG.Svg)  //-> returns draw
rect.parent(SVG.G)      //-> returns group
rect.parent('.test')    //-> returns nested

rect.reference(); 

```

###### 属性

```js
rect.attr({});
rect.attr('fill',null) // 删除属性
let x = rect.attr('width'); //获取属性
let attributes = rect.attr(); // 获取所有属性
let attributes = rect.attr(['width','height']); // 获取指定属性
```

##### 定位

```js
rect.attr({x:100,y:100});
```

##### 移动

```
rect.move(x,y);
rect.x();
rect.y();
rect.center();
rect.cx();
rect.cy();
rect.dmove();
rect.dx();
rect.dy();
```

##### 调整大小

```js
rect.size();
rect.width(); // 传入参数设置宽度，不传获取宽度
rect.height();
circle.radius(); // 半径
```

##### 填充

```
rect.fill();
rect.fill('img.jpg');// 填充图片
stroke()和fill()类似
```

rect.opacity()

##### transfrom()

```js
element.transfrom({
    translate:[],
    rotate: 5,
    scale: 2,
    skew:[],		// 倾斜
    both: true,
    origin:[50,50],
    position:[x,y],
    relative:[x,y]
})
element.flip('x'); //给定元素的旋转轴
```

```
element.css() // 与attr()类似
element.hide();
element.show();
element.visible(); // 是否可见
element.addClass();
element.classes(); // 获取节点的class
element.hasClass();
element.removeClass();
element.toggleClass(); // 切换class
rect.data('key',{value: {data: 0.3});
```

##### remember

```
rect.remember({
	oldFill: rect.attr('fill'),
	oldStorke: rect.attr('strocke')
})  // 将数据存储在内存中
清楚内存
rect.forget('oldFill')
```

##### DOM树添加

```js
var rect = draw.rect(100,100);
var group = draw.group;
group.add(rect);  //添加

rect.addTo(group); //添加到
rect.clone();
group.put(rect);
rect.potIn(group);
rect.remove();
rect.replace(draw.circ;le(200)); //替换
toRoot() toParent();
ungroup() // 分解一个组将其所有元素放入该组的父级，传递参数时可以指定组元素移动到哪个容器

```

```
flatten
递归分解所有容器并展平整个结构
group.flatten(container) // 递归取消组合中所有元素，并将其放入到给定的容器中
```

##### 插入元素

```
rect.after(circle); //在最后插入
rect.before(circle);
rect.insertAfter(circle); // 将当前元素插入到所传元素之后
rect.insertBefore(..)
rect.back(); // 将元素移到后面
rect.backward(); //向后移
rect.front(); // 移到最前面
rect.forward(); // 向前移
rect.next(); // 获取下一个元素
rect.position(); // 获取位置
rect.previous(); // 获取上一个元素
rect.siblings(); //获取所有兄弟节点，包括本身
var point = path.point(e.pageX,e.pageY); // 将屏幕坐标转换为元素坐标

var rect = draw.rect(100,100).move(50,50);
rect.inside(25,10) // 检查给定点是否在元素边界框内

element.bbox(); // 元素的边界框
element.rbox(); // 元素的变形框

drawing.viewbox(10,10,500,600) // 设置元素的视图框。
```

##### 动画

```
animate({
	duration: 2000, //多长时间，
	delay: 1000, // 延时
	when: 'now', // 动画起点，now absolute start relative last after
	swing； true,
	times: 5,
	wait: 200
})

```


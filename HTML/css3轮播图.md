```html
<div class="box">
	<ul>
        <li 1></li>
        <li 2></li>
        <li 3></li>
        <li 4></li>
        <li 1></li>
    </ul>
</div>
<style>
    box{
        overflow:hidden;
    }
    ul{
        listStyle: none;
        width:100%;
        white-space: nowrap
        animation: lb 10s linear infinite;
    }
    li{
        width:100%;
        diaplay: inline-block;
    }
    @keyframes lb{
        0% {
					transform: translateX(0);
				}

				28% {
					transform: translateX(0);
				}

				33% {
					transform: translateX(-100%);
				}

				61% {
					transform: translateX(-100%);
				}

				66% {
					transform: translateX(-200%);
				}

				94% {
					transform: translateX(-200%);
				}

				100% {
					transform: translateX(-300%);
				} 
    }
</style>

```

#### 伪类和伪元素

伪元素实质上是元素，但是不存在于DOM树中，是虚拟的元素，只是逻辑上存在，不能通过js来操作，只能在CSS渲染层加入。

伪类：用于向某些选择器添加特殊效果
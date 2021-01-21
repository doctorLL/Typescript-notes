#### 自定义指令

```vue
directives:{
	focus:{
		inserted: function (el){
			el.focus()
		}
	}
}
<input v-focus>
```

##### 钩子函数

bind: 只调用一次，指令第一次绑定到元素时调用。

inserted: 被绑定元素插入父节点时调用（父节点只要存在即可调用）；

update： 无论绑定值是否变化，只要绑定元素所在模板被更新即调用；

componentUpdated：被绑定元素所在模板完成一次更新周期时调用；

unbind： 指令与元素解绑时调用，只调用一次。

##### 参数：

| 入参     | 说明                                               |
| -------- | -------------------------------------------------- |
| el       | 绑定的元素，可直接操作DOM                          |
| binding  | 绑定对象                                           |
| vnode    | 编译生成的虚拟节点                                 |
| oldVnode | 上一个虚拟节点，仅在update与componentUpdated中可用 |

|    属性    | 说明                                                         | 示例                                        |
| :--------: | ------------------------------------------------------------ | ------------------------------------------- |
|    name    | 指令名，不包含前缀 `v-`。                                    | v-focus 中的 focus。                        |
|   value    | 指令所绑定的值（计算后）。                                   | `v-focus=“1 + 2”` 中的 3。                  |
|  oldValue  | 指令所绑定的前一个值，无论值是否改变都有值，且仅在 update 与 componentUpdated 中可用。 | -                                           |
| expression | 绑定的值的字符串形式（不计算）。                             | `v-focus=“1 + 2”` 中的  `1 + 2`。           |
|    arg     | 传递给指令的参数。                                           | `v-focus:xxx` 中的 xxx。                    |
| modifiers  | 包含修饰符的对象。                                           | `v-focus.a.b` 中，为 `{a:true, b:true}`。。 |

##### 多值入参

```vue
<div id="app3">
    <div v-deniro-directive2="{title:'物理学家新发现四起黑洞相撞事件',content:'物理学家探测到了它们向地球发来的引力波'}"></div>
</div>

Vue.directive('deniro-directive2', {
    bind: function (el, binding, vnode) {

        el.innerHTML =
            'title:' + binding.value.title + '<br>' +
            'content:' + binding.value.content + '<br>';
    }
});
```

##### 动态指令参数

```vue
<div v-pin:[direction]="260"></div>

data(){
	return direction: 'left'
}
directives:{
	pin: {
		bind: function(el,binding, vnode){
			el.style.position = 'fixed';
			var s = (binding.arg == 'left' ? 'left': 'top');
			el.style[s] = binding,value + 'px'
		}
	}
}
根据需求动态修改元素定位。
```

#### vue代理配置：

```js
proxy:{}
function createProxy(){
    const envObj = process.env;
    const envObjKeys = Object.keys(process.env);
    const proxy = {};
    envObjKeys.forEach((ele)=>{
		if(ele.indexOf('VUE_APP_IP_')===0){
            const variable = ele.split("_");
            const gateway = variable.pop();
            const isREWITE = variable.pop();
            const proxyObj = {
                target: envObj[ele],
                changeOrigin: true,
            };
            const cssLoader = {
                loader: 'css-loader',
                options: {
                  sourceMap: options.sourceMap,
                  minimize:true
                }
          	};
            if(isREWITE === 'REWRITE'){
				proxyObj.pathRewrite = {
					[`^${getway}`]:'',
                }
            }
            proxy[gateway] = proxyObj;
        }
    });
    return proxy;
}


  //vue-cli3.0 里面的 vue.config.js做配置
devServer: {
    proxy: {
        '/rng': {     //这里最好有一个 /
            target: 'http://45.105.124.130:8081',  // 后台接口域名
            ws: true,        //如果要代理 websockets，配置这个参数
            secure: false,  // 如果是https接口，需要配置这个参数
            changeOrigin: true,  //是否跨域
            pathRewrite:{
                '^/rng':''
            }
        }
    }
  }
```


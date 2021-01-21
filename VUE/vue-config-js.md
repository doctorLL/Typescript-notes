```js
module.exporte = {
    publicPath: '/',    //基本URL
  	outputDir: 'dist', //打包时的目标目录
    assetsDir: '' , // 放置生成的静态资源的（相对于outputDir）的目录
    filenameHashing: true, // 生成的静态资源在文件名中包含了hash以便更好地控制缓存。
    lintOnSave:'default/error/boolean/warning', //是否使用eslint-loader
    （或者：lintOnSave: process.env.NOOE_ENV == 'development'）
    productionSourceMap: false , // 生产环境中是否需要 source map 
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
    }，
    
}
```


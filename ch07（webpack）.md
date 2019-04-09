```js
let path = require('path')
let HTMLWebpackPlugin = require('html-webpack-plugin')
module.exports = {
    devServer:{
        port:3000,
        progress:true,
        contentBase:'./build',
        open:true,
    },//开发服务器配置

    mode:'production',//配置开发或者生产环境
    entry:'./src/index.js',//入口
    output:{            //出口
        filename:'bundle.[hash:8].js',//生成带哈希的文件名
        path:path.resolve(__dirname,'build')
    },
    plugins:[
        new HTMLWebpackPlugin({
             template: "./src/index.html",
             filename:"index.html",
             minify:{
                 removeAttributeQuotes:true,//移除不必要的双引号
                //  collapseWhitespace:true,//自动折叠空行
                
             },
             hash:true,
             })
    ]
    
}

```

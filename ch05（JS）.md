#JS相关

[近一万字的ES6语法知识点补充](https://juejin.im/post/5c6234f16fb9a049a81fcca5) 

[每个 JavaScript 工程师都应懂的33个概念](https://github.com/stephentian/33-js-concepts) 

[前端面试题讲解(THIS、构造函数、面向对象、堆栈内存以及闭包)](https://www.bilibili.com/video/av24383268) 

[JavaScript的es6详解](https://www.bilibili.com/video/av25438199) 

[一次弄懂Event Loop](https://juejin.im/post/5c3d8956e51d4511dc72c200) 

###跨域

原因：浏览器有一个同源策略

不同协议，不同域名（不同二级域名），不同端口都会造成跨域

常见的方法 jsonp CORS 

####jsonp

通过动态向HTML插入script标签来请求，只能get，不能post

####CORS 

实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。


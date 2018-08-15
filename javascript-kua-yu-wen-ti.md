# 前端跨域问题

## **哪些情况会产生跨域问题**

一个网站的网址组成包括协议名，子域名，主域名，端口号。比如 https://github.com/ ，其中https是协议名，www是子域名，github是主域名，端口号是80，当在在页面中从一个url请求数据时，如果这个url的协议名、子域名、主域名、端口号任意一个有一个不同，就会产生跨域问题。

即使是在 http://localhost:80/ 页面请求 http://127.0.0.1:80/ 也会有跨域问题

## 通过jsonp解决跨域问题

jsonp解决跨域问题的原理是，浏览器的script标签是不受同源策略限制\(你可以在你的网页中设置script的src属性问cdn服务器中静态文件的路径\)。那么就可以使用script标签从服务器获取数据，请求时添加一个参数为callbakc=?，?号时你要执行的回调方法。

[https://segmentfault.com/a/1190000011145364](https://segmentfault.com/a/1190000011145364)

同源策略下，某个服务器是无法获取到服务器以外的数据，但是html里面的img,iframe和script等标签是个例外，这些标签可以通过src属性请求到其他服务器上的数据。而JSONP就是通过script节点src调用跨域的请求。

当我们向服务器提交一个JSONP的请求时,我们给服务传了一个特殊的参数,告诉服务端要对结果特殊处理一下。这样服务端返回的数据就会进行一点包装，客户端就可以处理。

举个例子，服务端和客户端约定要传一个名为callback的参数来使用JSONP功能。比如请求的参数如下:

[http://www.example.net/sample.aspx?callback=mycallback](http://www.example.net/sample.aspx?callback=mycallback) 如果没有后面的callback参数，即不使用JSONP的模式，该服务的返回结果可能是一个单纯的json字符串，比如：{ foo : 'bar' }。但是如果使用JSONP模式，那么返回的是一个函数调用: mycallback\({ foo : 'bar' }\)，这样我们在代码之中，定义一个名为mycallback的回调函数，就可以解决跨域问题了。

##  通过CORS解决跨域问题

CORS的本质让服务器通过新增响应头Access-Control-Allow-Origin,通过HTTP方式来实现资源共享,让每个请求的服务直接返回资源.它使用了HTTP交互方式来确定请求源是否有资格请求该资源,并且通过设置HTTP Header来控制访问资源的权限.  
****

**后端设置一下response的header:**

```javascript
Access-Control-Allow-Origin: "*"
Access-Control-Allow-Methods: "GET"
Access-Control-Max-Age: "60"   
```

会先发一个option请求，它告诉了浏览器此后的60秒内,所有域都可以通过GET方法进行跨域访问该资源.然后浏览器自动再次发送了真正的GET请求,并返回对应的结果.  



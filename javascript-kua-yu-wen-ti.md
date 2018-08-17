# 前端跨域问题

## **哪些情况会产生跨域问题**

一个网站的网址组成包括协议名，子域名，主域名，端口号。比如 https://github.com/ ，其中https是协议名，www是子域名，github是主域名，端口号是80，当在在页面中从一个url请求数据时，如果这个url的协议名、子域名、主域名、端口号任意一个有一个不同，就会产生跨域问题。

即使是在 http://localhost:80/ 页面请求 http://127.0.0.1:80/ 也会有跨域问题

```text
URL                                      说明                    是否允许通信
http://www.domain.com/a.js
http://www.domain.com/b.js         同一域名，不同文件或路径           允许
http://www.domain.com/lab/c.js

http://www.domain.com:8000/a.js
http://www.domain.com/b.js         同一域名，不同端口                不允许
 
http://www.domain.com/a.js
https://www.domain.com/b.js        同一域名，不同协议                不允许
 
http://www.domain.com/a.js
http://192.168.4.12/b.js           域名和域名对应相同ip              不允许
 
http://www.domain.com/a.js
http://x.domain.com/b.js           主域相同，子域不同                不允许
http://domain.com/c.js
 
http://www.domain1.com/a.js
http://www.domain2.com/b.js        不同域名                         不允许
```

## 通过jsonp解决跨域问题

jsonp解决跨域问题的原理是，浏览器的script标签是不受同源策略限制\(你可以在你的网页中设置script的src属性问cdn服务器中静态文件的路径\)。那么就可以使用script标签从服务器获取数据，请求时添加一个参数为callbakc=?，?号时你要执行的回调方法。

[https://segmentfault.com/a/1190000011145364](https://segmentfault.com/a/1190000011145364)

同源策略下，某个服务器是无法获取到服务器以外的数据，但是html里面的img,iframe和script等标签是个例外，这些标签可以通过src属性请求到其他服务器上的数据。而JSONP就是通过script节点src调用跨域的请求。

当我们向服务器提交一个JSONP的请求时,我们给服务传了一个特殊的参数,告诉服务端要对结果特殊处理一下。这样服务端返回的数据就会进行一点包装，客户端就可以处理。

```javascript
  /*** 原生实现 ***/
 <script>
    var script = document.createElement('script');
    script.type = 'text/javascript';

    // 传参并指定回调执行函数为onBack
    script.src = 'http://www.domain2.com:8080/login?user=admin&callback=onBack';
    document.head.appendChild(script);

    // 回调执行函数
    function onBack(res) { 
        alert(JSON.stringify(res));
    }
 </script>
 
 /*** jquery ajax ***/
 $.ajax({
    url: 'http://www.domain2.com:8080/login',
    type: 'get',
    dataType: 'jsonp',  // 请求方式为jsonp
    jsonpCallback: "onBack",    // 自定义回调函数名
    data: {}
});


```

{% hint style="info" %}
 jsonp缺点：只能实现get一种请求。
{% endhint %}

## **document.domain + iframe跨域**

## **location.hash + iframe跨域**

##  **window.name + iframe跨域**

## **postMessage跨域**

## 通过CORS解决跨域问题

CORS的本质让服务器通过新增响应头Access-Control-Allow-Origin,通过HTTP方式来实现资源共享,让每个请求的服务直接返回资源.它使用了HTTP交互方式来确定请求源是否有资格请求该资源,并且通过设置HTTP Header来控制访问资源的权限.  
****

**后端设置一下response的header:**

```javascript
Access-Control-Allow-Origin: "*"
Access-Control-Allow-Methods: "GET"
Access-Control-Max-Age: "60"   

 res.writeHead(200, {
            'Access-Control-Allow-Credentials': 'true',     // 后端允许发送Cookie
            'Access-Control-Allow-Origin': 'http://www.domain1.com',    // 允许访问的域（协议+域名+端口）
            /* 
             * 此处设置的cookie还是domain2的而非domain1，因为后端也不能跨域写cookie(nginx反向代理可以实现)，
             * 但只要domain2中写入一次cookie认证，后面的跨域接口都能从domain2中获取cookie，从而实现所有的接口都能跨域访问
             */
            'Set-Cookie': 'l=a123456;Path=/;Domain=www.domain2.com;HttpOnly'  // HttpOnly的作用是让js无法读取cookie
        });
```

会先发一个option请求，它告诉了浏览器此后的60秒内,所有域都可以通过GET方法进行跨域访问该资源.然后浏览器自动再次发送了真正的GET请求,并返回对应的结果.  



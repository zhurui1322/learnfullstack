# HTML

## **DOCTYPE**

&lt;!DOCTYPE&gt;声明位于位于HTML文档中的第一行，处于 &lt;html&gt; 标签之前。告知浏览器的解析器用什么文档标准解析这个文档HTML5 中的写法&lt;!DOCTYPE html&gt;

## **display: block 和 inline 的区别**

常见的块级元素有 DIV, FORM, TABLE, P, PRE, H1~H6, DL, OL, UL 等等。  
常见的内联元素有 SPAN, A, STRONG, EM, LABEL, INPUT, SELECT, TEXTAREA, IMG, BR 等等。  
另外，SCRIPT, OBJECT, MAP, BUTTON, DEL, INS 这些元素，既可以作为块级元素，也可以作为内联元素。  
****

**display: block:** 

* DIV, FORM, TABLE, P, PRE, H1~H6, DL, OL, UL 
* 可包含block 和 inline 
* 从上至下，一个隔一个的布局的
* 可以响应 margin, width, height, max/min width/height 等属性声明

**display: inline** 

* PAN, A, STRONG, EM, LABEL, INPUT, SELECT, TEXTAREA, IMG, BR 等等
* 只能包含inline 元素
* 从左至右（也可能因为设置了direction而从右到左，或者从上到下）首尾相接，不间断的布局的
* 不想响应 margin, width, height, max/min width/height 等属性声明

**display: inline-block**

* **可以和其他元素共处与一行内；对内则让元素呈块级元素，可改变其宽高。**

{% hint style="info" %}
img tag本是inline, 经常需要设置宽高，所以一般设置为inline-block
{% endhint %}

**display: none:**

* 完全移除此元素

## **空void元素有那些**

空元素是在开始标签中关闭的。常见的空元素：&lt;br&gt; &lt;hr&gt; &lt;img&gt; &lt;input&gt; &lt;link&gt; &lt;meta&gt;

不过html5 需要用 &lt;br /&gt;来关闭空元素

## **浏览器内核的理解？** 

主要分成两部分：渲染引擎\(layout engineer或Rendering Engine\)和JS引擎。

渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等）

JS引擎则：解析和执行javascript来实现网页的动态效果。 最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

## **常见的浏览器内核有哪些？**

Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。\[又称MSHTML\]

Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等

Presto内核：Opera7及以上。 \[Opera内核原为：Presto，现为：Blink;\]

Webkit内核：Safari,Chrome等。 \[ Chrome的：Blink（WebKit的分支）\]

## **html5有哪些新特性？如何处理HTML5新标签的浏览器兼容问题？**

HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务功能。

绘画 canvas; 用于媒介回放的 video 和 audio 元素;

本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失; sessionStorage 的数据在浏览器关闭后自动删除;

语意化更好的内容元素，比如 article、footer、header、nav、section; 表单控件，calendar、date、time、email、url、search;

新的技术webworker, websocket, Geolocation;

支持HTML5新标签： IE8/IE7/IE6支持通过document.createElement方法产生的标签， 可以利用这一特性让这些浏览器支持HTML5新标签， 浏览器支持新标签后，还需要添加标签默认的样式。 当然也可以直接使用成熟的框架、比如html5shim

## **cookies，sessionStorage 和 localStorage 的区别？**

cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递。  
sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

存储大小：  
      cookie数据大小不能超过4k。  
      sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大多，5M或更大。  
  
有期时间：  
      localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；  
      sessionStorage  数据在当前浏览器窗口关闭后自动删除。  
      cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

## **HTML5的离线储存怎么使用工作原理能不能解释一下？**

首先manifest是一个后缀名为manifest的文件，在文件中定义那些需要缓存的文件，支持manifest的浏览器，会将按照manifest文件的规则，像文件保存在本地，从而在没有网络链接的情况下，也能访问页面。

当我们第一次正确配置app cache后，当我们再次访问该应用时，浏览器会首先检查manifest文件是否有变动，如果有变动就会把相应的变得跟新下来，同时改变浏览器里面的app cache，如果没有变动，就会直接把app cache的资源返回，基本流程是这样的。  
****

```markup
<html lang="en" manifest="index.manifest"> 定义在html头文件中
cache.manifest 文件:
CACHE MANIFEST
#version 1.3

CACHE:
    test.css                 可以缓存的文件

NETWORK:
 *                      离线时不可用的文件
FALLBACK:/html5/ 404.html           如果当前资源无法访问 用404来替代html5
```

可以通过js来手动更新本地缓存

`window.applicationCache.update()`  


manifest文件中的cache部分不能使用通配符，必须手动指定，这实在太让人不可理解，文件一多，就成了体力活。使用grunt 可以自动化生成manifest文件  
****

## **Label的作用是什么？是怎么用的？HTML5 feature**

label标签来定义表单控制间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。 radio button 点击text会自动选上button

`<label for="Name">Number:</label>  
<input type=“text“name="Name" id="Name"/>  
<label>Date:<input type="text" name="B"/></label>`  
****

## **10. HTML5的form如何关闭自动完成功能？**

自动完成可以让浏览器预测值，浏览器会根据之前的输入给出选项，类似自动补全

`autocomplete=off`  
****

## **如何实现浏览器内多个标签页之间的通信? \(阿里\)** 

WebSocket、SharedWorker； 也可以调用localstorge、cookies等本地存储方式；

localstorge另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件， 我们通过监听事件，控制它的值来进行页面信息通信  
  
****

## **Page Visibility API**

 HTML5 通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;  
  在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；

```javascript
function handleVisibilityChange() {
  if (document[hidden]) {
    videoElement.pause();
  } else {
    videoElement.play();
  }
}
document.addEventListener(visibilityChange, handleVisibilityChange, false);
```

##  **实现不使用 border 画出1px高的线**

```markup
<div style="height:1px;overflow:hidden;background:red"></div>
```

## **前端性能优化的方法**

\*\*\*\*

* 减少http请求次数通过webpack压缩请求：CSS Sprites, JS、CSS源码压缩、
* 图片大小控制合适；
* 网页Gzip，
* CDN托管，
* data缓存 
* 图片服务器。
* DNS预热
* 前端模板 JS+数据，减少由于HTML标签导致的带宽浪费，前端用变量保存AJAX请求结果，每次操作本地变量，不用请求，减少请求次数
* 用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能
* 当需要设置的样式很多时设置className而不是直接操作style
* 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作
* 避免使用CSS Expression（css表达式\)又称Dynamic properties\(动态属性\)
* 片预加载，将样式表放在顶部，将脚本放在底部  加上时间戳。
* 避免在页面的主体布局中使用table，table要等其中的内容完全下载之后才会显示出来，显示比div+css布局慢。 
* 对普通的网站有一个统一的思路，就是尽量向前端优化、减少数据库操作、减少磁盘IO。向前端优化指的是，在不影响功能和体验的情况下，能在浏览器执行的不要在服务端执行，能在缓存服务器上直接返回的不要到应用服务器，程序能直接取得的结果不要到外部取得，本机内能取得的数据不要到远程取，内存能取到的不要到磁盘取，缓存中有的不要去数据库查询。减少数据库操作指减少更新次数、缓存结果减少查询次数、将数据库执行的操作尽可能的让你的程序完成（例如join查询），减少磁盘IO指尽量不使用文件系统作为缓存、减少读写文件次数等。程序优化永远要优化慢的部分，换语言是无法“优化”的。 

## 

## 什么是DOM  Document Object Model

 就是将XML（或者HTML）内的节点定义成基本统一的对象数据可以供程序语言（如javaScript）控制的技术规范。

## 原生 JavaScript 的 DOM 操作




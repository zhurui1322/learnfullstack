# RESTful api

## RESTful api 

一种[万维网](https://zh.wikipedia.org/wiki/%E4%B8%87%E7%BB%B4%E7%BD%91)[软件架构](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E6%9E%B6%E6%9E%84)风格

匹配REST设计风格的Web API称为**RESTful API**。它从以下三个方面资源进行定义：

* 直观简短的资源地址：URI，比如：`http://example.com/resources/`。
* 传输的资源：Web服务接受与返回的[互联网媒体类型](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%94%E7%BD%91%E5%AA%92%E4%BD%93%E7%B1%BB%E5%9E%8B)，比如：[JSON](https://zh.wikipedia.org/wiki/JSON)，[XML](https://zh.wikipedia.org/wiki/XML)，[YAML](https://zh.wikipedia.org/wiki/YAML)等。
* 对资源的操作：Web服务在该资源上所支持的一系列[请求方法](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE#%E8%AF%B7%E6%B1%82%E6%96%B9%E6%B3%95)（比如：POST，GET，PUT或DELETE）。

GET： 获取资源

PUT: 替换资源（也可用于创建）

POST: 创建资源

DELETE： 删除资源

{% hint style="info" %}
URI的定义全部是名词，不要使用动词
{% endhint %}

### REST的优点

* 可更高效利用缓存来提高响应速度
* 通讯本身的无状态性可以让不同的服务器的处理一系列请求中的不同请求，提高服务器的扩展性
* 浏览器即可作为客户端，简化软件需求
* 相对于其他叠加在[HTTP协议](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE)之上的机制，REST的软件依赖性更小
* 不需要额外的资源发现机制
* 在软件技术演进中的长期的兼容性更好

## URI VS URL

统一资源标志符URI: 就是在某一规则下能把一个资源独一无二地标识出来。拿人做例子，所以身份证号才是URI，通过身份证号能让我们能且仅能确定一个人。

那统一资源定位符URL: 动物住址协议://地球/中国/浙江省/杭州市/西湖区/某大学/14号宿舍楼/525号寝/张三.人可以看到，这个字符串同样标识出了唯一的一个人，起到了URI的作用，所以URL是URI的子集。

URL是以描述人的位置来唯一确定一个人的。在上文我们用身份证号也可以唯一确定一个人。对于这个在杭州的张三，我们也可以用：身份证号：123456789来标识他。所以不论是用定位的方式还是用编号的方式，我们都可以唯一确定一个人，都是URl的一种实现，而URL就是用定位的方式实现的URI。

假设所有的Html文档都有唯一的编号，记作html:xxxxx，xxxxx是一串数字，即Html文档的身份证号码，这个能唯一标识一个Html文档，那么这个号码就是一个URI。

而URL则通过描述是哪个主机上哪个路径上的文件来唯一确定一个资源，也就是定位的方式来实现的URI。


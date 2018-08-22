# Javascript十大常用设计模式

[https://juejin.im/entry/58c280b1da2f600d8725b887](https://juejin.im/entry/58c280b1da2f600d8725b887)

## 工厂模式

 工厂模式类似于现实生活中的工厂可以产生大量相似的商品，去做同样的事情，实现同样的效果;这时候需要使用工厂模式

利用构造函数，使用new 来构造无数个实例

**复杂的工厂模式定义是：**将其成员对象的实列化推迟到子类中，子类可以重写父类接口方法以便创建的时候指定自己的对象类型。

## 单体模式

 单体模式提供了一种将代码组织为一个逻辑单元的手段，这个逻辑单元中的代码可以通过单一变量进行访问。

1. 可以用来划分命名空间，减少全局变量的数量。
2. 使用单体模式可以使代码组织的更为一致，使代码容易阅读和维护。
3. 可以被实例化，且实例化一次。

```javascript
// 单体模式
var Singleton = function(name){
    this.name = name;
    this.instance = null;
};
Singleton.prototype.getName = function(){
    return this.name;
}
// 获取实例对象
function getInstance(name) {
    if(!this.instance) {
        this.instance = new Singleton(name);
    }
    return this.instance;
}
// 测试单体模式的实例
var a = getInstance("aa");
var b = getInstance("bb");
```

比如点击弹窗就可以使用单例模式，这样不会一直创造新的div元素。

```javascript
// 实现单体模式弹窗
var createWindow = (function(){
    var div;
    return function(){
        if(!div) {
            div = document.createElement("div");
            div.innerHTML = "我是弹窗内容";
            div.style.display = 'none';
            document.body.appendChild(div);
        }
        return div;
    }
})();
document.getElementById("Id").onclick = function(){
    // 点击后先创建一个div元素
    var win = createWindow();
    win.style.display = "block";
}

```

## 模块模式

 模块模式的思路是为单体模式添加私有变量和私有方法能够减少全局变量的使用

```javascript
var singleMode = (function(){
    // 创建私有变量
    var privateNum = 112;
    // 创建私有函数
    function privateFunc(){
        // 实现自己的业务逻辑代码
    }
    // 返回一个对象包含公有方法和属性
    return {
        publicMethod1: publicMethod1,
        publicMethod2: publicMethod1
    };
})();
```

   模块模式使用了一个返回对象的匿名函数。在这个匿名函数内部，先定义了私有变量和函数，供内部函数使用，然后将一个对象字面量作为函数的值返回，返回的对象字面量中只包含可以公开的属性和方法。这样的话，可以提供外部使用该方法；由于该返回对象中的公有方法是在匿名函数内部定义的，因此它可以访问内部的私有变量和函数。



##  代理模式

 代理是一个对象，它可以用来控制对本体对象的访问，它与本体对象实现了同样的接口，代理对象会把所有的调用方法传递给本体对象的

```javascript
// 先申明一个奶茶妹对象
var TeaAndMilkGirl = function(name) {
    this.name = name;
};
// 这是京东ceo先生
var Ceo = function(girl) {
    this.girl = girl;
    // 送结婚礼物 给奶茶妹
    this.sendMarriageRing = function(ring) {
        console.log("Hi " + this.girl.name + ", ceo送你一个礼物：" + ring);
    }
};
// 京东ceo的经纪人是代理，来代替送
var ProxyObj = function(girl){
    this.girl = girl;
    // 经纪人代理送礼物给奶茶妹
    this.sendGift = function(gift) {
        // 代理模式负责本体对象实例化
        (new Ceo(this.girl)).sendMarriageRing(gift);
    }
};
// 初始化
var proxy = new ProxyObj(new TeaAndMilkGirl("奶茶妹"));
proxy.sendGift("结婚戒"); // Hi 奶茶妹, ceo送你一个礼物：结婚戒
```

 代码如上的基本结构，TeaAndMilkGirl 是一个被送的对象\(这里是奶茶妹\)；Ceo 是送礼物的对象，他保存了奶茶妹这个属性，及有一个自己的特权方法sendMarriageRing 就是送礼物给奶茶妹这么一个方法；然后呢他是想通过他的经纪人去把这件事完成，于是需要创建一个经济人的代理模式，名字叫ProxyObj ；他的主要做的事情是，把ceo交给他的礼物送给ceo的情人，因此该对象同样需要保存ceo情人的对象作为自己的属性，同时也需要一个特权方法sendGift ，该方法是送礼物，因此在该方法内可以实例化本体对象，这里的本体对象是ceo送花这件事情，因此需要实例化该本体对象后及调用本体对象的方法\(sendMarriageRing\).

 对于我们提到的优点，第二点的话，我们下面可以来理解下虚拟代理，虚拟代理用于控制对那种创建开销很大的本体访问，它会把本体的实例化推迟到有方法被调用的时候；比如说现在有一个对象的实例化很慢的话，不能在网页加载的时候立即完成，我们可以为其创建一个虚拟代理，让他把该对象的实例推迟到需要的时候。

##  订阅模式 

 支持简单的广播通信，当对象状态发生改变时，会自动通知已经订阅过的对象。发布者与订阅者耦合性降低，发布者只管发布一条消息出去，它不关心这条消息如何被订阅者使用，同时，订阅者只监听发布者的事件名，只要发布者的事件名不变，它不管发布者如何改变；

## 职责链模式

##  命令模式

##  **宏命令**

##  模板方法模式

##  策略模式

##  中介者模式




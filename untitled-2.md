# Javascript

## **介绍js有哪些内置对象和基本类型（primitive types）**

这些值是在底层上直接实现的，他们不是object，所以没有原型，没有构造函数

* number
* string
* boolean
* undefined
* null

{% hint style="info" %}
typeOf varaible 来检查类型
{% endhint %}

原始值可以用数据封装变成类， Object 是 JavaScript 中所有对象的父对象

这样就会带有object的继承函数  


![&#x56FE;&#x7247;&#x63CF;&#x8FF0;](https://lh3.googleusercontent.com/M0qlQRPUSm9LD124u4hkX3w9gd91nh-cm4ZPbcaXi6lhzjj0HlZ3kt1Fg_vT5qlXpAUrSzPHRH5ndS5YBsmaksdeh35WdCfipaiVgOVFsXLRWLAZcTfgSOM0Ea2vbwBcJIOG2oLk)

数据封装类对象：Object、Array、Boolean、Number 和 String。 其他对象：Function、Arguments、Math、Date、RegExp、Error  


## **关于typeOf 函数** 

```javascript
var a = 3;
console.log(typeof a);   number

var b = "Hello";
console.log(typeof b);   string

var c = {};
console.log(typeof c);   object

var d = [];
console.log(typeof d); // weird!   object 
console.log(Object.prototype.toString.call(d)); // better! [object array]

function Person(name) {
    this.name = name;
}

var e = new Person('Jane');
console.log(typeof e);   object
console.log(e instanceof Person);    in e in the prototype chain we can find Person

console.log(typeof undefined); // makes sense undefined
console.log(typeof null); // a bug since, like, forever...  object

var z = function() { };
console.log(typeof z); // object 
```

## **JavaScript有几种类型的值？画一下他们的内存图吗？**

栈：原始数据类型（Undefined，Null，Boolean，Number、String）

堆：引用数据类型（对象、数组和函数） 两种类型的区别是：存储位置不同；

原始数据类型直接存储在栈\(stack\)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；

引用数据类型存储在堆\(heap\)中的对象,占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体  


![](https://lh3.googleusercontent.com/-K_Ox_7omsT8p2dExuuLnCfpoU9fYMlhmQCsyDaDnzrZ8WywDq2QP3CUTK25ySc8SqE51pQ8TR7ISnwVGaFoOUyshDkb1k7ckF3sjWSrK4LeiDHJM8NREid8uzTMrnqNXudPOVRT)

## Javascript 作用域的相关问题

当Javanese程序编译时，会先生成Global Object \(windows in browser\)   
This 也就是指向Global Object   
outer environment 

程序会先给变量和函数预解析**“hoisting",** 预解析就是把所有的声明提升到顶部。

varable 储存再stack中， 但是只是define 并没有赋值 （预解析）  
function 储存再heap中，全部的code都会存储

![execution context stack ](https://lh6.googleusercontent.com/PvAgNoS5DG6OHr7bL1LwBEuwwsjiuMk3S7w-U8uIGSnlJAS2gzvVNWVpRhqXcdEcfZ8Nw78vUeNOzX8yOzOW2zU0EhNhNFCdnhxGRJnBLX1GlSiRynwFmvVS8XI2rWsuceSiBigj)

## **Javascript作用链域?**

全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。

当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，直至全局函数，这种组织形式就是作用域链。

## **null，undefined 的区别？**

null 表示一个对象是“没有值”的值，也就是值为“空”

undefined 表示一个变量声明了没有初始化\(赋值\)；

undefined不是一个有效的JSON，而null是； 

undefined的类型\(typeof\)是undefined；是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined； 

null的类型\(typeof\)是object；是一个对象\(空对象, 没有任何属性和方法\)

{% hint style="info" %}
  **在验证null时，一定要使用　=== ，因为 == 无法分别 null 和 undefined**

**null == undefined // true**

**null === undefined // false**  
{% endhint %}



```text

```

## **eval是做什么的？**

它的功能是把对应的字符串解析成JS代码并运行； 应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。 由JSON字符串转换为JSON对象的时候可以用eval，var obj =eval\('\('+ str +'\)'\);

## **let 和 var的区别**

1. var 会实现预加载 所以会显示undefined, 而let不会预加载 所以会显示not initialize
2. var 可以重复定义, let 不可以
3. let可以形成块级作用域, 而以前var 想要实现块级作用域需要使用IIFE 形成函数作用域

## const 用法

const一般定义常量 但是可以定义object const a = {} 依然可以改变对象的数据结构和属性

## **Javascript如何实现封装？**

```javascript
function Cat(name,color){
　　　　this.name = name;
　　　　this.color = color;
}
Cat.prototype.type = "猫科动物";
Cat.prototype.eat = function(){alert("吃老鼠")};

var cat1 = new Cat("大毛","黄色");
var cat2 = new Cat("二毛","黑色");
alert(cat1.type); // 猫科动物
cat1.eat(); // 吃老鼠
```

这个方法用来判断，某个proptotype对象和某个实例之间的关系。 `Cat.prototype.isPrototypeOf(cat1)`

每个实例对象都有一个hasOwnProperty\(\)方法，用来判断某一个属性到底是本地属性，还是继承自prototype对象的属性。 

`cat1.hasOwnProperty("name")`

in运算符可以用来判断，某个实例是否含有某个属性，不管是不是本地属性。 “name in cat1 

`for (var v in cat)` 会打出prototype中的属性

## **JavaScript原型，原型链 ? 有什么特点？**

每个对象都会在其内部初始化一个属性，就是prototype\(原型\)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。  


所有的javascript object 都会继承原型的属性和方法

使用object constructor 去建立object

然后使用new Person\(\)

但是不能直接添加新的属性到一个已经存在的constructor

所以我们要使用prototype去添加新的属性和方法

`Person.prototype.nationality = "English";`

or

`Person.prototype.name = function() return this.firstName + " " +this.lastName;};`

![](https://lh4.googleusercontent.com/NtaISmIYIbf4zLreiUCMkvXvaAR9wjug9NAjJ7JYx5tDiBVPTjNeWh20rgmShaw4CtzDAdVU9lZNQ4TDuAvi-dVarYEgETrf__icKu4sp5RqhaciXdCiyBggTfHPwiZiJ9uKMhnE)

## proto VS  prototype

_proto_ 隐式原型

* 每一个函数在创建之后都会拥有一个名为prototype的属性，这个属性指向函数的原型对象。
* 显式原型的作用：用来实现基于原型的继承与属性的共享。

_prototype_ 显式原型

* avaScript中任意对象都有一个内置属性\[\[prototype\]\]，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过\_\_proto\_\_来访问
* 隐式原型的作用：构成原型链，同样用于实现基于原型的继承。举个例子，当我们访问obj这个对象中的x属性时，如果在obj中找不到，那么就会沿着\_\_proto\_\_依次查找

 \_\_proto\_\_是**每个对象**都有的一个属性，而prototype是**函数**才会有的属性。

 \_\_proto\_\_指向的是**当前对象**的**原型对象**，而prototype指向的，是以**当前函数**作为**构造函数**构造出来的**对象**的**原型对象**

## Javacript继承的几种实现方式？

### **1.构造函数绑定**

使用call或apply方法，将父对象的构造函数绑定在子对象上，即在子对象构造函数中加一行：

```javascript
function Cat(name,color){
    Animal.apply(this, arguments);
    this.name = name;
    this.color = color;
}
var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物
```

### **2.prototype模式**

  
代码的第一行，我们将Cat的prototype对象指向一个Animal的实例。 它相当于完全删除了prototype 对象原先的值，然后赋予一个新值。 因此，在运行"Cat.prototype = new Animal\(\);"这一行之后，cat1.constructor也指向Animal！ 这显然会导致继承链的紊乱（cat1明明是用构造函数Cat生成的），因此我们必须手动纠正，将Cat.prototype对象的constructor值改为Cat。这就是第二行的意思。

```javascript
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物
```

### **3.直接继承prototype**

用Cat.prototype = Animal.prototype; 替换 Cat.prototype = new Animal\(\); 效率高 不需要建立animal 的实例

### **4.利用空对象作为中介**

```javascript
function extend2(Child, Parent) {
    var p = Parent.prototype;
    var c = Child.prototype;
    for (var i in p) {
        c[i] = p[i];
    }
    c.uber = p;
}
```

## **非构造函数的继承**

### **1.object 函数**

```javascript
function object(o) {
　　　function F() {}
　　　F.prototype = o;
　　　return new F();
}
//就是把子对象的prototype属性，指向父对象

//再加上子对象本身的属性
var Doctor = object(Chinese);

Doctor.career = '医生';
```

## 浅拷贝

浅拷贝有问题就是子对象获得是地址 当父对象被篡改的时候 会影响子对象

ES6 自带内置函数

`Object.assign(target, ... sources)`

```javascript
function extendCopy(p) {
　　　　var c = {};
　　　　for (var i in p) { 
　　　　　　c[i] = p[i];
　　　　}
　　　　return c;
}
```

## 深拷贝

```javascript
obj1 = { a: 0 , b: { c: 0}};
let obj3 = JSON.parse(JSON.stringify(obj1));
obj1.a = 4;
obj1.b.c = 4;
console.log(JSON.stringify(obj3)); // { a: 0, b: { c: 0}}
```

```javascript
function deepCopy(p, c = {}) {
    for (var i in p) {
        if (typeof p[i] === 'object') {
            c[i] = (p[i].constructor === Array) ? [] : {};
            deepCopy(p[i], c[i]);
　　　　　} else {
　　　　　　　c[i] = p[i];
　　　　　}
　　　}
　　　return c;
}
深拷贝利用迭代可以深层拷贝

```

##  **javascript创建对象的几种方式？**

```javascript
javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。


 1、对象字面量的方式

     person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};

 2、用function来模拟无参的构造函数

     function Person(){}
     var person=new Person();//定义一个function，如果使用new"实例化",该function可以看作是一个Class
     person.name="Mark";
     person.age="25";
     person.work=function(){
     alert(person.name+" hello...");
     }
     person.work();

 3、用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）

     function Pet(name,age,hobby){
        this.name=name;//this作用域：当前对象
        this.age=age;
        this.hobby=hobby;
        this.eat=function(){
           alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
        }
     }
     var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
     maidou.eat();//调用eat方法


 4、用工厂方式来创建（内置对象）

      var wcDog =new Object();
      wcDog.name="旺财";
      wcDog.age=3;
      wcDog.work=function(){
        alert("我是"+wcDog.name+",汪汪汪......");
      }
      wcDog.work();


 5、用原型方式来创建

     function Dog(){

      }
      Dog.prototype.name="旺财";
      Dog.prototype.eat=function(){
      alert(this.name+"是个吃货");
      }
      var wangcai =new Dog();
      wangcai.eat();


 5、用混合方式来创建

     function Car(name,price){
       this.name=name;
       this.price=price;
     }
      Car.prototype.sell=function(){
        alert("我是"+this.name+"，我现在卖"+this.price+"万元");
       }
     var camry =new Car("凯美瑞",27);
     camry.sell();

```

## 普通函数和构造函数的区别

普通函数：不使用new运算符的函数就是普通函数，最简单的函数

构造函数：如用函数用来初始化\(使用**new**运算符\)一个新建的对象，我们称之为构造函数\(constructor\)

```javascript
function Prince(name,age){
    this.gender="male";
    this.kind=true;
    this.rich=true;
    this.name=name;
    this.age=age;
}
Prince.prototype.toFrog=function(){
    console.log("Prince "+this.name+" turned into a frog.");
}
var prince=new Prince("charming",25);
prince.toFrog();//Prince charming turned into a frog.
prince.kind;//true
```

```javascript
//当以new调用构造函数(执行var p = new Person())时，函数内部会发生以下情况:
//1.创建一个空对象
var prince = {}
//2.this变量指向对象p
Prince .call(prince)
//3.p继承了构造函数Person()的原型
prince.__proto__ = Prince.prototype
```

构造函数里一般是没有return的，但是如果return的是五种简单类型，忽视return，但是如果是object, 则不再返回this 对象，而是返回return的值。

## **谈谈This对象的理解**

this总是指向函数的直接调用者（而非间接调用者）； 如果有new关键字，this指向new出来的那个对象； 在事件中，this指向触发这个事件的对象

```javascript
var f = function () {
  console.log(this.x);
}

var x = 1;
var obj = {
  f: f,   f 实际上是保存的地址
  x: 2,
};

// 单独执行
f() // 1  f()直接只想地址，执行环境是全局变量

// obj 环境执行
obj.f() // 2  通过obj找到的f 所以说执行环境是obj

var foo = obj.f()

foo() // 1 这是后foo() 实在环境变量中 所以是1  foo是直接指向函数地址的

```

## **判断一个对象是否属于某个类**

```javascript
使用instanceof （待完善）
if(a instanceof Person){
    alert('yes');
}
```

## **什么是闭包（closure），为什么要用它**

 **内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后**。  闭包通常用来创建内部变量，使得这些变量不能被外部随意修改，同时又可以通过指定的函数接口来操作。

1. 函数内再嵌套函数 
2. 内部函数可以引用外层的参数和变量
3. 参数和变量不会被垃圾回收机制回收

```javascript
function f1(){
    var n=999;
    nAdd=function(){
        n+=1
    }
    function f2(){
　　     alert(n);
　　 }
　　 return f2;
}
var result=f1();
result(); // 999
nAdd();
result(); // 1000
```

为什么会这样呢？原因就在于f1是f2的父函数，而f2被赋给了一个全局变量，这导致f2始终在内存中，而f2的存在依赖于f1，因此f1也始终在内存中，不会在调用结束后，被垃圾回收机制（garbage collection）回收。

这段代码中另一个值得注意的地方，就是"nAdd=function\(\){n+=1}"这一行，首先在nAdd前面没有使用var关键字，因此nAdd是一个全局变量，而不是局部变量。其次，nAdd的值是一个匿名函数（anonymous function），而这个匿名函数本身也是一个闭包，所以nAdd相当于是一个setter，可以在函数外部对函数内部的局部变量进行操作。

## **Call\(\) Apply\(\) Bind\(\)**

 The **`bind()`** method creates a new function that, when called, has its `this` keyword set to the provided value, 

 The **`call()`** method calls a function with a given `this` value and arguments provided individually.

 The **`apply()`** method calls a function with a given `this` value, and `arguments` provided as an array

```javascript
var person = {
    firstname: 'John',
    lastname: 'Doe',
    getFullName: function() {
        var fullname = this.firstname + ' ' + this.lastname;
        return fullname;
    }
}

var logName = function(lang1, lang2) {
    console.log('Logged: ' + this.getFullName());
    console.log('Arguments: ' + lang1 + ' ' + lang2);
    console.log('-----------');
}

var logPersonName = logName.bind(person);
logPersonName('en');
logName.call(person, 'en', 'es');
logName.apply(person, ['en', 'es']);
```

## **Funtion currying**

create a copy of function but with some present parameter  


```javascript
function multiply(a, b, c) {
    return a*b*c;   
}

var multipleByTwo = multiply.bind(this, 2);
console.log(multipleByTwo(4,2));

var multipleByThree = multiply.bind(this, 3);
console.log(multipleByThree(4));
```

## **Javascript垃圾回收**

 垃圾回收器会**按照固定的时间间隔周期性**的执行。

 全局变量的生命周期直至浏览器卸载页面才会结束

局部变量只在函数执行的过程中存在。而在这个过程中，会为局部变量在栈（或堆）内存上分配相应的空间，以便存储它们的值。然后在函数中使用这些变量，直至函数执行结束、释放它们的内存以供将来使用。

### 标记清楚

js中最常用的垃圾回收方式就是标记清除。当变量进入环境时，例如，在函数中声明一个变量，就将这个变量标记为“进入环境”。从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到它们。而当变量离开环境时，则将其标记为“离开环境”。

GC运行时，会给所有的变量标记，然后去除环境变量已经被环境中变量引用的标记如闭包。之后会销毁带标记的变量。

## **Json 转换**

```javascript
JSON字符串转换为JSON对象:
var obj =eval('('+ str +')');
var obj = str.parseJSON();
var obj = JSON.parse(str);

JSON对象转换为JSON字符串：
var last=obj.toJSONString();
var last=JSON.stringify(obj);
```

## **\["1", "2", "3"\].map\(parseInt\) 答案是多少？**

function callbackfn\(value, index, array1\) 这是map的函数callback

三个函数是

```javascript
parseInt("1",0) //0或者不设置都是按10来算
parseInt("2",1) //1 不在 2~36之间
parseInt("3",2) //3在二进制里面invalid
所以结果是 [1,NaN,NaN]
```

## **JavaScript 代码中的"use strict";是什么意思 ?** 

‘use strict’

可以在任何的地方使用 形成scope 

person = a 在不是strict模式下可以编译 但是再strict模式会说undefined 

不能删除prototype的property 

// Assignment to a non-writable global 

// Assignment to a new property on a non-extensible object 

// Assignment to a getter-only property

## 数组的操作

* push\(\): Adds one or more elements to the end of an array and returns the new length of the array.
* pop\(\): Removes the last element from an array and returns that element.
* shift\(\): Removes the first element from an array and returns that element.
* reverse\(\): Reverses the order of the elements of an array — the first becomes the last, and the last becomes the first.
* sort\(\): Sorts the elements of an array in place and returns the array.
* splice\(\): Adds and/or removes elements from an array.
* unshift\(\): Adds one or more elements to the front of an array and returns the new **length** of the array.

删除首尾的方式是使用:`pop`和`shift`。但是如果我们要删除特殊的指定元素，先要获取到指定元素的下标，然后使用`splice`进行替换。

```javascript
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 1); -> Jan April June
months.splice(1, 0, 'Feb') -> Jan Feb March April June
```

ES5中新加的方法

forEach : 不会遍历没有定义的元素  
map  
filter  
some  
every  
indexOf  
lastIndexOf  
reduce  
reduceRight: 从右边开始遍历

## setTimeout的误区 {#settimeout%E7%9A%84%E8%AF%AF%E5%8C%BA}

而是setInterval 和 setTimeout 函数运转的最短周期是 5ms 左右

如果需要更加短的周期，可以使用:

1. requestAnimationFrame 它允许 JavaScript 以 60+帧/s 的速度处理动画，他的运行时间间隔比 setTimeout 是要短很多的。 
2. process.nextTick 这个是 NodeJS 中的一个函数，利用他可以几乎达到上面看到的 while 循环的效率 
3. ajax 或者 插入节点 的 readState 变化 
4. MutationObserver 
5. setImmediate

 由于Javascript是单线程的，所以会存在被阻塞的情况

 try...catch捕捉不到它的错误:

## 生成随机数

```text
function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min)) + min;
}
```

## 事件冒泡与事件捕获

### 事件冒泡

 微软提出了名为`事件冒泡(event bubbling)`的事件流。事件冒泡可以形象地比喻为把一颗石头投入水中，泡泡会一直从水底冒出水面。也就是说，事件会从最内层的元素开始发生，一直向上传播，直到document对象。

### 事件捕获

 网景提出另一种事件流名为`事件捕获(event capturing)`。与事件冒泡相反，事件会从最外层开始发生，直到最具体的元素。

![](https://pic2.zhimg.com/80/v2-bf3b8dbab027713a2b21b9e8a5b7a6c4_hd.jpg)

### addEventListener的第三个参数

```text
element.addEventListener(event, function, useCapture)
```

第一个参数是需要绑定的事件  
第二个参数是触发事件后要执行的函数  
第三个参数默认值是false，表示在**事件冒泡阶段**调用事件处理函数;如果参数为true，则表示在**事件捕获阶段**调用处理函数。

 对于事件代理来说，在事件捕获或者事件冒泡阶段处理并没有明显的优劣之分，但是由于事件冒泡的事件流模型被所有主流的浏览器兼容，从兼容性角度来说还是建议大家使用事件冒泡模型。

 **绑定在被点击元素的事件是按照代码顺序发生**，其他元素通过冒泡或者捕获“感知”的事件，按照W3C的标准，先发生捕获事件，后发生冒泡事件。**所有事件的顺序是：其他元素捕获阶段事件 -&gt; 本元素代码顺序事件 -&gt; 其他元素冒泡阶段事件 。**

{% hint style="info" %}
 stopPropagation函数可以停止冒泡机制
{% endhint %}

## 事件委托

一般来讲，会把一个或者一组元素的事件委托到它的父层或者更外层元素上，真正绑定事件的是外层元素，当事件响应到需要绑定的元素上时，会通过事件冒泡机制从而触发它的外层元素的绑定事件上，然后在外层元素上去执行函数。这是利用了事件冒泡的机制

 **委托的优点**

 减少内存消耗  

```markup
<ul id="list">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
  ......
  <li>item n</li>
</ul>
<** ...... 代表中间还有未知数个 li **>
<** 这个点击事件绑定到他的父层，也就是 `ul` 上 w**>
<** 然后在执行事件的时候再去匹配判断目标元素 **>
```

####  动态绑定事件

因为事件是绑定在父层的，和目标元素的增减是没有关系的，执行到目标元素是在真正响应执行事件函数的过程中去匹配的；

```javascript
// 给父层元素绑定事件
document.getElementById('list').addEventListener('click', function (e) {
  // 兼容性处理
  var event = e || window.event;
  var target = event.target || event.srcElement;
  if (target.matches('li.class-1')) {
    console.log('the content is: ', target.innerHTML);
  }
});
```

 **比如 focus、blur 之类的事件本身没有事件冒泡机制，所以无法委托；**

\*\*\*\*

## JavaScript内存分析


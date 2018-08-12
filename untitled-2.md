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
****

## Javacript继承的几种实现方式？




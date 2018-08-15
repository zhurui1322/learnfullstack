# ECMAScript 6

##  **Arrows function**

var odds = evens.map\(v =&gt; v + 1\);

## **Classes**

```javascript
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
}
```

This code snippet is taken from the classes sample \(live demo\). Here super\(\) is called to avoid duplicating the constructor parts' that are common between Rectangle and Square.

## **Template Strings**

```javascript
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
// Construct an HTTP request prefix is used to interpret the replacements and construction
POST`http://foo.org/bar?a=${a}&b=${b}

```

## **Destructuring**

```javascript
var {op, lhs, rhs} = getASTNode()
```

## **Default + Rest + Spread**

```javascript
function f(x, y=12) {
  // y is 12 if not passed (or passed as undefined)
  return x + y;
}
f(3) == 15


function f(x, ...y) {
  // y is an Array
  return x * y.length;
}
f(3, "hello", true) == 6
function f(x, y, z) {
  return x + y + z;
}
// Pass each elem of array as argument
f(...[1,2,3]) == 6
```

## **Map + Set + WeakMap + WeakSet**

```javascript
var s = new Set();
s.add("hello").add("goodbye").add("hello");
s.size === 2;
s.has("hello") === true;

// Maps
var m = new Map();
m.set("hello", 42);
m.set(s, 34);
m.get(s) == 34;

// Weak Maps
var wm = new WeakMap();
wm.set(s, { extra: 42 });
wm.size === undefined

// Weak Sets
var ws = new WeakSet();
ws.add({ data: 42 });

```

weak set and weak map只能使用object作为key， 并且可以被垃圾回收回收。

## Symbol

 ES6引入了一种新的原始数据类型Symbol，表示独一无二的值，它是JavaScript的第七种数据类型。 基本上，它是一种类似于字符串的数据类型。

```javascript
let s = Symbol();
console.log(typeof s);  // symbol

var s1 = Symbol('foo');
var s2 = Symbol('bar');
console.log(s1);    // Symbol(foo)
console.log(s2);    // Symbol(bar)
console.log(s1.toString()); // Symbol(foo)

```

 另外，我们需要重点记住的一点是：每个Symbol实例都是唯一的。因此，当你比较两个Symbol实例的时候，将总会返回`false`：

**应用场景1：使用Symbol来作为对象属性名\(key\)**

 Symbol类型的key是不能通过`Object.keys()`或者`for...in`来枚举的，它未被包含在对象自身的属性名集合\(property names\)之中。所以，利用该特性，我们可以把一些不需要对外操作和访问的属性使用Symbol来定义。

 我们可以利用这一特点来更好的设计我们的数据对象，让“对内操作”和“对外选择性输出”变得更加优雅。

```text
可以使用 来获取symbol
Object.getOwnPropertySymbols(obj) // [Symbol(name)]
```

**应用场景2：使用Symbol来替代常量**

不需要为所有的常量想名字

**应用场景3：使用Symbol定义类的私有属性/方法**

 我们知道在JavaScript中，是没有如Java等面向对象语言的访问控制关键字`private`的，类上所有定义的属性或方法都是可公开访问的。因此这对我们进行API的设计时造成了一些困扰。

## 用Set 去重

```javascript
[...new Set([1,2,3,1,'a',1,'a'])]
```






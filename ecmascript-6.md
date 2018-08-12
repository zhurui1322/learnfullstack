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

## 用Set 去重

```javascript
[...new Set([1,2,3,1,'a',1,'a'])]
```




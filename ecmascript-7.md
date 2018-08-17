# ECMAScript 7

## async / await



```javascript
async fetchDate(url) => {
    try {
        const response = await axios.get(`q?query= ${query}`);
        const data = response.date
        this.props.processFetchData(data)
    } catch(error) {
        console.log(error)
    }
}
```

使用async/await 实际上是异步的但是看起来是同步的，这样可以让阅读代码更方便。top bottom structure 



```javascript
|-------- dough --------> |-------- sauce --------> |-- cheese -->
async function makePizza(sauceType = 'red') {
  
  let dough  = await makeDough();
  let sauce  = await makeSauce(sauceType);
  let cheese = await grateCheese(sauce.determineCheese());
  
  dough.add(sauce);
  dough.add(cheese);
  
  return dough;
}
```

```javascript
|-------- dough -------->
|--- sauce --->           |-- cheese -->
async function makePizza(sauceType = 'red') {
  
  let [ dough, sauce ] =
    await Promise.all([ makeDough(), makeSauce(sauceType) ]);
  let cheese = await grateCheese(sauce.determineCheese());
  
  dough.add(sauce);
  dough.add(cheese);
  
  return dough;
}
```

```javascript
|--------- dough --------->
|---- sauce ----> |-- cheese -->

async function makePizza(sauceType = 'red') {
  
  let doughPromise = makeDough();
  let saucePromise = makeSauce(sauceType);
  
  let sauce  = await saucePromise;
  let cheese = await grateCheese(sauce.determineCheese());
  let dough  = await doughPromise;
  
  dough.add(sauce);
  dough.add(cheese);
  
  return dough;
}
```

## String.prototype.padStart/padEnd

```javascript
// No text
''.padStart(10, 'Hi') // 'HiHiHiHiHi'

// Some text
'def'.padStart(6, 'abc') // 'abcdef'

// Only use what gets to length
'5678'.padStart(7, '1234') // '1235678'

// padEnd(desiredLength, textToAppend)

'23'.padEnd(8, '0') // '23000000'
```

## Object.entries

```javascript
// Object literal
Object.entries({ 'a': 'A', 'b': 'B' }); // [["a","A"],["b","B"]]

// String
Object.entries('david') // [["0","d"],["1","a"],["2","v"],["3","i"],["4","d"]]
```

## Object.values

ES6 we have Object.keys, ES7 we will have Object.values

```javascript
Object.values({ 'a': 23, 'b': 19 }) // [23, 19]

// Array-like object (order not preserved)
Object.values({ 80: 'eighty', 0: 1, 1: 'yes' }) // [1, 'yes', 'eighty']

// String
Object.values('davidwalsh') // ["d", "a", "v", "i", "d", "w", "a", "l", "s", "h"]

// Array
Object.values([1, 2, 3]) // [1, 2, 3]
```

## Array.prototype.includes

Array.prototype.includes is a bit like **indexOf** but instead returns a true or false value instead of the item's index:

```javascript
['a', 'b', 'c'].includes('a') // true, not 0 like indexOf would give
['a', 'b', 'c'].includes('d') // false
```

## Exponentiation

```javascript
// 2 to the power of 8
Math.pow(2, 8) // 256

// ..becomes
2 ** 8 // 256
```




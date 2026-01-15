```javascript
const arr = [1, 2, 3, 4, 5];

const sliceResult = arr.slice(1, 4);
const spliceResult = [...arr];
spliceResult.splice(1, 3);

const mapResult = arr.map(x => x * 2);

const filterResult = arr.filter(x => x % 2 === 0);

const reduceResult = arr.reduce((sum, x) => sum + x, 0);

sliceResult;
spliceResult;
mapResult;
filterResult;
reduceResult;
```



```js
// slice: returns new array, does NOT modify original
const a = [1, 2, 3, 4, 5];
a.slice(1, 4);        // [2, 3, 4]
a;                    // [1, 2, 3, 4, 5]

// splice: modifies original array
const b = [1, 2, 3, 4, 5];
b.splice(1, 3);       // [2, 3, 4]
b;                    // [1, 5]

// map: transforms each element
const c = [1, 2, 3];
c.map(x => x * 2);    // [2, 4, 6]

// filter: keeps elements matching condition
const d = [1, 2, 3, 4];
d.filter(x => x % 2 === 0); // [2, 4]

// reduce: reduces array to single value
const e = [1, 2, 3, 4];
e.reduce((sum, x) => sum + x, 0); // 10
```



**`map` does NOT modify the original array.**
It **returns a new array**.

```js
const arr = [1, 2, 3];

const result = arr.map(x => x * 2);

arr;     // [1, 2, 3]
result;  // [2, 4, 6]
```



```js
// lastIndexOf: last occurrence index, -1 if not found
const a = [1, 2, 3, 2];
a.lastIndexOf(2); // 3

// shift: removes first element (mutates array)
const b = [10, 20, 30];
b.shift(); // 10
b;         // [20, 30]

// unshift: adds elements at start (mutates array)
const c = [20, 30];
c.unshift(10);
c;         // [10, 20, 30]

// some: true if ANY element matches condition
const d = [1, 2, 3, 4];
d.some(x => x > 3); // true

// every: true if ALL elements match condition
const e = [2, 4, 6];
e.every(x => x % 2 === 0); // true
```



```js
// remove duplicates from array
// using Set
const arr = [1, 2, 2, 3, 4, 4];
const unique1 = [...new Set(arr)]; // [1, 2, 3, 4]

// using filter + indexOf
const unique2 = arr.filter((v, i, a) => a.indexOf(v) === i);

// using reduce
const unique3 = arr.reduce((acc, v) => {
  if (!acc.includes(v)) acc.push(v);
  return acc;
}, []);
```



```js
// Sorting in java
// default sort (strings)
const a = ['b', 'a', 'c'];
a.sort(); // ['a', 'b', 'c']

// numbers ascending
const b = [10, 2, 5, 1];
b.sort((x, y) => x - y); // [1, 2, 5, 10]

// numbers descending
const c = [10, 2, 5, 1];
c.sort((x, y) => y - x); // [10, 5, 2, 1]

// strings with locale
const d = ['é', 'a', 'z'];
d.sort((x, y) => x.localeCompare(y));

// objects by key
const e = [{ age: 30 }, { age: 20 }, { age: 40 }];
e.sort((x, y) => x.age - y.age);
```

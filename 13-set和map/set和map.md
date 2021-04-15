## set

### 基本用法

es6提供了新的数据结构set,类似于数组,但是成员都是唯一的,没有重复的值

set本身是一个构造函数,用来生成set数据结构

```shell
const s = new Set();
[2,3,5,4,5,2,2].forEach(x => s.add(x));
for (let i of s){
  console.log(i);
}
// 2 3 5 4
```

### Array和Set对比

都是一个储存多值的容器,两者可以互相转换,使用场景上有区别

- Arrayde的indexof方法比Set的has方法效率低下
- Set不含重复值(可以利用这一特性进行数组的去重)
- Set通过delete方法删除某个值，而Array只能通过splice。两者的使用方便程度前者更优
- Array的很多新方法map、filter、some、every等是Set没有的（但是通过两者可以互相转换来使用）

### set实例的操作方法

```javascript
let set = new Set();
set.add(1)
set.add("1")
console.log(set.size)  //2
```

可以用数组来初始化一个set,set构造器确保不重复的使用这些值

```javascript
 let set = new Set([1,2,4,5,4,3,2,1])
 console.log(set.size)  // 5
```

**add(value):** 添加某个值，返回Set结构本身
**has(value):** 返回布尔值，表示该值是否为Set的成员

```javascript
let set = new Set()
set.add("1")
set.add(1)
console.log(set.has(1))
console.log(set.has("6"))
```

**delete(value):** 删除某个值，返回一个布尔值，表示是否成功
**clear(value):**清除所有成员，没有返回值

```javascript
let set = new Set()
set.add("1")
set.add(1)
console.log(set.has(1))  // true
set.delete(1)
console.log(set.size)   // 1
set.clear()
console.log(set.size)   // 0
```

### set遍历操作

**keys():**返回键名的遍历器
**values():** 返回健值的遍历器
**entries():**返回键值对的遍历器
**forEach():** 每个成员

由于`Set`结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致。

```javascript
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]

let set = new Set([1,2])
set.forEach(function(value,key){
    console.log(key + ":" + value)
})
// 1 ：1
// 2： 2
```

### 数组去重

```javascript
 let arr = [1,2,3,3,4]
 let set = new Set(arr)
 let newArr = Array.from(set)
 console.log(newArr)
// [1,2,3,4]
```

### weakset

weakset 结构与set类似,它与set有两个区别

- weakset的成员只能是对象,不能是其他类型的值
- weakset对象都是弱引用,如果其他对象不再引用该对象,那么垃圾回收机制自动回收该对象所占的内存,所以weakset是不可遍历的

WeakSet 结构有以下三个方法：
**WeakSet.prototype.add(value)**：向 WeakSet 实例添加一个新成员。
**WeakSet.prototype.delete(value)**：清除 WeakSet 实例的指定成员。
**WeakSet.prototype.has(value)**：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。
WeakSet的一个用处是储存DOM节点，而不用担心这些节点会从文档中移除时，会引发内存泄露。

## map

### 含义及基本用法

js 的对象,本质上是键值对的集合,但是传统上只能用字符串当做键.带来了很大的限制

es6提供了Map数据结构,类似于对象.也是键值对的集合,但是键的范围不局限于字符串,各种类型的值(包括对象)都可以当做键,是更完善的hash结构实现

```javascript
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

### map实例的操作方法

**size**属性

size属性返回 Map 结构的成员总数。

```javascript
const map = new Map();
map.set('foo', true);
map.set('bar', false);
map.size // 2
```

**set(key,value)**

set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该键。

```javascript
const m = new Map();
m.set('edition', 6)        // 键是字符串
m.set(262, 'standard')     // 键是数值
m.set(undefined, 'nah')    // 键是 undefined
```

set方法返回的是当前的Map对象，因此可以采用链式写法。

```javascript
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');
```

**get(key)**

```javascript
const m = new Map();
const hello = function() {console.log('hello');};
m.set(hello, 'Hello ES6!') // 键是函数
m.get(hello)  // Hello ES6!
```

**has(key)**

has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

```javascript
const m = new Map();
m.set('edition', 6);
m.set(262, 'standard');
m.set(undefined, 'nah');
m.has('edition')     // true
m.has('years')       // false
m.has(262)           // true
m.has(undefined)     // true
```

**delete(key)**

delete方法删除某个键，返回true。如果删除失败，返回false。

```javascript
const m = new Map();
m.set(undefined, 'nah');
m.has(undefined)     // true
m.delete(undefined)
m.has(undefined)       // false
```

**clear()**

```javascript
let map = new Map();
map.set('foo', true);
map.set('bar', false);
map.size // 2
map.clear()
map.size // 0
```

### map遍历方法

**keys()：**返回键名的遍历器。
**values()：**返回键值的遍历器。
**entries()：**返回所有成员的遍历器。
**forEach()：**遍历 Map 的所有成员。
需要特别注意的是，Map 的遍历顺序就是插入顺序。

```javascript
const map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);

for (let key of map.keys()) {
  console.log(key);
}
// "F"
// "T"

for (let value of map.values()) {
  console.log(value);
}
// "no"
// "yes"

for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
// "F" "no"
// "T" "yes"

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"

// 等同于使用map.entries()
for (let [key, value] of map) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"
```

### map与其他数据类型的转换

**Map 转为数组**

Map 转为数组最方便的方法，就是使用扩展运算符（...）。

```javascript
const myMap = new Map()
.set(true, 7)
.set({foo: 3}, ['abc'])

console.log(myMap)
console.log([...myMap])
```

**数组 转为 Map**

将数组传入 Map 构造函数，就可以转为 Map。

```javascript
new Map([
  [true, 7],
  [{foo: 3}, ['abc']]
])
```
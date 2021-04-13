## let

### 基本用法

let 和 var 很像,但只在该代码块有效。

```javascript
{
    let a = 10;
    var b = 1;
}
a // ReferenceError: a is not defined.
b // 1
```

for很适合let命令

### 不存在变量提升

```javascript
var会发生变量提升现象,即变量可以在声明前进行使用,值为undefined
// var的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

### 暂时性死区(简称TDZ)

暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。

声明即绑定

如果区域内存在const和let命令,这个区块对这些命令声明的变量,一开始就形成了封闭作用域,凡是在声明之前就使用这些变量,就会报错.

```javascript
var tmp = 123;

if(true){
    tmp = 'abc'; // ReferenceError
    let tmp
}
```

### 不允许重复声明

## const

### 基本用法

const声明一个只读的常量.一旦声明,常量的值就不能改变

const命令声明 的常量也是不提升,存在暂时性死区,只能在声明的位置后面使用

```javascript
const PI = 3.1415
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

### 声明变量的6中方法

 es5只有两种,var function

es6有6种,除了let,const 还有import,class


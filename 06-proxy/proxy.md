简化对象或数组属性变化

### 概念

proxy意思为代理,在访问对象之前建立一道拦截,任何访问该对象的操作之前都会通过这道拦截,即执行proxy里面定义的方法

### 基本用法

```javascript
let pro = new Proxy(target, handler)
--new Proxy()表示生成一个Proxy实例
--target参数表示要拦截的目标对象
--handler参数也是一个对象,用来制定拦截行为
```

### handler

Proxy支持13种拦截行为

**get(target,peopKey,receiver)**

用于拦截某个属性的读取操作,可接受三个参数

- target:目标对象
- propkey:属性名
- receiver (可选):proxy实例本身(严格来说,是操作行为所针对的对象)

**set(target,propKey,value,receiver)**

用于拦截某个属性的赋值操作,可以接受四个参数

- target:目标对象
- propKey:属性名
- value:属性值
- receiver(可选):Proxy实例本身

实例

创建hero对象为要拦截的对象

拦截操作对象handler为空,未对拦截对象设定拦截方法

```javascript
let hero = {
  name: "赵云",
  age: 25
}

let handler = {}

let heroProxy = new Proxy(hero, handler);

console.log(heroProxy.name);
// --> 赵云
heroProxy.name = "黄忠";
console.log(heroProxy.name);
// --> 黄忠
```

创建hero对象为所要拦截的对象;

handler对象为拦截对象后执行的操作，这里get方法为读取操作，即用户想要读取heroProxy中的属性时执行的拦截操作。

最后创建一个Proxy实例，当读取heroProxy中的属性时，结果打印出来的总是“黄忠”字符串。

```javascript
let hero = {
  name: "赵云",
  age: 25
}

let handler = {
  get: (hero, name, ) => {
    const heroName =`英雄名是${hero.name}`;
    return heroName;
  },
  set:(hero,name,value)=>{
    console.log(`${hero.name} change to ${value}`);
    hero[name] = value;
    return true;
  }
}

let heroProxy = new Proxy(hero, handler);
let obj = Object.create(heroProxy);

console.log(obj.name);
obj.name = '黄忠';
console.log(obj.name);

// --> 英雄名是赵云
// --> 赵云 change to 黄忠
// --> 英雄名是黄忠
```

Proxy也可以作为其他对象的原型对象使用。

```javascript
let hero = {
  name: "赵云",
  age: 25
}

let handler = {
  get: (hero, name, ) => {
    const heroName =`英雄名是${hero.name}`;
    return heroName;
  },
  set:(hero,name,value)=>{
    console.log(`${hero.name} change to ${value}`);
    hero[name] = value;
    return true;
  }
}

let heroProxy = new Proxy(hero, handler);
let obj = Object.create(heroProxy);

console.log(obj.name);
obj.name = '黄忠';
console.log(obj.name);

// --> 英雄名是赵云
// --> 赵云 change to 黄忠
// --> 英雄名是黄忠
```


## promise的含义

所谓promise,简单来说就是一个容器,保存着未来才会结束的事件的结果,从语法上来说,Promise是一个对象,从它可以获取异步操作的消息。

```shell
promise对象有两个特点:
  对象的状态不受外界影响,promise代表一个异步操作,有三种状态,pending(进行中),fulfilled(已成功)和rejected(已失败).只有异步操作的结果.可以决定当前是哪一种状态,任何操作都无法改变这个状态
  一单状态改变,就不会再变,任何时候都可以得到这个结果.promise对象的状态改变,只有两种可能,从pending变为fulfilled和从pending变为rejected,只要这两种情况发生,状态就凝固了,不会在变了,会一直保持这个结果,这是就称为resolved(已定型),如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
  缺点:
  	无法取消,一单新建就会立即执行,无法中途取消,如果不设置回调函数,promise内部抛出的错误不会反应到外部,当处于pending状态时,无法得知目前进行到了哪一个阶段
```

## resolve

promise接受一个函数,传入两个参数resolve,reject,分别表示异步操作执行成功和失败的回调函数,resolve是将promise的状态设置为fulfilled,reject是将promise设置为rejected

```javascript
var p = new Promise(function(resolve,reject){
    // 做一些异步操作
    setTimeout(function(){
         console.log("执行完成")
   		 resolve("随便数据")
    }, 2000)
})
```

上面的代码只是new一个对象,并没有调用就已经执行了,所以在用promise的时候一般是包在一个函数中,在需要的时候去运行这个函数

在包装好的函数最后,return出Promise对象.

```javascript
function runAsync(){
    var p = new Promise(function(resolve,reject){
         // 做一些异步操作
        setTimeout(function(){
             console.log("执行完成");
             resolve("随便什么数据");
        }, 2000);
    });
    return p;
}
runAsync()
```

在runAsync()的返回上直接调用then方法,

运行后,会在两秒后输出"执行完成",紧接着输出"随便什么数据"

```javascript
runAsync().then(function(data){
    console.log(data);
    //后面可以用传过来的数据做些其他操作
});
```

## reject

失败的回调,把Promise的状态设置为rejected

```javascript
function getNumber(){
    var p = new Promise(function(resolve, reject){
        //做一些异步操作
        setTimeout(function(){
            var num = Math.ceil(Math.random()*10); //生成1-10的随机数
            if(num<=5){
                resolve(num);
            }
            else{
                reject('数字太大了');
            }
        }, 2000);
    });
    return p;            
}

getNumber()
.then(
    function(data){
        console.log('resolved');
        console.log(data);
    }, 
    function(reason, data){
        console.log('rejected');
        console.log(reason);
    }
);
```

## catch

用来指定reject的回调

```javascript
getNumber()
.then(function(){
    console.log('resolved');
    console.log(data);
})
.catch(function(){
    console.log('rejected');
    console.log(reason);
})
```

## all

Promise的all方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后才执行回调。

用Promise.all来执行，all接收一个数组参数，里面的值最终都算返回Promise对象。这样，三个异步操作的并行执行的，等到它们都执行完后才会进到then里面。那么，三个异步操作返回的数据哪里去了呢？都在then里面呢，all会把所有异步操作的结果放进一个数组中传给then，就是上面的results

```javascript
Promise
.all([runAsync1(), runAsync2(), runAsync3()])
.then(function(results){
    console.log(results);
});

```






## async 作用

async函数返回的是一个的Promise对象

## await

await如果等到一个Promise对象,等待Promise对象resolve,然后得到resolve的值,作为await的运算结果

## async/await  用不用的比较

```javascript
//不使用(箭头函数版本)
function takeLongTime (){
    return new Promise(resolve => {
        setTimeout(() => resolve("long_time_value"), 1000);
    });
}
takeLongTime().then(v => {
    console.log("got", v)
})

function takeLongTime(){
    return new Promise(function(resolve){
        setTimeout(function(){
            resolve("long_time_value")
        },1000)
    })
}

takeLongTime().then(function(v){
    console.log("get", v)
})
//用
function takeLongTime (){
    return new Promise(resolve => {
        setTimeout(() => resolve("long_time_value"), 1000);
    });
}
async function test(){
    const v = await takeLongTime();
    console.log(v)
}
test()


```

## 优势在处理.then链

```shell
单一的promise链不能体现async的优势,处理多个promise组成的then链的时候,优势就体现出来了
```


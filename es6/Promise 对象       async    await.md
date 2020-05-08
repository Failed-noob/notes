### Promise 对象    /   async    await / generator 函数



在javascript 中   所有代码都是单线程的 何为单线程; 个人理解就是 只能按照顺序从上到下依次进行;



异步操作都是在任务线程上 [这句话可能不是很准确] 但异步操作都是在同步之后的;

**Promise** 对象用于表示一个异步操作的最终完成 (或失败), 及其结果值.

promise 由三种状态 :

只有 pending -> resolved  || pending->rejected  不可能处于pending状态

pending : 初始状态 等待中..... 

fulfilled:  完成  意味着 操作已经成功完成

rejected : 拒绝  意味着操作失败;



语法:

```markdown
new Promise( function(resolve, reject) {...} /* executor */  );
```

```javascript
//基本的用法
let pro = new Promise((resolved,rejected)=>{
            // resolved('success');
            rejected('failed')
        })
        pro.then(res=>{
            console.log(res)
        }).catch(rec=>{
            console.log(rec)
        })
```





由于异步消息 无法知道先后顺序; 比如 node的fs模块的读取文件 同时读取两个文件时 这两文件打印的的先后顺序 完全是看运气 并不是按照从上到下的顺序;由于他是异步操作;

![](D:\QQ截图\fs读取文件.PNG)



用Promise对象解决异步消息的先后顺序问题:

```javascript
let fs = require('fs')
let p1  =new Promise(function(resolve,reject){
  //resolve, reject 是两个回调函数 resolve是成功 reject 是失败
  fs.readFile('./test.txt',function(err,data){
    if(err){
      reject('test error')
    }else {
      resolve(data.toString())
    }
    
  })
})

let p2  =new Promise(function(resolve,reject){
  //resolve, reject 是两个回调函数 resolve是成功 reject 是失败
  fs.readFile('./testTwo.txt',function(err,data){
    if(err){
      reject('testTwo error')
  }else{
     resolve(data.toString())
  }
  })
})


//可以通过 Promise.prototype.all 方法来选择哪一个异步信息为第一个 或者调换p1 p2的位置
Promise.all([p1,p2]).then(datas=>{
  console.log(datas[1])
},errs=>{
  console.log(errs)
})
```



#### **再来说 async .... await**

```javascript
async function test(sum){
  return sum

}
console.log(test(2)) // 在function前面加上 async 然后他会返回一个Promise resolve的对象 
//ouput: Promise {2}
test(2).then(err=>{
  console.log(err)
})

async function test(sum){
  return sum
  // console.log(2)

}
// console.log(test(2)) // 在function前面加上 async 然后他会返回一个Promise resolve的对象
test(2).then(data=>{
  console.log(data)
})

function getSomething(){
  return 'something';
}
console.log(getSomething())
```

里面有两函数 async声明的函数在前面 后面的函数后调用 却先打印出结果 足以证明 有async声明的函数是异步的



据资料里所知: async 表示函数里有异步操作,await表示 紧跟在后面的 表达式需要等待结果 [这特么说的什么!!!] 

个人认为await 还是比较难理解的 下面的代码看能不能缓解一下:

```javascript
// async function test(){
//   return 'sum'
//   // console.log(2)

// }
// console.log(test(2)) // 在function前面加上 async 然后他会返回一个Promise resolve的对象
// test(2).then(data=>{
//   console.log(data)
// })

//按道理 resolve 里面的东西1s后实现 await好像省去了这延迟时间
async function setTime(){
  return new Promise(function(resolve,reject){
    setTimeout(resolve('1s后执行的内容'),1000)
  })
  
};

async function getTime(){
  let content = await setTime()
  console.log(content)
}
console.log('-------')
getTime()
console.log('-------')
// function getSomething(){
//   return 'something';
// }
// // console.log(getSomething())

// async function testone(){
//   let aa = await 33;
//   let a = await getSomething();
//   let b = await test();
//   console.log(b,a,aa)
//   console.log(a)
//   console.log(aa)
  
// }
// testone()
```




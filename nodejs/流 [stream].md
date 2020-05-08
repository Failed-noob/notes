### 流 [stream 这也是属于文件模块的 不是stream]

基本上互联网上传输的数据都是以流的方式来传输的, 

**可知流是一种传输手段,在一个应用中,流是一组有序的,有起点和终点的传输手段**



当传输的数据过大时 stream的作用就显示出来了 都分批次来读取 [写] 数据的

流的类型:

- `[Writable` - 可写入数据的流（例如 `fs.createWriteStream()`）。]()
- `Readable` - 可读取数据的流（例如 `fs.createReadStream()`）。
- `Duplex` - 可读又可写的流（例如 `net.Socket`）。
- `Transform` - 在读写过程中可以修改或转换数据的 `Duplex` 流（例如 `zlib.createDeflate()`）。

此外，该模块还包括实用函数 `stream.pipeline()`、`stream.finished()` 和 `stream.Readable.from()`。





读取流基本流程:

​	创建一个读取流 , 然后监听事件  监听事件进行相应的操作;

**读取流:**

![](D:\QQ截图\readStream.PNG)

**写入流:**

![](D:\QQ截图\writeStream.PNG)

```javascript
let fs =require('fs')

console.time()
fs.readFile('./haha.txt',function(err,data){
  if(err){
    throw err
  }else {
    console.log('--',data)
  }
})
console.timeEnd()
//可读流
console.time()
let readStream=fs.createReadStream('./haha.txt')

//用on关键字进行监听 data事件

readStream.on('data',function(res){
  console.log('-------------');
  console.log(res)
});
//监听err事件 当出现错误的时候 抛出错误
readStream.on('err',function(err){
  throw err
})
//当数据读完后 做出的处理
readStream.on('end',function(){
  console.log('读取完成')
})
console.timeEnd()

//可写流

let writeStream = fs.createWriteStream('./others.txt')
writeStream.write('只是我写的第一句\n')
writeStream.write('这是我写的第二局\n')
writeStream.write('this is third line\n')
writeStream.end() //这句话是必须要有的

//监听finish 当写入完成后做相关的操作
writeStream.on('finish',function(){
  console.log('写入完成')
})


let rs = fs.createReadStream('1.txt', {     // 返回了一个可读流的实例
    flags: 'r'        //对文件进行何种操作
        encoding: 'utf-8'        //设置之后，读取的是字符串，不然默认为buffer
        start:3                    //从索引3开始读
        end:7                    // 读到索引为7的  包括结束
        highWaterMark: 1
})       
```





管道 [pipe]  是实现流的一种机制 可以一边写入 一边读取 [当然pipe的功能不阔能这么狭窄]

```javascript
// 当要复制大文件的时候 此时用到pipe 就很方便了 先用可读流 写入流来实现
let fs = require('fs');


//创建一个可读流 可写流
let reads = fs.createReadStream('./haha.txt');
let writes = fs.createWriteStream('./copyhaha.txt')



//用pipe来实现复制文件
reads.pipe(writes);

```



链式流压缩文件

```javascript
let fs = require('fs');
let zlib  =require ('zlib') //这个模块可以进行压缩文件[当然不是唯一的功能]
//简易链式流 实现文件压缩
let readstr = fs.createReadStream('./haha.txt');
let writestr = fs.createWriteStream('./haha.txt.zip')
let gzip = zlib.createGzip()
readstr.pipe(gzip).pipe(writestr) //先将可读流进行压缩然后 写入可写流
readstr.pipe(gzip).on('end',function(){
  console.log('压缩完成')
})
```


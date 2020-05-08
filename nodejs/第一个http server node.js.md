### day1   node.js

**运行js    在控制台 输入 node xxx.js 或者不加js后缀也行**



node 是在服务器端运行的js代码 它是由 ECMAscript 语法 和 一些其他api组成的  他没有BOM 和 DOM ;



node创建的第一个应用;

![](D:\QQ截图\node组成.png)



```javascript


/*用http的creatServer()方法来创建服务器
 并用listen 绑定8880端口;
 通过request.response 来接收响应数据;
 */ 
var http = require("http");

http.createServer(function(request,response){
    response.writeHead(200,{'Content-Type':'text/plain'});

    response.end('hello world\n');
}).listen(8880);

console.log('Server running at http://127.0.0.1:8880/');
```





读写文件 

```JavaScript

var fs= require('fs');

/*同步读取文件 */
var data= fs.readFileSync('./test.txt');
console.log(data.toString())

/* 异步读取文件*/

fs.readFile('./test.txt',(err,data)=>{
    if(err){
        console.log(err)
    }
    console.log(data.toString());
})

```


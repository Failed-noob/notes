### http 模块

[ 所有浏览器发起的请求都是 GET 请求  form 表单可以post请求 还可以用ajax 模拟form表单 ]

http 模块 有client 和 server 

##### http.get(options[, callback])

`callback` 调用时只有一个参数，该参数是 [`http.IncomingMessage`](http://nodejs.cn/s/2RqpEw) 的实例。

##### http.get(url[, options][, callback])



{头条新闻接口}

http://v.juhe.cn/toutiao/index?type=top&key=6e44bea2798c16b94cabc9fef0fc0bca



```javascript
// 将数据爬取下来 然后用流 写入
let http = require('http');
let fs = require('fs')

//http.get() 用后台 模拟客户端获取数据
let url = 'http://nodejs.cn/api/http.html#http_http_get_options_callback'
http.get(url,function(res){
  // console.log(res) // 返回的是一个 IncomingMessage 的对象 而且是一个可读流
  // res.on('data',function(data){
  //   console.log(data.toString())
  // })
  res.pipe(fs.createWriteStream('./copyNodeHttpModule.html')).on('finish',function(){
    console.log('copy successfully!!')
  })
  
})
```

用http.get方法开做一个简易爬虫: [批量下载图片]



```javascript
//用 http 做一个简易爬虫 来批量下载图片
let http = require ('http');
let fs = require('fs');
let path =require ('path')

//先将整个网页 爬取下来
http.get('http://www.nipic.com/topic/show_27355_1.html',function(res){
  let data= '';
  let result ='';
  let arr = [];
 
  //绑定 当数据在读取的时候 将数据用变量保存下来
  res.on('data',function(chunk){
    data+= chunk.toString()
    // console.log(chunk.toString())
  }); 
  res.on('end',function(){
  let reg = /<img src="(.+?)" alt=".*?">/img
    //正则表达式的exec(str)方法有数据的话就返回一个含有指定正则的数组 包括正则里面括号里面玩意为数组的另一个元素 然后指针指向下一个附合要求的字符串   
   while(result = reg.exec(data)){
    //将每个照片存到空数组中
      arr.push(result[1])
    } 
    arr.forEach((item)=>{
      // console.log('old',item)
      item = item.replace('pic/','file/').replace('4.jpg','2.jpg') //将校照片换成大相片
      // console.log('new',item)
     getImg(item)
    })
  })
 
  function getImg(url){
    // console.log(url)
    let fn = path.basename(url)
    http.get(url,function(res){
      res.pipe(fs.createWriteStream(`./images/${fn}.jpg`))
    })
  }
})
```



http.createSrever((req,res)=>{

​ //上面的这种可以 下面的也可以解决跨域问题

//后端设置允许跨域
​      res.setHeader("Access-Control-Allow-Origin","*");
​      //设置响应的头信息
​      res.writeHead(200,{"Content-type" : "text/plain;charset=utf-8"});



 res.writeHead(200, {

​    'Content-Type': 'text/plain;charset=utf-8;',

​    "Access-Control-Allow-Origin":"*"

  });

})

**在后台 req.socket.remoteAddress 可以获取访问的服务器的 ip**



这里说说响应头 res.writeHead(状态码,{}) 后面的这个对象中 有 

'Content-Type':'text/html;charset:utf-8'  默认就为html 类型

'Content-Length': 24   [**一般不设置这属性 响应的字节是多少就是多少**] 如果你相应给内容小于这个规定的字节 浏览器就会处于一个挂起的状态 

'Access-Controll-Allow-Origin': '*'  设置服务器可跨域  [这里成为 cors 跨域]  这玩意也可以

​    res.setHeader("Access-Control-Allow-Origin","*"); 可以不写在 res.writeHead 的响应头对象中







### **http 状态码:**

![](D:\QQ截图\http状态码.PNG)

MIME 类型



Multipurpose Internet Mail Extensions 也称 MIME 类型 是一种标准,用老表示文档,文件,字节流的性质和格式  ; 

**!important** :

浏览器通常使用MIME类型 (而不是文件拓展名) 来确定如何处理 url 

**因此 web服务器在响应头中添加正确的MIME 类型非常重要**.

若没有配置 MIME类型 默认为 text/html ;若配置不正确 浏览器可能就会曲解文件内容 ,网站无法正常工作,并且下载地文件也会被错误处理;



一些常用的 MIME 类型 [这需要设置在服务器响应头的对象中]

| 文件拓展名 | MIME 类型          |
| ---------- | ------------------ |
| .txt       | text/plain         |
| .css       | text/css           |
| .js        | text/javascript    |
| .html      | text/html          |
| .jpg       | image/jpeg         |
| .png       | image/png          |
| .mp3       | audio/mpeg         |
| .pdf       | application/pdf    |
| .zip       | application/x-gzip |



ajax get请求 在地址栏上

post 请求 在请求体上 




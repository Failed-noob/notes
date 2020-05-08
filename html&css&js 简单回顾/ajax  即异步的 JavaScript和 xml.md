### ajax  即异步的 JavaScript和 xml



![](D:\QQ截图\ajax请求过程.png)

ajax是封装过后的异步请求; 先来看看原生的异步请求;

- 不刷新页面更新网页
- 在页面加载后从服务器请求数据
- 在页面加载后从服务器接收数据
- 在后台向服务器发送数据

![](D:\QQ截图\xml对象的方法.png)





下面的代码是创建XMLHtttprequest 对象 通过get方式获取 txt文件

ActiveXObject 是专门对 ie7 以下做的兼容处理; (我自己再电脑上处理 但是获取不到 总是 block by CORS  好像是由于跨域问题???????????) 网上对于 ajax 是否能够获取到本地文件这件事情 也很模糊; (假设无法访问 只能在同一个服务器上访问 那就先到这 )



```html
<html>
<head>
<script type="text/javascript">
function loadXMLDoc()
{
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
xmlhttp.open("GET","/ajax/demo_get.asp",true);
xmlhttp.send();
}
</script>
</head>
<body>

<h2>AJAX</h2>
<button type="button" onclick="loadXMLDoc()">请求数据</button>
<div id="myDiv"></div>

</body>
</html>

```



当响应的是给xml文件就用 **responseText** 

若响应的是xml文件就用 **responseXML**



再来看看 请求的方式 **GET　　＆　　 POST ;**

ＧＥＴ没什么注意的；　当请求方式为ＰＯＳＴ时，，，如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据



```html
<html>
<head>
<script type="text/javascript">
function loadXMLDoc()
{
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
xmlhttp.open("POST","/ajax/demo_post2.asp",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Bill&lname=Gates");
}
</script>
</head>
<body>

<h2>AJAX</h2>
<button type="button" onclick="loadXMLDoc()">请求数据</button>
<div id="myDiv"></div>
 
</body>
</html>

```



XMLHttprequest 对象的 onreadystatechange事件

![](D:\QQ截图\ajax 请求.png)





![](D:\QQ截图\ajax status.png)



![](D:\QQ截图\ajax status-2.png)
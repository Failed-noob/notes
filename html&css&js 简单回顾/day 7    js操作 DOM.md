

### day 7    js操作 DOM 

想要操作DOM  就要先获取的到该元素  一般有以下几种方法:

document.getElementById("DD")

document.getElementsByClassName("")/*这是通过类 来获取元素*/

document.getElmentsByName("")/*通过name属性来获取元素 应该只要 getElements 都会返回一个集合*/

document.getElementsByTagName("") /*通过 元素名称来获取到元素*/

![](D:\QQ截图\DOM.png)





下面是一个 为div添加子元素的例子:(这里的window.onload 是html代码执行后才 运行js代码 ;如果 将js代码放在 html代码前面 没有家window.onload的话 代码时不会按照开发者的意愿来)  讲道理 下面的window.onload   写的跟我以前学的不一样了 不行忘了 



对于window.onload 当要发送请求 或者加载数据时 就会用到 具体情况 看实际情况

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .lala {
            color: yellow;
        }
    </style>
     <script type="text/javascript">
        window.onload= function() {
            c()
        }
        function c() {
                var eg= document.getElementById('eg');
                console.log(eg);
                var plusP = document.createElement('p');/*为div添加一个p标签*/
                plusP.innerText= 'hahhaha';
                plusP.setAttribute('class','lala') /*为新添加的标签 增加一个属性*/
                eg.appendChild(plusP);

            }
    </script>
</head>
<body>
   
    <div id="eg">
        <p>ouch!!!</p>
        <button onclick="c()">annniu</button>
    </div>
</body>
</html>
```


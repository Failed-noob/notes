#### day 13 window 对象

window对象有太多的属性值了,一些常用的要记住;

window.self 返回当前窗口的引用

window.parent   返回当前窗体的父窗体对象

window.top 返回当前窗体最顶层的父窗体的引用

window.outerwidth       返回当前窗口的外部宽

window.outerheight  返回当前窗口的外部高

window.innerwidth       返回当前窗口的可显示区域宽

window.innerheight  返回当前窗口的可显示区域高



window对象 属性太多了 你可以在控制台中打印window对象 就可以看到他的所有属性和方法;

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        #container {
            width: 200px;
            height: 200px;
            background: linear-gradient(to top left,pink,purple)
        }
    </style>
     <script>
         window.onload=function(){
             console.log(window)
            var con = document.getElementById('container'); 
            console.log(con.offsetHeight+'----'+ con.offsetWidth)
            console.log(con.clientHeight+'------'+con.clientWidth)
            console.log(window.innerWidth+'------'+window.innerHeight)
            console.log(window.outerWidth+'------'+window.outerHeight)
            var a= prompt('输出一个大于五的数','5')
                console.log(a)
            }
            var firm= confirm('Press a button');
            if(firm==true){
                alert('yep!!!!')
            }else{
                alert('Game over')
            }
        
    </script>
</head>
<body>
   
    <div id="container"></div>
</body>
</html>
```


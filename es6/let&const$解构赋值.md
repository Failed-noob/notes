### 关于es6的新特性-1

关键字:

  **let  & const**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
       let a= 1;
       
        console.log(a);
        {
            var b=3;

        }
        console.log(b)

        console.log(c);
        const c=4;
    </script>
    <pre>
        let和const 都不能重复声明,否则报错; 
        const声明的是一个只读的常量  一旦声明，常量的值就不能改变。
        let & const 在区域内 只能再该区域内访问到这两个变量, 否则就会报错
        若用var声明的时候就能在的区域外访问到该元素;
        还有这两关键字 都不存在变量提升;所谓变量提升就是先使用 再声明;   就var关键字可以;
        综上: let 最好用在块作用域中 例如向for循环那样的大括号里;
    </pre>
</body>
</html>
```

![](D:\QQ截图\解构-2.png)



![](D:\QQ截图\结构赋值.png)
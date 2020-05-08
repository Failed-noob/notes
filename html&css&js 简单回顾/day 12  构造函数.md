#### day 12  构造函数



构造函数与普通函数的 声明方式是一样的,但一般函数名 首字母都大写;

而且调用的时候 都是通过new关键字来 创建一个对象 



下面是 构造函数的简单例子:

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
       function Person (name,age) {
            this.name= name;
            this.age= age;
            this.say= function() {
                alert( `我叫${this.name},今年${this.age}岁`)
            }
       };
       Person.prototype.haha= function(){console.log('我是添加到原型链上的第一个方法');};
       console.log(Person.__proto__)
       var per = new Person('Tom',20);
       console.log(per.say())
       console.log(per.haha)
    </script>
    <pre>
        构造函数 与普通函数的声明方式一样 但函数名首字母 一般都要大写
        调用时 一般都用 new 来构造一个新的函数 
    </pre>
</body>
</html>
```


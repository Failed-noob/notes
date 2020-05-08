### day 14 函数的 call() & apply() 方法;  



call() ,  apply() 都可以调用函数和 给函数传递参数;

注意这两方法是 函数的方法 不要瞎用;

call() apply()  都可以改变 函数中 this的指向  若继续在后面传参的话 call 只需要用逗号隔开即可 而apply的参数需要用 数组包起来;

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
        var obj= {
            name: 'hahaha'
        }
        function example(a,b) {
            console.log('call & apply'+'--------'+a+'--------'+b);
            console.log(this.name);
        };
        example(1,2)
        example.call(obj,1,2) /*这样不用自己调用函数 通过call 可以调用函数 也可以在后面传递实参*/
        // example.apply(example,[1,5]) /*而与call不同的是 apply传递参数需要将参数放在数组中*/
    </script>
</body>
</html>
```



Object.keys( arg )

参数为: **要返回枚举 自身属性 的对象**  ;

众所周知 对象是由 key value 这两键值对组成 

该方法返回给定对象的所有可枚举的字符串属性



Object.values(obj)

##### 参数为 要**返回自身属性值**的对象

返回值 一个包含对象自身所有可枚举的属性值的数组
#### day 9   string对象 &正则表达式  



这是string的一些方法:


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
        var str= new String(); //创建一个string对象 
        var h= 'hello';
        var w= 'world';
        var hw= h.concat(w);
        
        console.log(hw); // 将两个字符串连接在一起
       
        var strs= 'hello world 是一般语*言入门的第一个程序';
        // console.log(typeof strs); //object
        console.log(strs.length);

        console.log(strs.charAt(5)); //charAt() 里参数时 字符串字母所在的位置

        console.log(strs.indexOf(' ')) // 5   从左到右检索 指定字符第一次出现的位置;

        console.log(strs.lastIndexOf(' ')) //5    从右到左 指定字符第一次的位置

        console.log(strs.slice(2,3)); //从左往右 前闭后开的区间 返回这样一个字符串;

        console.log(strs.split('')); //将字符串分割成一个数组; ['h','e','l','l','o',' ','w','o','r','l','d']
        console.log(strs.split(' '))  // 中间隔了一个空格 就说明字符串中 每隔一个空格 就是一个数组元素
        console.log(strs.split('*'))

        console.log(strs.substr(1,3)); // 目前来看 与slice的作用无二 substr(start,length) start 是起始的位置 length则是长度;

        console.log(strs.substring(1,3)); // 后面的3 可写 可不写 使用substring时要千万注意 不可随意瞎用;
        console.log(strs.substring(1));
        
        console.log(strs.valueOf()); // 返回最原始的值
    </script>
</body>
</html>
```





##### 正则表达式:

正则表达式是由一个字符序列形成的搜索模式。

当你在文本中搜索数据时，你可以用搜索模式来描述你要查询的内容。

正则表达式可以是一个简单的字符，或一个更复杂的模式。

正则表达式可用于所有文本搜索和文本替换的操作。

正则表达式一般用于表单验证中; 都是用 '**/ /**'  包含起来的;

在正则表达式中    **i                     m               g**   :

![](D:\QQ截图\正则表达式.png)



![](D:\QQ截图\正则.png)

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
            var a= /hello/i; /* i m g  */
            var str= 'world hello';
            console.log(str.search(a));  
            /* 通俗来讲,变量a就是标准 以a为标准 在字符串中检索 发现该标准的第一个字母的起始位置*/

            console.log(str.replace(/world/g,' ')) /*在字符串中检索到world 并将其用 空格替换*/
            console.log(str)
            console.log(str.replace('hello','hahhaha')) /*后面替换前面的*/

            var re= new RegExp('o');
            console.log(re.test('hello everyone!!!')) /*看字符串中是否含有正则表达式 有返回true 反之 false*/
            console.log(re.exec('hello everyone!!!'))

    </script>
    <pre>
        search() ,replace() 均是字符串的方法;
          replace()  也可直接 用于字符串替换字符串 两个字符串替换时
        是后面的替换前面的;

        对于正则表达式对象: RegExp 有test()    exec()这两方法 ;
        test() test() 方法用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。
        
        exec() 该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null。

    </pre>
</body>
</html>
```



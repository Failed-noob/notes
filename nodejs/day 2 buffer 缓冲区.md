### day 2 buffer 缓冲区  & 模块化



缓冲区 : 在内存中开辟的存储空间 用于存储数据;

buffer.from (str)  将str 转换为一个buffer类型 **以二进制存储,十六进制显示在控制台;**



再英文中一个字母占一个字节 而汉字是 一个汉字占三个字节; 下面是一些简单的Buffer的方法或属性;

```JavaScript
var str= '我是董晗';
var arr= [1,2,3,'hello','donghan','pp'];
var buf= Buffer.from(str)
console.log(arr)
console.log(Buffer.from(arr));
console.log(buf);
console.log(buf.length);//buffer的长度 也对等于占用内存的字节数;
console.log(str.length);
```







### 模块化



**这里顺便提上一句 arguments 是函数的特有属性** 

**arguments.callee()是arguments的重要属性。表示arguments所在函数的引用地址。**


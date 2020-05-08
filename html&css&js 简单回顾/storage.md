**storage**

​	H5之前通常都是用Cookie在本地进行存储;

Cookie的缺点很明显 存储量太小,具体的储量还会因浏览器的不同而有所差别,大致都在

数k左右;

每次http(s)请求时,Cookie都会跟随发送到服务器,浪费宽带;





localStorage的数据时永久存储的,除非人为删除;



sessionStorage 会话期间的数据,会话结束,数据也会删除;



还有一种 indexedDB 则更为强大;之后在了解;



localStorage 和 sessionStorage 都是对象  可以在控制台中打印出 他们的方法和属性;

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
        console.log(Storage.prototype)
        console.group('localStorge')
        console.log(localStorage);
        localStorage.setItem('s','sdf');
        localStorage.removeItem('s');
        // console.log(localStorage.getItem('s'))
        console.groupEnd();

        console.group('sessionStorage');
        console.log(sessionStorage);
        console.groupEnd()
    </script>
    <a href="test.html">test</a>
</body>
</html>
```







**localStorage 和 sessionStorage 的异同点:**



1. 两个都属于本地存储数据;

2. 存储量都比Cookie大 大约再5M左右;

3. 数据都不会跟随http(s)请求发送到服务端;

4. 两者都具有相同的属性和方法,都是从Storage对象哪里继承而来

5. .localStorage会在本地永久性存储，sessionStorage存储的数据仅在会话期间有效。sessionStorage的数据共享和sessionStorage会话周期（生命周期）与localStorage有很大不同。;





   **sessionStorage 存储数据的特点:**

   同域的任何页面都可以访问到localStorage存储的数据。

   但sessionStorage 与localStorage有着较大的不同，简述如下：

   （1）.sessionStorage 受到同源策略限制。

   （2）.sessionStorage 存储数据还受到浏览器选项卡的限制。

   （3）.手动新开一个选项卡，即便同域同URL，也不会共享sessionStorage 数据。

   （4）.当前选项卡关闭，sessionStorage 中存储的数据也随之被销毁。




 


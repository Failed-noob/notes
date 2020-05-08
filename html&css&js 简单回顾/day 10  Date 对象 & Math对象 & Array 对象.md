#### day 10  Date 对象 & Math对象 & Array 对象





Date 对象常用的几个方法 如下:


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
            function a(){
                 var time= document.getElementsByClassName('time')[0];
                var date= new Date();
                var hour= date.getHours(); //获取当前 多少 时
                var minutes= date.getMinutes(); // 获取当前多少 分
                var seconds= date.getSeconds(); //获取当前多少秒
                var time= document.getElementsByClassName('time')[0];
                time.value=  `北京时间${hour}点${minutes}分${seconds}秒`;    
                // console.log(`北京时间${hour}点${minutes}分${seconds}秒`)
             }
            
             function start(){
                    setInterval(a,1000)
             }
    </script>
    <input type="text" class="time">
    <button onclick= 'start()'>annniu</button>
</body>
</html>
```



Math对象: 这个感觉没什么好说的,就是一些特殊的值

**Math.floor(Math.random()*(n-m+1)+m); // 可以输出 任意值到任意值的随机数**

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
       
        function conpare (a,b){
            console.log(Math.max(a,b)+'更大一些')
            console.log(Math.floor(3.7))
            console.log(Math.round(3.5))
            console.log(Math.ceil(3.7))
           
        }
        conpare(4,6);
        function Quzhi(m,n){
            var zhi= Math.floor(Math.random()*(n-m+1)+m);
            document.write(zhi)
        }
        Quzhi(2,3)
    </script>
    <pre>
        Math对象 较常用的
         floor()(向 下取整) round()(四舍五入) ceil()(向 上取整) random() (产生 0-1 之间的随机数)
    </pre>
</body>
</html>



//对于一个数字 如何将 它分别拆分 
				
				console.log(parseInt(sum / 10000 % 10))  万
				console.log(parseInt(sum / 1000 % 10))  千
				console.log(parseInt(sum / 100 %10)) 百位
				console.log(parseInt(sum / 10 % 10)) 十位
				console.log(parseInt(sum % 10)) 个位
				
```



**Array对象:**

通过length 属性 可以 返回数组的长度;

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
        var arr= [1,3,5];
        var arr1= ['hello'];
        console.log(arr.length); //数组长度
        console.log(arr[0].toString()) 

        console.log(arr.concat(arr1)); //concat() 将两个数组连接起来组成一个新的数组;

        console.log(arr.join(',')); //join()将数组的元素 按照新的分割方式分割开来 返回的是一个string;

        console.log(arr.pop()); //删除数组的最后一个元素 并返回 此时数组已经发生变化;
        console.log(arr)

        console.log(arr.reverse());// 将数组的顺序颠倒;

        console.log(arr.shift()); //删除数组的首个元素并返回;
        console.log(arr);

        console.log(arr.push('haha','hihi')); //在数组的末尾添加元素 并返回数组的长度;
        console.log(arr);

        console.log(arr.slice(0,2)); 
        // 从指定下标开始 放回一个新数组 但不会改变原来的数组  
        //有两个参数 前闭后开 前面的例子就返回 第一个和第二个元素
      
        console.log(arr.splice(1,0,'hello')) //splice(index,删除元素的个数,'新增的元素或删除的元素') 
        console.log(arr);
        console.log(arr.splice(1,1)); // 这里就删除了刚刚添加的那个元素
        console.log(arr)

        console.log(arr.unshift('aaa','weitao')); //向数组开头添加多个或一个 元素并返回 数组长度;
        console.log(arr)
    </script>
    <pre>
        array 对象
    </pre>
</body>
</html>
```


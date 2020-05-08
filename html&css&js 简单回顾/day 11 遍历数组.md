### day 11 遍历 对象和数组:

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
        var arr = ['hah','lalla','fruit','pair','peach']
        var obj = {
            name: 'hsj',
            age: 12,
            gender: 'male'
        }

        for(b in obj){
            console.log(b); //输出的是对象的key值 
            console.log(obj[b])
            console.log(`key: ${b} , value: ${obj[b]}`)
        }

        // console.log(obj)
        for(b in arr){
            console.log(arr[b]);
        }
       
        console.log(arr.__proto__)
        console.group("for循环")
        for (var i=0;i<arr.length;i++){
            console.log(arr[i])
        };
        console.groupEnd();
        arr.forEach(function(item){
            console.log(item)
        })

        for (a of arr){
            console.log(a)
        }
   </script>
</body>
</html>
```


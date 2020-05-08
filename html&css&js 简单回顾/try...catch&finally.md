控制台常见的一些错误提示:

六种错误：

- ReferenceError:找不到对象时
- TypeError:错误的使用了类型或对象的方法时
- RangeError:使用内置对象的方法时，参数超范围
- SyntaxError:语法写错了
- EvalError:错误的使用了Eval   
- URIError:URI错误

try catch

  try { //执行的代码，其中可能有异常。一旦发现异常，则立即跳到catch执行。否则不会执行catch里面的内容 } 

catch { //除非try里面执行代码发生了异常，否则这里的代码不会执行 } 

finally { //不管什么情况都会执行，包括try catch 里面用了return ,可以理解为只要执行了try或者catch，就一定会执行 finally }   

![](D:\QQ截图\try_catch.png)





实例代码:

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<input type="number" id="input">
		<script>
			// function a(value) {
			// 	if(value<0){
			// 		throw new Error(value+' 是小于零的')
			// 	}
			// }
			// a(-1)
			
			
			document.getElementById('input').addEventListener('blur',_=>{
				var value = document.getElementById('input').value
				value  =parseInt(value);
				try{
					if(value>5) throw `${value}大于5`;
					if(value==5) throw new Error('wraning!!!!');
					if(value <5) throw '这个数小于五';
				}catch(err){
					console.log(err)
				}finally{
					console.log('hhahahah')
				}
			})
		</script>
	</body>
</html>

```


day 4 



css  单位 

![](D:\QQ截图\css 单位.png)





渐变和过渡

渐变分为 线性渐变 和 径向渐变![](D:\QQ截图\渐变.png)

```css
#eg { 
background: linear-gradient (to right ,red ,yellow) //从左向右  从红色到黄色;
background: linear-gradient(to bottom right, red, yellow); // 从左上到右下 
```
}
上面是 线性渐变

径向渐变:
​	#grad {
  	background-image: radial-gradient(red 5%, yellow 15%, green 60%);//红色占5% 黄色占15% ;绿色占60%
​	}

​	![](D:\QQ截图\径向一.png)



```css
#grad1 {
height: 150px;
width: 200px;
background-color: red; /* 浏览器不支持的时候显示 */
background-image: radial-gradient(red, yellow, green); /* 标准的语法（必须放在最后） */
}

#grad2 {
height: 150px;
width: 200px;
background-color: red; /* 浏览器不支持的时候显示 */
background-image: radial-gradient(circle, red, yellow, green); /* 标准的语法（必须放在最后） */
}
```

![](D:\QQ截图\径向二.png)



```css
#grad1 {
  height: 150px;
  width: 150px;
  background-color: red; /* 浏览器不支持的时候显示 */
  background-image: radial-gradient(closest-side at 60% 55%, red, yellow, black); 
}

#grad2 {
  height: 150px;
  width: 150px;
  background-color: red; /* 浏览器不支持的时候显示 */
  background-image: radial-gradient(farthest-side at 60% 55%, red, yellow, black); 
}

#grad3 {
  height: 150px;
  width: 150px;
  background-color: red; /* 浏览器不支持的时候显示 */
  background-image: radial-gradient(closest-corner at 60% 55%, red, yellow, black);
}

#grad4 {
  height: 150px;
  width: 150px;
  background-color: red; /* 浏览器不支持的时候显示 */
  background-image: radial-gradient(farthest-corner at 60% 55%, red, yellow, black); 
}
```

![](D:\QQ截图\径向三.png)



过渡:

transfrom 属性; 属性值如下: 

![](D:\QQ截图\transform.png)

![](D:\QQ截图\t1.png)





动画实例 :  (动画的实现的方式 如下)

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
<style> 
#myDIV
{
	width:300px;
	height:200px;
	background:red;
	animation:mymove 5s infinite;
	/*Safari 和 Chrome:*/
	-webkit-animation:mymove 5s infinite;
}

@keyframes mymove
	{
	from {background-color:red;
		transfrom: translate(0,0)}
	to {background-color:blue;
		transform: translate(100px,100px)}
}

/*Safari 和 Chrome:*/
@-webkit-keyframes mymove
{
	from {background-color:red;}
	to {background-color:blue;}
}
</style>

</head>
<body>

<p>背景颜色逐渐地从红色变化到蓝色：<p>

<div id="myDIV"></div>

<p>在 CSS 中，background-position 属性是 <em>可动画化（animatable）</em> 的。</p>

<p>Internet Explorer 10、Firefox 和 Opera 支持 CSS 动画。</p>
<p>Safari 和 Chrome 通过带有前缀 -webkit-，支持 CSS 动画。</p>

</body>
</html>
```









animation 动画 属性 

语法: animation: name  duration timing-function delay iteration-count direction fill-mode play-state;



![animation](D:\QQ截图\animation.png)

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
<style> 
#myDIV
{
	width:300px;
	height:200px;
	background:red;
	animation:mymove 5s infinite;
	/*Safari 和 Chrome:*/
	-webkit-animation:mymove 5s infinite;
}

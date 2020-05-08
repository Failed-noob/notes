#### ==less== 安装 和 使用

Less （Leaner Style Sheets 的缩写） 是一门向后兼容的 CSS 扩展语言。

比较 sass而言 less 不需要在window环境下不需要安装ruby;



link @import 这两的引入方式不同

<link rel="stylesheet" href="./style.css">

<style>
	@import url('./style.css')
</style>

less 的安装: [当然这样安装需要node]

```markdown
cnpm i less -g
```



![](D:\QQ截图\less的基本使用.png)



我以为 有less 之后 直接将.less引进去使用 然而并不是 当你写完less文件后 在有.less 的目录下 运行cmd 输入以下指令:

```markdown
lessc test.less 自定义的css文件名称.css
```



**然后将 css文件通过 link 标签 或者 @import 来引入 css文件  这个玩意跟css 一样 结尾的时候也需要用 ; 隔开**



### variables [变量]

```less
// 声明变量 @自定义名称 若有多个元素用同一种颜色的时候,有时候想改变颜色的时候 直接改变变量的值即可;[当然不局限于颜色上 其他属性也可以] 
@setColor : red;
.example {
    color: @serColor
}


//ouput:
.example {
    color: red;
}
```



### mixins [混合]

```less
//此时 .test 就有和fa 一样的样式了 若test本来就有的样式 会被新的样式覆盖
.fa {
	width: 200px;
	height: 300px;
	border:solid palegreen 2px;
	border-radius: .5em;
	opacity: .6;
	margin-top: 10px;

}
.test {
	color: @setColor;
    width: 100px;
	.fa()
}
```



### 嵌套[Nesting] 

之前我以为这个嵌套 需要缩进才起作用 后来才知道这玩意只是为了美观

```less
//这里面 p 就是test 的子元素  通过 缩进 来设置子元素的样式 这与sass中的似乎是一样的
.test {
	// color: @setColor;
	width: 100px !important;
	.fa();
	p{
		color: greenyellow;
	}
}

// &  表示为.content 的父元素
.content {
	color: @setColor;
	&::before {
		content:'-';
		display:inline-block;
		margin-right: 10px;
	};
	&::after {
		content:'-';
		display:inline-block;
		margin-left: 10px;
	}
}
```



### @规则嵌套和冒泡



```css
/*之前媒体查询如下*/
@media screen and (min-width: ---px) {
    .fa {
        font-size: 24px;
    }
} 


//
.fa {
	width: calc(100vh-500px);
	height: 300px;
	border:solid palegreen 2px;
	border-radius: .5em;
	opacity: .6;
	margin-top: 10px;
	@media (min-width:300px) {
		background-color: darkturquoise; /*当 屏幕小于 300px是 .fa 颜色变为默认值*/
	}

}
```




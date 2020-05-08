day 3

对于浮动:

   float  有三个属性值 center left right .当设置该属性后 该元素 就会脱离正常的文档流  

在正常的父元素中 给子元素设置float属性 如果父元素没有设置高度 父元素就会坍塌 就是因为父元素都是子元素撑起来的（前提是父元素未设置高度）然而子元素设置float属性后就会脱离文档流 所以就会出现坍塌；



当出现坍塌时的解决办法：

在不是ie8及以下版本时,元素都可以开启一个隐藏的属性 BFC(block formatting context)

但是直接开启bfc功能是无法完美的解决坍塌问题的.先来看看 哪几种方式可以开启bfc:



***1、float的值不是none。***
**2、position的值不是static或者relative。**
***3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex***
***4、overflow的值不是visible***

再来看看解决坍塌的解决办法:

(注:  这里说说clear属性 是清除浮动对自身的影响 并不是清除其他元素的浮动 分别有 left right both none 四个属性值

其中both是指 消除左边还是右边 影响更严重的消除 并不是消除所有的 )

1. 给容器设置 固定的宽高 (不推荐 一般而言 子元素都是随着父元素而变化的)

2. 给父元素设置 overflow属性 设置hidden 或者 auto

3. 在子元素后加上 一个空的div然后 clear:both清除浮动

4. 给父元素用伪选择器 :after 如下:
    .father:after {
      content: '';
      display: block;
      clear: both;
    }






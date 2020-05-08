day 5  关于弹性布局& @font-face



# 

 先回忆一下 @font-face 是关于 自定义字体的 在css中  设置字体是font-family  代码如下:

```css

```





弹性布局:  flex



![](D:\QQ截图\direction.png)

下面几个是给父元素设置的 一定要注意: (怕你忘记 row 横向 column 纵向 wrap 换行)

![](D:\QQ截图\flex.png)

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

justify-content : 属性定义了项目在主轴上的对齐方式。

属性值: flex-start | flex-end | center | space-between | space-around;



效果如下图: 以下全都是 以横向为主轴 从左到右   space-between  每个元素之间的间距相等;

space-around: 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

![](D:\QQ截图\justify.png)



![](D:\QQ截图\flex2.png)



![](D:\QQ截图\flex2-1.png)



![](D:\QQ截图\flex3.png)



![](D:\QQ截图\flex3-1.png)

接下来就是 在父元素设置flex属性的前提下 对子元素的处理;

![](D:\QQ截图\felx4.png)



**order** 就是排序 默认为零  值越小 越靠前 可以为负数 

**flex-grow**  放大比例 默认为零

**flex-shrink** :  缩小比例 默认为一 如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。  当其他属性不变时 设置其中一个值 在一定范围内 值越大 就越小

![](D:\QQ截图\flex5.png)


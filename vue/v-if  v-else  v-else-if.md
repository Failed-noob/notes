### v-if  v-else  v-else-if   



这里再重复一遍 v-fi   v-show的区别 :



v-if  参数若为true  vue就会创建带有v-if 属性的元素出来 为false时  此时 页面中还没有该元素;

v-show  当这个参数为true时   就是为该元素 设置了一个css属性  display : block / inline (反正就是这两 )

为false时     就是display: none  ;



v-else   可以理解为  下面的else    v-else-if   就相当于else-if

```
if(i==2){
    console.log('ok');
    
}else{
    console.log('failed');
}
```


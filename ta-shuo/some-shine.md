设置某一个模块的hover-class

```
hover-class='toolHover'

.toolHover {
    opacity:0.6;
}
```

黑色变灰这种效果一般使用 `opacity` 就很好了。不用另外再设置一种颜色。

微信有很多的icon ,这个小组件的颜色并不是固定的，可以设置任意color.设置方式是

```
<icon type="{{item}}" size="40" color="#ff0000"/>
```

一个使用&&的高级用法：

```
if(a){
//执行的代码
}

那么就可以写成

a && 要执行的代码
```

说不好，就是简化到不能再简化的感觉，看了轩哥的简化然后发现原来还可以进一步简化。

现在的长按事件用的几乎都是longpress


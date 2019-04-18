swiper组件使用的相关东西

1、禁止swiper滑动：

```
<swiper-item catchtouchmove='catchTouchMove'>   <!--重点这里-->

// 截获竖向滑动
  catchTouchMove:function(res){
    return false
  }
```

在`swiper-item`上加上这个属性并且搭配上这个方法，那么滑动将不再起作用。并且可以使用变量控制是否渲染这个方法，渲染这个方法那么就不能滑动，不渲染那么就可以滑动。











参考

[微信小程序swiper禁止用户手动滑动](https://www.cnblogs.com/kiimi/p/9205086.html)


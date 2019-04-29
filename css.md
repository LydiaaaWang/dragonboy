巧用transition  transform就可以让样式效果看起来好许多

1、当hover-class的时候就给当前按钮加上这个样式

```
.anismall{
  transform: scale(0.97);
}
```

2、从一个属性变动到另一些属性，看起来比较平滑

```
.swiper-container .dots .dot {
  margin: 0 8rpx;
  width: 12rpx;
  height: 12rpx;
  background: rgba(0, 73, 237, 0.2);
  border-radius: 8rpx;
  transition: all 0.6s;
}

.swiper-container .dots .dot.active {
  width: 24rpx;
  background: rgba(0, 73, 237, 1);
}
```

正常状况下是上边的属性，当active的时候那就改变一下宽度和背景色，但是都是平滑的过渡过来的。




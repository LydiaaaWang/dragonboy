将进度条的样式修改一下：

并且看一下之前是怎么实现的上传，以及看一下微信的安卓的那个函数是否可以使用了，如果不能，那就继续这样子实现。



为了实现图片的拖拽，控制了一个`overflow:hidden;position:fixed`

这个链式写法呀，值得学习：

```
wx.createSelectorQuery().select('.albumView').boundingClientRect(rect => {
    this.albumOffset = rect.top
}).exec()
```




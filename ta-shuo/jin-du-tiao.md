将进度条的样式修改一下：

并且看一下之前是怎么实现的上传，以及看一下微信的安卓的那个函数是否可以使用了，如果不能，那就继续这样子实现。

为了实现图片的拖拽，控制了一个`overflow:hidden;position:fixed`

这个链式写法呀，值得学习：

```
wx.createSelectorQuery().select('.albumView').boundingClientRect(rect => {
    this.albumOffset = rect.top
}).exec()
```

了解一下这里的个人数据是怎么修改的：

一般的数据使用的是接口上传，图片使用的是阿里云的上传。

在使用阿里云上传的时候会先通过接口去获取一些token验证之类的值，然后再调用阿里云的上传。

图片上传的时候只会上传新的图片，以前的图片不会上传

用户如果删除图片，那么并不会删除以前的图片，只是展示的时候会展示部分图片而已。

上传图片到阿里云成功之后还得

关于个人数据修改这里的一些高级的写法：

```
 let [requestData, modifyRequest] = this.buildRequest()
```

这是变量的解构赋值里边的对象的解构赋值方法。

一个问题：`JSON.stringify`的作用是什么？把一个数组这样子做一个跟另外一个数组进行比较？


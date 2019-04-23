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

一个问题：`JSON.stringify`的作用是什么？把一个数组这样子做一个跟另外一个数组进行比较？对，这样子直接使用==就可以确定是否相等了。

写一个图片上传进度组件======

不使用progress组件是因为希望颜色是渐变的颜色

现在需要再一次写一个组件：可是我基本上都忘了怎么写了，😭。那就再看一遍文档吧：

1、组件名称可以不跟文件夹的名称相同。

2、

这个组件只需要两个数据，那就是百分比&是否可以使用百分比，以及两个方法，显示和隐藏组件的方法。

监听器如果可以用那么就更好了，但是现在的监听器需要的版本比较高。

`showLoading`不会主动消失除非调用`hideLoading`

现在的问题就是怎么把百分比的数据传到页面上。。。。。。想了一个通过page传递的方法。

而且这个进度条会在两个页面用到，所以应该把另外一个页面也引入这个组件。

我有点懵，怎么就不执行aliyun的上传方法了呢！！！

```
"usingComponents": {
    "up-progress": "../../components/up-progress/index"
        "up-progress": "../../components/up-progress/index",
  }
```

而且是没有组件的时候执行这个方法，有了组件就不执行方法====

一个比较可疑的配置：

```
"navigationStyle": "custom"
```

排除是我组件写的有问题：证明了不是我组件写的有问题，而是这个页面有问题

想着不用组件了，那让效果好一点用个`template`总行吧，结果是可以的，因为刚刚忘了把`usingComponents`去掉。

现在需要的就是看一下数据是怎么计算的，以及更新的那个函数行不行，如果ok就使用，不ok就继续用现在这个。

查了一下微信公众平台社区：https://developers.weixin.qq.com/community/develop/doc/000e06415e8080732868e776f56000?highLine=onProgressUpdate 有人提出了这个问题，然后官方给出的回答是：http://mrpeak.cn/blog/http-upload-progress/  确实[Http文件上传进度为什么不准  ](http://mrpeak.cn/blog/http-upload-progress/)

它的意思是不仅仅是微信这里不准，其他的也都不准，这是http机制的问题。

现在只剩下了一个问题，那就是数据怎么计算的+ complete那个页面样式。

得先实现了再说选择哪一种：

重要的不是样式，是那个流畅的效果。不是突然的变多，而是慢慢的滑动到那一部分。




关于获取地理位置：

如果用户点击拒绝，那么下次点击还会出现弹框吗？看时间间隔，短时间内不会发起，但是如果删掉了小程序那么再进来的时候就会需要授权了。\(具体时间，由微信官方维护\)

如果用户点击忽略，那么就只会执行complete

wx.getLocation 用户授权后才可以使用

用户授权不需要使用button,用到button的是opensetting.

如果没有授权过，那么就会出现弹框，如果授权过，那么就会不出现弹框然后默默的获取他的地理位置。

```js
wx.getLocation({
  success: res => {
    this.location = [res.longitude, res.latitude];
  },
  complete:res=>{//点允许、拒绝、忽略都会执行这个方法
    this.browseAfter()
  }
})
```

getLocation这个api有三个返回函数，suc/fail/complete 如果用户既没有拒绝也没有接受，那么就会执行第三个，然后就不会显示请求过这个权限。

如果用户点击允许或者拒绝，那么就会执行fail&complete或者suc&complete，不管如何都会执行这个方法的。


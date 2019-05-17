关于那些放到app.globalData里边的数据

因为平时完全看不到的吖，如果想看就得打印console出来了。

signupData  ???

abTest ==2  老用户

app.globalData.privilege.superEndtime = res.data.everydaySuperTL  //每日超喜欢的过期时间戳

```
说明：everydaySuperTL == 4102444800000代表超喜欢是永久的,否则就不是永久,
拿这个时间戳和目前时间对比，可以算出每日超喜欢还剩几天,如果算出来是负数代表没有每日超喜欢权限
```

app.globalData.userInfo.followPublic 是否关注公众号

app.globalData.superLike  是否有超喜欢的能力

app.globalData.privilege 管理用户特权



我对数据的理解：

总的来说，前端显示可以用到的数据就是========接口数据、storage数据、前端保存到暂时有效的app.globaldata的数据，

一共就这几种，然后根据数据的意思进行一些本页面数据的设置，从而显示出某些效果。


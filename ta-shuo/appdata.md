关于那些放到app.globalData里边的数据

因为平时完全看不到的吖，如果想看就得打印console出来了。

signupData  ???

abTest ==2  老用户

app.globalData.privilege.superEndtime = res.data.everydaySuperTL  //每日超喜欢的过期时间戳

```
说明：everydaySuperTL == 4102444800000代表超喜欢是永久的,否则就不是永久,
拿这个时间戳和目前时间对比，可以算出每日超喜欢还剩几天,如果算出来是负数代表没有每日超喜欢权限
```




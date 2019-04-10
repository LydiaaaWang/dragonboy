## slice方法的使用？他的优缺点？

```
app.globalData.chathistory[user.uid] = session.message.slice(0)
```

这个指的是将session.message所代表的那个数组再选取一下，0的话代表从0 开始选取，跟正常赋值没区别，为什么还要用？

解释：当start 为0 时， 等于说是 克隆一个新的数组，克隆后 两个数组进行各自的操作，都互不影响，

## app.globalData内的数据什么时候会清空：

老大总是说本次登陆期间有效

我的实验：代码重新ctrl + s就没有了

切后台，切前台依然会有。进入其他页面也依然会有。


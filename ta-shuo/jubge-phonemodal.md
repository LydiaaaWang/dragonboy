

判断手机型号的一个写法

```js
if (app.globalData.phoneModel.search('iPhone X') != -1 || app.globalData.phoneModel.search('iPhone11') != -1) {
    this.setData({
      phoneModel: 'iphonex'
    })
  }
```

此处使用到的serch方法是用来判断某个字符串是否包含在另外一个字符串中的


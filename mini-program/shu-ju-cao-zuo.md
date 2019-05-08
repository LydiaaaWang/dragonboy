在普通的页面也可以控制app.js页面的方法，添加方法啥的

```
if (app.globalData.accessToken && app.globalData.accessId ) {
      this.afterAccessToken()
    } else if (app.globalData.accessToken && app.globalData.wechatId) {
      this.afterWechatId()
    }
    app.accessTokenReadyCallback = () => {
      this.afterAccessToken()
    }
    app.wechatIdReadyCallback = () => {
      this.afterWechatId()
    }
```

第一个页面的执行速度和app.js的执行速度不能确定。

小程序在微信官方的报告中显示表现优秀，这也证明了我们的策略是对的。



显示在页面上的数据要不要写在data里，我觉得取决于要不要赋一个默认值。


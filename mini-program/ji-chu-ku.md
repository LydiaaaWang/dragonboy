对基础库的处理：

```
基础库的获得：
 wx.getSystemInfo({
    success: res => {
      var version = res.SDKVersion;
      console.log(version,"处理前")//2.4.0
      version = version.replace(/\./g, "")
      console.log(version, "处理后")//240
      if (parseInt(version) >= 230) {
        //版本>=2.3.0
      }
    }
  })
```

真正的用户在使用的时候获取到的是用户自身的基础库，然后基本上都&gt;我们设置的最低。如果不大于，那么微信那边会提醒。


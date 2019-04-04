1、

目前支持的选择器：

::after  比如view::after是在view组件后边插入内容

::before 比如view::before是在view组件前边插入内容

2、

sitemap配置  站点地图  配置一下允许微信建立索引的机制

3、

WXS的某些函数是比较好用的，可以用用试试，因为在ios设备上小程序内的WXS会比JavaScript代码快2~20倍。在安卓设备上二者运行效率无差异。

4、

页面的setData过于频繁会导致卡顿，但是组件的setData过去频繁就不会卡顿，这是一个事实，不晓得是啥道理。

5、

```
//新版本强制更新
  if (resp.data.forceUpdate) {//服务器返回来的数据控制
    const updateManager = wx.getUpdateManager()
    updateManager.onUpdateReady(function () {
      updateManager.applyUpdate()
    })
  }
```




一个关于地理位置的bug

安卓手机上如果我删掉过小程序，那么小程序曾经请求过的权限就不见了。\[X\]

点了opensetting这个button之后立刻跳转页面，跳转页面回来之后才会执行opensetting这个方法里边的数据。

首先：复现这个情景

当进入页面的时候不想授权的话不点接受也不点拒绝，只要点返回，就可以将授权的那个框遮起来。由此造成的

getLocation这个api有三个返回函数，suc/fail/complete 如果用户既没有拒绝也没有接受，那么就会执行第三个，然后就不会显示请求过这个权限。

如果用户点击允许或者拒绝，那么就会执行fail&complete或者suc&complete，不管如何都会执行这个方法的。

不要改成在首页重复弹起，可以改成在打开设置那里判断一下有没有地理位置的授权，如果没有，那么就先调用一下getLoacation.然后再打开setting那个页面。

目前找到的最有效的实现方式：

每次进入那个页面的时候使用getSetting判断一下有没有，如果没有，那么就再getLocation:

```
代码的改动就只有else那里。
wx.getSetting({
      success: (res) => {
        if (res.authSetting["scope.userLocation"] !== undefined) {
          this.setData({
            userLocation: res.authSetting["scope.userLocation"]
          })
        }else{
          wx.getLocation({
            success: (res) =>{
              // this.setData({
              //   userLocation: res.authSetting["scope.userLocation"]
              // })
            }
          })
        }

      }
    })
```

当用户点击授权并使用当前位置的时候：判断一下，getSetting判断有没有，然后再判断如果有，是不是false.

终于找到原因了，是因为观察api执行情况不仔细，如果点击返回，不只会执行fail,还会执行complete.

另外一个就是判断条件乱写。

```
res.authSetting["scope.userLocation"]==undefiened //代表他按的是返回
！== unde //代表对方点了同意或者拒绝
```

//如果对方没有点拒绝而是点了同意呢？

如果用户点了同意，那么就应该保存下来地理位置，并且显示使用当前位置，就不应该再显示授权之类的了。

## 如何给一个函数传默认参数？

定义的时候写上值，使用的时候不传就是默认的值。


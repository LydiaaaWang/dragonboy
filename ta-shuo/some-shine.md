设置某一个模块的hover-class

```
hover-class='toolHover'

.toolHover {
    opacity:0.6;
}
```

黑色变灰这种效果一般使用 `opacity` 就很好了。不用另外再设置一种颜色。

微信有很多的icon ,这个小组件的颜色并不是固定的，可以设置任意color.设置方式是

```
<icon type="{{item}}" size="40" color="#ff0000"/>
```

一个使用&&的高级用法：

```
if(a){
//执行的代码
}

那么就可以写成

a && 要执行的代码
```

说不好，就是简化到不能再简化的感觉，看了轩哥的简化然后发现原来还可以进一步简化。

现在的长按事件用的几乎都是longpress

将一个for循环的嵌套的改成了map，感觉自己棒棒哒，不知道轩哥会不会给我来个改变了，期待。

```
for (var i = 0; i < this.data.sticker.length; i++) {
    for (var j = 0; j < this.data.sticker[i].content.length; j++) {
      for (var z = 0; z < this.data.sticker[i].content[j].length;z++){
        console.log("没查到")
        if (e.detail.value == this.data.sticker[i].content[j][z].name) {
          console.log("查询到了")
          this.setData({
            emojiPrevPath: this.data.sticker[i].content[j][z].path,
            offsetLeft: 470,
            emojiTop: this._pxToRpx(res[0].top)-280,
            emojiTip:true
          })

          if (this.data.emojiPrevPath || this.data.emojiTip){
            setTimeout(() => {
              this.setData({
                c: false,
                emojiTip: false
              })
            }, 4000)
          }

          return;
        }
      }
    }
  }
```

修改后：

```
this.data.sticker.map((sticker,sidx)=>{
    sticker.content.map((content,cidx)=>{
      if (e.detail.value == content[cidx].name){
        //show
        this.setData({
          emojiPrevPath: content[cidx].path,
          offsetLeft: 470,
          emojiTop: this._pxToRpx(res[0].top) - 280,
          emojiTip: true
        })
        // hide after 4s
        if (this.data.emojiPrevPath || this.data.emojiTip) {
          setTimeout(() => {
            this.setData({
              c: false,
              emojiTip: false
            })
          }, 4000)
        }
        return;
      }


    })
  })
```

果然给我带来了更高级的改变：那就是直接使用一个对象去保存所有的那些值，当需要用到某一个的时候，直接取出来，而不用循环。

```
const emojiGenerator = require("emoji");
const emoji = emojiGenerator.getEmoji()
const sticker = emojiGenerator.getSticker()
const stickerTip = emojiGenerator.getStickerTip()

this.setData({
    emojiTipArr: stickerTip[e.detail.value],
    emojiTipTop: this._pxToRpx(res[0].top) - 240,
})
```

关于小程序的设置：

```1
"navigationBarTitleText": ""
```

设为空看起开效果就特别好。

关于获取可视区域的height这里，由于height是会改变的，所以在使用的时候现成获取，或者就是精准把握什么情况下高度会变。

一个写法的改进：

```
var start = []
 for (let i = 0; i < this.data.user.photo.length; i++) {
   start.push(i)
 }
```

改进后：

```
var start = this.data.user.photo.map((v, i) => i)
```

我的一个写法：

```
checkDelete: function(sid,para) {
   let arr = app.globalData[para].slice()
    let index = arr.findIndex((value) => {
      return value.session.sid == sid
    })
    arr.splice(index, 1)    
    app.globalData[para] = arr.slice()
  },
```

我不清楚什么时候使用slice.于是就这样写了。然后改成了看起来更好的写法：

```
checkDelete: function (sid, para) {
    let index = app.globalData[para].findIndex((item) => {
      return item.session.sid == sid
    })
    index >= 0 && app.globalData[para].splice(index, 1)
},
```

具体做的优化就是：完全不需要加一个中间变量。

如果没有符合条件的那么


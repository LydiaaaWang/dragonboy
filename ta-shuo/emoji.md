需要完成的功能：

自定义dots.中间的dot要大一点。

一共需要用到两个点：可以是图也可以是view写出来的点

或者说就用三个view块，然后通过控制类名来决定显示哪一个点，但是这样的缺点是没有动画的切换效果。

既然是模仿微信的输入效果，那么这个点也模仿微信的效果好了。

有三个固定的点在底下，当页面切换的时候有一个大一点的点在不停的移动，当切换完了之后就会完全覆盖掉另外一个小点。

当已有输入的文字的情况下，如果调出emoji面板，那么此时的发送是不能点击的

长按emoji表情需要出现一个预览的图：那么怎样做能实现？怎样做可以更好？

如果他可能出现在任意一个位置，那么最好是fixed定位了。

当手指触摸动作结束后取消，也就是touchend这个事件了吧。

然后呢就发现，最关键的是这个位置怎么处理呢？

然后就发现了现在他们的代码里边已经有了代码转换的这个地方：pxToRpx的方法

左右不能超出屏幕：offsetLeft-86&gt;0?offsetLeft-86:0

276是自身的宽度，所以不能大于 750-280=470

createSelectorQuery的用法就很关键了，果然很多地方都会用到这个：

最终发现关于长按后取消的这个方法：

安卓执行的是touchcncel  ios执行touchend，所以就都写上吧

现在是都起作用了，但是滑动变卡了！！！！然后把catch换成bind竟然不卡了！！！！！

bindtouchend是ios上起作用的。cancel是安卓上起作用的。

多张emoji的时候需要显示出来，需要能够左右滑动-----

如果在一个view上写wx:for那么那个view本身也会被渲染，循环的渲染。

不是第一次遇见scroll这个问题了，但是还是没记住，就一个css: `white-space:nowrap;`

#### 错误的学习：

有的时候因为自己的某个地方的设置不对，然后造成了一个结果，比如说直接给数组设置为\[ \],我以为不能这样设置，但是最后发现是if的那个条件没有进去，所以才出现了这种。

当用户点击表情的时候不要让表情左右滑动。那么需要禁止swiper的滑动，swiper的滑动可以禁止嘛?可以。

那么现在需要做的就是长按切换了位置之后相继显示不同表情的预览这个了。

得知道表情的样式是咋写的？

每一个表情有一个固定的宽高，108rpx.左右的距离也知道是34rpx.文字的高度也知道30rpx,文字与图片的上边距是6rpx,下边距是20rpx.

经过我十分复杂的左边距离和上边距离计算之后，实现了目的效果，但是被几下就改的特别精简了。我都不明白为啥。我的天哪！！！！修改的这么快，思路改的也这么快。

1、看懂轩哥修改的思路

2、将循环map那里改成一个对象，然后设一些关键字，然后这种直接判断一下该对象里边这个属性有没有就可以了。

通过x,y确定行和列，通过行和列确定index,



```
catchTouchMove(e){
    let nowY = this._pxToRpx(e.touches[0].clientY);
    let nowX = this._pxToRpx(e.touches[0].clientX);
    
    if (nowY > this.clientY && nowY < this.clientY + 328 && nowX > 25 && nowX < 725) {
      let row = nowY > this.clientY + 164 ? 1 : 0
      let col = Math.floor((nowX - 25) / 176)
      let index = row * 4 + col
      if (this.emojiArea != index) {
        this.emojiArea = index;
        let tempArr = this.data.sticker[this.data.stickerSet - 1].content[this.data.curPage]
        this.setData({
          emojiPrevPath: tempArr[index].path,
          emojiLeft: col * 156,//这样子的写法牺牲了绝对的居中
          emojiTop: this.clientY - (row ? 95 :260)
        })
      }
    }
  }
```

emoji这里的管理方式也很厉害：


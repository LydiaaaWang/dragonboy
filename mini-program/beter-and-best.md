# 一些better and best 收集

1、

```js
      if (group == 0) {
        this.setData({
          'slideheight[0]': slideheight,
        })
      } else if (group == 1) {
        this.setData({
          'slideheight[1]': slideheight,
        })
      }
```

and

```js
      this.setData({
        ['slideheight[' + group + ']']: slideheight,
      })
```

这算是什么写法？ES6吗？

解析：不是，因为小程序setData的时候不可以左边直接写两个字符串的拼接，形式应该是 `key:value` 的形式。所以可以加一个中括号。

2、凡是不需要在页面上显示的数据都可以不放到page.data里。可以直接放到page里。这样只要这个页面关掉，数据就重新置为初始值。

3、+=2

```js
            if (this.data.pageIndex == 0) {
              this.setData({
                'pagePivot[0]': this.data.pagePivot[0] + 2
              }, () => {
                resolve()
              })
            } else if (this.data.pageIndex == 1) {
              this.setData({
                'pagePivot[1]': this.data.pagePivot[1] + 2
              }, () => {
                resolve()
              })
            }
```

and

```
this.pagePivot[this.data.pageIndex] += 2
resolve()
```

解析：因为某些数据不需要放到页面上，所以就不需要用setData来重新设置值了。由于只是执行js代码从上往下，不像setData那样是异步的，所以不需要.then那样的。

4、

var that=this 可以获取到this指向，逻辑也能完成，但是不好












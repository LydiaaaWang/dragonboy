

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

解析：


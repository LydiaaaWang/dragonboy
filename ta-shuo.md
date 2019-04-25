# step 1 获取到页面

```js
var pages = getCurrentPages()
var prevPage = pages[pages.length - 2]
```

# step  2 设置前一个页面的数据

1. 比如前一个页面的数据是这样的：

```js
page({
    queCaching:null,//添加问题缓存
})
```

那么在本页面设置的时候可以使用

```js
prevPage.queCaching="设置值的尝试"
```

此时在前一个页面就可以看到这个值已经更改了。

1. 比如前一个页面的数据是这样的：

```js
page({
    data:{
        questions: [],
    }
})
```

那么在本页面设置的时候可以使用

```js
prevPage.setData({
    questions: ques,
})
```

# 其他应用

可以在本页面使用上一个页面的数据，比如使用`questions` like this:

```js
this.setData({
    param: prevPage.data.questions[options.id],
    vaLength: prevPage.data.questions[options.id].length
})
```

判断是从哪一个页面进来的：

```
if (prevPage.route == 'pages/question/question'){}
```

2019.4.25新增

### 使用前一个页面的函数、方法

```
curPage.upImgProgress(30)
```

关于`getCurrentPages()`的应用基本上就这些了。


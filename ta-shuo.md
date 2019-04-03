

# step 1 获取到页面

```js
var pages = getCurrentPages()
var prevPage = pages[pages.length - 2]
```



# step  2 设置前一个页面的数据

比如前一个页面的数据是这样的：

```
page({
queCaching:null,//添加问题缓存
})
```

那么在本页面设置的时候可以使用


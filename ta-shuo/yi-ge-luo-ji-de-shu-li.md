是因为页面之前的写法获取不到传出来的值，所以改成了promise的写法，我以为我不会改，没想到我可以

```js
audioToText(url) {
    return new Promise((resolve,reject)=>{
      this.instance.audioToText({
        url: url,
        done: (err, msg) => {
          if (err) {
            //错误处理
            reject(err)
          }
          if (msg) {
            resolve(msg)
            console.log(msg.text)
          }
        }
      });
    })

  },
```

微信转出来文字是空的，会提醒转换文字失败，但是我们这里不会转换失败，只会显示为空，所以这个需要处理。

又一次遇到这个问题

```
Only number 0-9 could inside []: session.message[index].trans
```

虽然以前就解决了，但是我完全想不起来当初是怎么解决的，然后找到了以前英语学院的源码

```js
//显示隐藏内容
  showHideHtml:function(e){
    // console.log(e.currentTarget.dataset.chapterindex, "外面索引");
    // console.log(e.currentTarget.dataset.stepmodelindex, "模块索引")
    // console.log(e.currentTarget.dataset.isshowhtml, "是否展开");
    var chapterIndex = e.currentTarget.dataset.chapterindex;
    var stepModelIndex = e.currentTarget.dataset.stepmodelindex;
    var isShowHtml = e.currentTarget.dataset.isshowhtml;
    this.data.courseDetailInfo.chapterStepInfoList[chapterIndex].stepModelInfoList[stepModelIndex].isShowHtml = !isShowHtml;
    this.setData({
      [`courseDetailInfo.chapterStepInfoList[${chapterIndex}].stepModelInfoList[${stepModelIndex}].isShowHtml`]: !isShowHtml
    })
  },
```

那么这算是一种什么写法？好像是ES6的新写法，链接在这里：一开始没找到是因为页面搜索不怎么管用，如果已经在那个页面了再搜索，就起作用，如果切换过去搜索，那就不管用。

这是通过 [ES6 的 模板字符串](http://es6.ruanyifeng.com/#docs/string#模板字符串) 和 属性名表达式:

模板字符串（template string）是增强版的字符串，用反引号（\`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

## 最小宽度：

刚刚想要设置最小的宽度，但是不知道min-width跟width同时出现的时候min-width还管不管用，没想到非常管用，即使width作为内联样式比min-width的优先级高。

### 字符串截取：

slice截取（0，4），返回截取到的字符串。

### 判断一个变量有没有被定义

```
var needLoad = (chathistory === undefined)
```

确实这样写语义更清晰


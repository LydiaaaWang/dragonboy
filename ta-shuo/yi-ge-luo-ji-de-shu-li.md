之前的写法获取不到传出来的值，所以改成了promise的写法，我以为我不会改，没想到我可以

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

虽然以前就解决了，但是我完全想不起来当初是怎么解决的


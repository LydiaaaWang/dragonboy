关于请求的优化-----节流

函数节流运用的实际场景有：窗口调整，页面滚动，抢购疯狂点击等等。

在这里以疯狂点击为例进行分析。

首先写一个简单的页面，当点击按钮时，数字不断增大，模拟抢购按钮。

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="show">0</div>
    <button id="btn">点我</button>
    <script>
        var oDiv=document.getElementById("show");
        oBtn=document.getElementById("btn");
        oBtn.onclick=function(){
            oDiv.innerHTML=parseInt(oDiv.innerHTML)+1
        }
    </script>
</body>
</html>
```

我们肯定不希望用户去疯狂点击导致数字不断增加，甚至是使用恶意脚本去实现疯狂点击按钮

```js
for(var i=0;i<100;i++){
    oBtn.onclick()
}
//此代码无法运行，just 举个栗子
```

所以就要引入一个新思想，_**那就是在一秒钟之内无论用户点多少次，都只算他点了一次，这就是节流的核心思想。**_

```js
function throttle(handle,wait){
    var lastTime=0;
    return function(){
        var nowTime=new Date().getTime();
        if(nowTime-lastTime>wait){
            handle.apply(this,arguments);
            lastTime=nowTime;
        }
    }
}
function buy(){
    oDiv.innerHTML=parseInt(oDiv.innerHTML)+1
}
oBtn.onclick=throttle(buy,1000)
```

现在分析一下throttle方法。

参数中 handle 为需要进行节流的方法，wait为等待时间。

因为我们需要实现在一定的等待时间wait内不能执行buy\(\)方法，所以首先需要两个时间戳，一个记录第一次点击的时间lasttime，一个记录当前的时间nowtime，只有当 nowtime 与 lasttime 的时间差大于wait时，才会再次触发buy\(\)，同时改变lasttime为新时间戳。

放在throttle\(\)中就是首先记录初始时间为0，当第一次点击时，获得现在时间为nowtime，时间差大于wait，执行buy\(\),然后本次点击的时间就成了一个新的时间点，下次点击就需要和这次点击的时间进行判断，所以设置当前时间为初始时间，然后下次点击时继续判断。

防抖和节流虽然实现起来不难，但在实际开发中还是很常用的，因为它们可以极大的优化网络请求性能，提高用户体验。


首先找了一些以前收藏的，发现实现起来没有她说这个小程序里边只是添加类名的方式好，其实他们也有使用html的。

CSS Spinners：在线提供纯css写的页面加载效果，让等待时间不再空白，各种炫酷的CSS加载效果等你来发现！点击想要的效果，会弹出相应代码，复制粘贴即可带走。

```
https://boguz.github.io/Spinners/
```

codepen:

集中了很多的css效果

要想实现微信的那个加载中的效果，我觉得应该让图片旋转起来。

会用到的两个我一直不太熟悉的属性：

transiton属性可以设置旋转所需要的时间

transform属性可以设置旋转的效果

#### 我是这么实现的：

去iconFont矢量图标库找了很多的loading的图，然后让图旋转起来，绕着Z轴

```
transform: rotateZ(0deg);
```

然后不同百分比使用不同的角度

```
@keyframes loadAnimate{
  0% {
    transform: rotateZ(0deg);
  }

  25% {
    transform: rotateZ(90deg);
  }

  50% {
    transform: rotateZ(180deg);
  }

  75% {
    transform: rotateZ(270deg);
  }

  100% {
    transform: rotateZ(360deg);
  }
}
```

最后应用到元素上

```
.loading{
  animation-name: loadAnimate;
  animation-duration: 600ms;
  animation-timing-function: ease-out;
  animation-iteration-count: infinite;
  animation-fill-mode: forwards;
  -webkit-animation-name: loadAnimate;
  -webkit-animation-duration: 600ms;
  -webkit-animation-timing-function: ease-out;
  -webkit-animation-iteration-count: infinite;
  -webkit-animation-fill-mode: forwards;
}
```

把这个类名放到那个图片上就可以了。

###### 最终实现了很多个loading的效果，然后被指导说用微信自带的button的loading就好了。哈哈哈囧。

那么就用微信button的loading效果好了。

那么如何把一个有自身样式的button设为什么样式都没有的呢？

```
<button loading="{{true}}" plain="{{true}}" style='border:none;'></button>
```

组件的width设置成空，就可以根据长度撑开的自己来，组件的width设置为0，那么就真的会是0.


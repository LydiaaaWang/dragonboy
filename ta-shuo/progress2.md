两个进度条变成了先变满了，但是瞬间又回到了开始的阶段，然后才返回的页面。

问题在于interval的执行安排的不ok

如果再细分，是可以实现的，但是这样子写的动画的个数太多了，这样子不好，

待尝试：

还可以使用transition试一下，

也可以使用canvas。

先使用transition:此时这里的position:absolute不能有，并不是，原因又找错了，是因为width没有传到模板内。没有能赋值。

属性的过度效果只需要一个css transition就能搞定，我还想要写动画，看来果然是对这些基础的了解还不够，仅仅只是知道这么一个属性，就可以节省很多时间了。

然后再从编辑普通的开始-&gt;上传图片--&gt;图片和编辑都有的

将所有的that=this去掉

```
Math.floor() 返回小于或等于一个给定数字的最大整数
```

看到了一个随机跑进度的例子：https://justcoding.iteye.com/blog/2210960

一个感觉比较6的进度条：https://blog.csdn.net/zhangke3016/article/details/52195711 可以用在自己的项目上



出问题的原因在于两个interval同时存在的时候会一起同时执行两个interval.所以interval只能有一个存在

那如果是两个interval 一个控制width 一个控制percent呢？

关于timer的处理：timer的并不是clear之后就不存在了，而是保留了上一次执行的次数的值，反正有值。所以，如果想要下一次interval顺利执行，那么就需要把timer设置成为null.

需要试一下能否在  封装公共函数的时候涉及到本页面的数据也能使用


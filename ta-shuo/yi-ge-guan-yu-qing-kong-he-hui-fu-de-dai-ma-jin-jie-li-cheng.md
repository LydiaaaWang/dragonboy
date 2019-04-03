# 一个关于清空和恢复的代码进阶历程

最开始是把需要保存到了storage里边。

但是大神说缓存这个东西比较重1是耗时 2是难用，它有限制，10mb,不会轻易消除，意味着它是消耗品。remove移除之后也不行，因为remove是有可能失败的，缓存读取和删除成功率都不是100%，能用变量的我一般是不会用缓存的。如果接触过后端语言，那么缓存就好比数据库。

setData的成功率差不多是100%，因为只要代码没错它就会100%执行，因为它就是跑代码，storage相当于和数据库交互，是异步的，在某些特殊情况会有问题，所有异步的操作都可能失败。

接着改了一个版本把所有的代码放到了上一个页面里边，假设它离开了就不需要了。

改完之后发现有一些变没了这样不好，虽然功能是实现了，但是不是最佳的方案。

最终的方案是把所有的需要保存的数据放到globalData里边，接着也可以把它弄成一个js文件放到utill里边。这样的话就相当于维护一个本地的数据库。每一个页面都可以引入js,并且都可以使用以及修改js里的值。

这是看起来集成度最高的一种做法了。

那么这种做法要怎么写呢？

在utils文件夹下建立一个文件，比如叫clearData.js,然后定义一个变量叫clearData

```
var clearData={}//使用var ,不使用const的原因是这个里边的数据得进行改动
```

然后再暴露出去让每个需要用到的页面都可以引入它使用。那么

```
export default clearData;
```

需要使用的页面怎么引入呢？

```
import clearData from "../../utils/clearData.js"  //可以是相对路径也可以是绝对路径,小程序上使用绝对路径不成
```

上面的export和import是ES6的语法，目前最好的模块解决方案就是用ES6.

## 相关链接

[module.exports与exports，export与export default之间的关系和区别](https://www.cnblogs.com/fayin/p/6831071.html)

[CommonJS规范](http://javascript.ruanyifeng.com/nodejs/module.html)

[ES6 Module 的语法](http://es6.ruanyifeng.com/#docs/module)

这里边需要操作的有：

删除对象的某一个属性：

```js
var a={"id":1,"name":"danlis"};
//添加属性
a.age=18;
console.log(a);
//结果：Object { id: 1, name: "danlis", age: 18 }
//修改属性
a.age="我怎么知道";
//结果：Object { id: 1, name: "danlis", age: "我怎么知道" }
//删除属性
delete a.age;
//结果：Object { id: 1, name: "danlis" }
```

如上 `delete a.age`或者`delete a[age]`

如果希望更改某一个值那么怎么修改呢，修改后需要保存到js里边去呢。

需要懂得就是这个js文件得增删改查。

```
如果想要更改属性和属性值，直接更改就成，其他模块可以读到改写后得值。
```

那么export default到底是啥意思？

```
本质上，export default就是输出一个叫做default的变量或方法，然后系统允许你为它取任意名字。
```
























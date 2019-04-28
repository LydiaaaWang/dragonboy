第一次了解到关于请求的优化---防抖和节流

啥是防抖？

**防抖\(debounce\)**：在函数需要频繁触发时，只有当有足够空闲的时间时，才执行一次。就好像在百度搜索时，每次输入之后都有联想词弹出，这个控制联想词的方法就不可能是输入框内容一改变就触发的，他一定是当你结束输入一段时间之后才会触发。

函数防抖运用的实际场景有：实时搜索，拖拽，登录用户名密码格式验证等等。

实现函数防抖的关键就是对setTimeout\(\)这个方法的运用。先以实时搜索为例分析一下。

首先我们要写一个监听函数用来监听搜索框的value的变化。

```js
var oInp;// 假设在此取得输入框
oInp.oninput = ajax;
// 模拟ajax请求后台数据
function ajax() {
    console.log(this.value);// 搜索框value值
}
```

写完之后我们会发现每当我们输入一个单词，即每当搜索框内容发生变化时都会触发我们的监听函数来请求后台数据，如此频繁的请求肯定不是我们想要的，所以我们就需要稍加处理一下，使其不再一改变就触发，而是当我们输完之后再触发发送请求。针对这种需求我们可以使用防抖来实现。

```js
var oInp;// 假设在此取得输入框
var timer = null; // 定义一个全局定时器
oInp.oninput = function(e) {    
  clearTimeout(timer);    
  timer = setTimeout(function(){       
    ajax();    
   }, 1000);
 };
 // 模拟ajax请求后台数据
 function ajax() {console.log(this.value);// 搜索框value值}

```

这个整体的实现思想就是，当搜索框内容发生改变时，就会触发一个定时器。但是当搜索框内容再次发生改变时，我们先清除上一个定时器，再重新创建一个定时器。这样，只有当我们结束输入，搜索框内容在一定时间内不再发生改变时才会发送请求。

但是上面的代码块还有两个问题，一个就是this的指向，setTimeout\(\)形成了一个闭包，当执行的时候，ajax\(\)方法中的this实际指向window，所以我们还需要进行以下优化，改变this指向。

我的理解：其实只需要使用es6的箭头函数就好了。

```js
var oInp;// 假设在此取得输入框
var timer = null; // 定义一个全局定时器
oInp.oninput = function(e) {    
    var _this = this;
    clearTimeout(timer);
   timer = setTimeout(function(){
       ajax().apply(_this); // 绑定this
   }, 1000);};
// 模拟ajax请求后台数据
function ajax(){    
    console.log(this.value);// 搜索框value值
}

```

第二个问题就是e -- 事件对象，在上面一系列的方法调用之中，e已经被丢了，变成了undefined,所以我们还需要进行以下优化，将事件对象重新找回来。

```js
var oInp;// 假设在此取得输入框
var timer = null; // 定义一个全局定时器
oInp.oninput = function(e) {
    var _this = this,
    _arg = arguments; // e
     clearTimeout(timer);
     timer = setTimeout(function(){
       ajax().apply(_this, _arg); // 绑定this, 传入e
     }, 1000);
};
// 模拟ajax请求后台数据
function ajax(){    
    console.log(this.value);// 搜索框value值
}
 
```




我的理解：就是会返回，中止函数的运行。

如果直接`return; `那么没有函数结果

如果是` return false; `那么：一般情况下为事件处理函数返回false,可以防止默认的事件行为。例如，默认情况下点击一个&lt;a&gt;元素，页面会跳转到该元素href属性指定的页。但是如果不希望执行这个事件而是执行其他事件比如执行自定义的onclick，那么这时候就可以给这个事件处理函数加上这一句，然后就来执行这个事件处理函数了，而不会去执行链接的跳转。所以一般都是用来取消默认行为的、阻止提交表单的、阻止继续执行下面的代码的。让表单的提交事件返回false,那表单就不会提交:onsubmit="return false";

如果是return true; 那么会返回正确的处理结果？依然是上边的&lt;a&gt;元素，此时如果使用return true;那么依然会跳转链接。其实return true;就相当于 return x+y;这种







\[参考资料\]

MDN （https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/return）

博客资料 （https://www.cnblogs.com/zhangym118/p/6438702.html）


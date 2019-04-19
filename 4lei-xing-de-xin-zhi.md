关于数据类型 我的理解：

`undefined==null`

`null`是一个表示“空”的对象，转为数值时为`0`；`undefined`是一个表示"此处无定义"的原始值，转为数值时为`NaN`。

我的理解：一般没有主动定义一个变量为undefined的情况。而且他俩竟然相等。undefined的意思就是未定义。

调用函数时，某个参数未设置任何值，这时就可以传入`null`，表示该参数为空。

我的理解：所以下次如果一个函数有几个参数，但是其中的某个参数这里又不需要，并且定义的时候就设置了默认值，那么下次可以使用传入null。

`parseInt()`是一个全局的将字符串转换为整数的方法，但是也有很多的特殊情况，只是目前觉得不太需要记住。

`parseFloat()`是一个全局的将字符串转换为小数的方法，

他俩都是针对字符串的，所以如果传入其他的值会出现各种各样的问题。

`isNAN()`返回的`true`的不只是`NAN`，还有字符串，所以这个方法只对传入数字有效。就因为这个特点，

```
typeof value === 'number' && isNaN(value)  所以先判断类型然后再判断是不是数字这样才会比较好。
```

对以上这一点的我的感觉：哇哇哇，这才是比较好的js程序写出来应该是的样子。人家甚至提出了一个更好的方法，那就是NAN是唯一一个不等于自身的值。我奇怪了，那么无穷等于无穷嘛?在控制台上打印了一下，还真是这样子的。

```
Infinity==Infinity  // true
```

有一个方法存在，判断一个值是不是正常的数值，isFinite\(\),感觉没啥用，因为null的返回也是true

字符串与数组是相似的，但是数组有增删改查，但是字符串是没有的。这些操作会默默地失败，但是没有错误提醒。

unicode是关于字符串的。有的字符返回的length是两个，所以JavaScript 返回的字符串长度可能是不正确的。

为什么要使用base64?不是为了加密，而是为了不出现特殊字符。

原来js是自带了base64转化的，完全不需要去其他网站转换base64格式了。

```
function b64Encode(str) {
  return btoa(encodeURIComponent(str));
}

function b64Decode(str) {
  return decodeURIComponent(atob(str));
}

b64Encode('你好') // "JUU0JUJEJUEwJUU1JUE1JUJE"
b64Decode('JUU0JUJEJUEwJUU1JUE1JUJE') // "你好"
```

对象，是JavaScript最重要的数据类型，确实是一个非常重要的类型，能简化很多循环类的操作。都是key-value.所有的key都是字符串。如果是数值，也会被转化为字符串。还有一个深化我对对象印象的，那就是属性随便增加和删除。不用在声明的时候就得有。还可以查看一个对象拥有的所有属性，使用

```
var obj = {
  key1: 1,
  key2: 2
};

Object.keys(obj);
// ['key1', 'key2']
```

就可以。

还可以遍历整个对象，用的是for...in...循环。

这是一个成熟的方法：

```
var person = { name: '老张' };

for (var key in person) {
  if (person.hasOwnProperty(key)) {
    console.log(key);
  }
}
//这样子的话就会只遍历对象自身的属性了。
```

核心参考  [阮一峰 js入门](https://wangdoc.com/javascript/types/number.html)


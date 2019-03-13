

## 原始（Primitive）类型

---

弄清楚一个问题：原始类型有哪几种？null 是对象嘛？

在 JS 中，存在着 6 种原始值，分别是：

* `boolean`
* `null`
* `undefined`
* `number`
* `string`
* `symbol`

首先原始类型存储的都是值，是没有函数可以调用的，比如`undefined.toString()`，此时会报错。但是`'1'.toString()`是可以使用的。其实在这种情况下，`'1'`已经不是原始类型了，而是被强制转换成了`String`类型也就是对象类型，所以可以调用`toString`函数。

另外对于`null`来说，很多人会认为他是个对象类型，其实这是错误的。虽然`typeof null`会输出`object`，但是这只是 JS 存在的一个悠久 Bug。在 JS 的最初版本中使用的是 32 位系统，为了性能考虑使用低位存储变量的类型信息，`000`开头代表是对象，然而`null`表示为全零，所以将它错误的判断为`object`。虽然现在的内部类型判断代码已经改变了，但是对于这个 Bug 却是一直流传下来。

**我的理解**：symbol这个独一无二的值，定义的时候直接Symbol函数，这个函数可以加参数，即使参数相等，但是两个symbol的值是不相等的。转为字符串和布尔值都是可以的。转为布尔值的时候是true.由于可以转为字符串，所以作为对象的属性值的时候不能使用点，而是使用方括号。目前我还不知道可以在哪里使用==

## 对象（Object）类型

---

弄清楚一个问题；对象类型和原始类型的不同之处？函数参数是对象会发生什么问题？

**我的理解：**最根本的不同是存储的东西不一样，原始类型存储的是值，对象类型存储的是地址（指针）。

在 JS 中，除了原始类型那么其他的都是对象类型了。对象类型和原始类型不同的是，原始类型存储的是值，对象类型存储的是地址（指针）。当你创建了一个对象类型的时候，计算机会在内存中帮我们开辟一个空间来存放值，但是我们需要找到这个空间，这个空间会拥有一个地址（指针）。

```js
const a = []
```

对于常量`a`来说，假设内存地址（指针）为`#001`，那么在地址`#001`的位置存放了值`[]`，常量`a`存放了地址（指针）`#001`，再看以下代码

```js
const a = []

const b = a
b.push(1)
```

当_我们将变量赋值给另外一个变量时，复制的是原本变量的地址（指针）_，也就是说当前变量`b`存放的地址（指针）也是`#001`，当我们进行数据修改的时候，就会修改存放在地址（指针）`#001`上的值，也就导致了两个变量的值都发生了改变。

接下来我们来看函数参数是对象的情况

```js
function test(person) {
  person.age = 26
  person = { name: 'moon',age: 30}
  return person
}

const p1 = {
  name: 'wang',
  age: 25
}

const p2 = test(p1)
console.log(p1) // -> ?
console.log(p2) // -> ?
```

对于以上代码，你是否能正确的写出结果呢？接下来让我为你解析一番：

* 首先，函数传参是传递对象指针的副本
* 到函数内部修改参数的属性这步，我相信大家都知道，当前`p1`的值也被修改了
* 但是当我们重新为`person`分配了一个对象时就出现了分歧，请看下图



![](https://user-gold-cdn.xitu.io/2018/11/14/16712ce155afef8c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



所以最后`person`拥有了一个新的地址（指针），也就和`p1`没有任何关系了，导致了最终两个变量的值是不相同的。

**我的理解：**只有在变量赋值给另一个变量的时候才会赋值地址，但是使用一个对象赋值那么就不会只赋值地址，就会整个都改。

## typeof vs instanceof

---

弄清楚一个问题：typeof 是否能正确判断类型？instanceof 能正确判断对象的原理是什么？

`typeof`对于原始类型来说，除了`null`都可以显示正确的类型

```js
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
```

`typeof`对于对象来说，除了函数都会显示`object`，所以说`typeof`并不能准确判断变量到底是什么类型

```js
typeof [] // 'object'
typeof {} // 'object'
typeof console.log // 'function'
```

如果我们想判断一个对象的正确类型，这时候可以考虑使用`instanceof`，因为内部机制是通过原型链来判断的，在后面的章节中我们也会自己去实现一个`instanceof`。

```js
const Person = function() {}
const p1 = new Person()
p1 instanceof Person // true

var str = 'hello world'
str instanceof String // false

var str1 = new String('hello world')
str1 instanceof String // true
```

对于原始类型来说，你想直接通过`instanceof`来判断类型是不行的，当然我们还是有办法让`instanceof`判断原始类型的

```js
class PrimitiveString {
  static [Symbol.hasInstance](x) {
    return typeof x === 'string'
  }
}
console.log('hello world' instanceof PrimitiveString) // true
```

你可能不知道`Symbol.hasInstance`是什么东西，其实就是一个能让我们自定义`instanceof`行为的东西，以上代码等同于`typeof 'hello world' === 'string'`，所以结果自然是`true`了。这其实也侧面反映了一个问题，`instanceof`也不是百分之百可信的。

我的理解：看来并没有一个办法瞬间把所有的类型分辨出来。typeof用来看简单类型。instanceof用来看对象类型。



参考资料 [yck掘金小册](https://juejin.im/book/5bdc715fe51d454e755f75ef/section/5c024ecbf265da616a476638#heading-5)


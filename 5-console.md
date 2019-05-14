js有一个东西叫占位符 %s %d %c

如果以后想知道某个方法调用了多少次，那么不需要定义一个变量去++了，直接console.count













如果以后想要知道某个操作的过程花的时间总和，那么就可以使用console.time\("name"\)与console.timeEnd\("name"\)

```
console.time('Array initialize');

var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};

console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```

console.clear\(\)可以清空控制台的内容，当然也可以使用其他清空.



判断一个变量是否为对象：

```js
function isObject(value) {
  return value === Object(value);
}

isObject([]) // true
isObject(true) // false
```




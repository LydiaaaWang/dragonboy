数组的操作方法里边：

pop push  shift unshift 方法执行之后，改变的都是执行这个方法的数组。

concat\(\)连接两个数组形成一个新的数组。`arr.concat(arr2)`

fill\(\)  使用固定值填充数组

```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.fill("Runoob");
输出结果：
Runoob,Runoob,Runoob,Runoob
```

for  ... of

for...in

使用filter进行数组的一个拷贝：对新生成的数组进行操作不会影响原来的数组

```
var arr = invite.filter(d=>d)
```

**`findIndex()`**方法返回数组中满足提供的测试函数的第一个元素的**索引**。否则返回-1。

就因为这个的存在，可以使用一个数组管理n个名字不同的对象。


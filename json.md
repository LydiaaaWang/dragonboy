[json.stringify\(\)和json.parse\(\)](https://www.cnblogs.com/panmy/p/5925986.html)

json.stringfy\(\)将对象、数组转换成字符串；json.parse\(\)将字符串转成json对象。

我的理解：

json里边不能使用单引号

用法：

判断两个数组是否相等，可以先将数组字符串化，然后直接用==来判断是否相等。



深拷贝的一种方法：

JSON.parse\(JSON.stringify\(某个数组/某个对象\)\)


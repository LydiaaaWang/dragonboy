# markdown语法介绍
Markdown 是一种轻量级标记语言

##标题
Markdown 共支持六级标题
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```
效果如下：
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

##锚点
待完善

##引用
段落前加`>`即可

>这是一段引用文本。
引用可以嵌套，不过一般没必要这么做。

```
> ## 这是一个标题。
> 1. 这是第一行列表项。
> 2. 这是第二行列表项。
>
> 给出一些例子代码：
>
> return shell_exec(`echo $input | $markdown_script`);
```

效果：
> ## 这是一个标题。
> 1. 这是第一行列表项。
> 2. 这是第二行列表项。
>
> 给出一些例子代码：
>
> return shell_exec(`echo $input | $markdown_script`);

##列表
####无序：
使用星号、加号或是减号作为列表标记 `* + -`
```
- hhh
- www
- oooo
```
效果如下：

- hhh
- www
- oooo

####有序：使用数字+英文句号+空格
```
1. 第一行
2. 第二行
```
1. 第一行
2. 第二行

##斜体与加粗

####斜体与加粗：

```
**这是加粗的文字**
*这是倾斜的文字*`
***这是斜体加粗的文字***
~~这是加删除线的文字~~
```

**这是加粗的文字**
*这是倾斜的文字*`
***这是斜体加粗的文字***
~~这是加删除线的文字~~

##超链接
方括号显示说明，圆括号内显示网址， Markdown 会自动把它转成链接。比如说：
`[这里是维基百科](https://lydiaaawang.github.io/)`
效果是：[这里是维基百科](https://lydiaaawang.github.io/)

##图片超链接
`![这是一张图片](http://img.xzkz.com/data/attachment/forum/201610/01/135533xt2xhkk7x5avhjv3.jpg)`

一个惊叹号『!』，接着一个方括号，里面是图片的替代文字，接着一个普通括号，里面是图片的网址，

效果：

![这是一张图片](http://img.xzkz.com/data/attachment/forum/201610/01/135533xt2xhkk7x5avhjv3.jpg)

如果这样就是导致图片看起来特别大，因为显示的是原来的大小，那么怎么让图片显示的小一点呢？
<img src="http://img.xzkz.com/data/attachment/forum/201610/01/135533xt2xhkk7x5avhjv3.jpg" alt="" width="100px"/>

`<img src="http://img.xzkz.com/data/attachment/forum/201610/01/135533xt2xhkk7x5avhjv3.jpg" alt="" width="100px"/>`是通过这个代码实现变小的。因为gitbook支持`html`.

##分割线
使用3个及三个以上的`-`就可以实现一个分割线，✍ 注意：分割线前后必须有空格，否则将不会起作用。
三个或者三个以上的 `-` 或者` * `都可以。
```
哈哈哈

---

嘿嘿嘿
```

哈哈哈

---

嘿嘿嘿

##关于特殊符号
浏览器可以解析，所以就能使用啦。
搜索【特殊符号】就能看到相关的[网站](http://cn.piliapp.com/symbol/)。以下是部分符号：网站上还能看到符号的原始含义。
ღ • ⁂ € ™ ↑ → ↓ ⇝ √ ∞ ░ ▲ ▶ ◀ ● ☀ ☁ ☂ ☃ ☄ ★ ☆ ☉ ☐ ☑ ☎ ☚ ☛ ☜ ☝ ☞ ☟ ☠ ☢ ☣ ☪ ☮ ☯ ☸ ☹ ☺ ☻ ☼ ☽ ☾ ♔ ♕ ♖ ♗ ♘ ♚ ♛ ♜ ♝ ♞ ♟ ♡ ♨ ♩ ♪ ♫ ♬ ✈ ✉ ✍ ✎ ✓ ✔ ✘ ✚ ✝ ✞ ✟ ✠ ✡ ✦ ✧ ✩ ✪ ✮ ✯ ✹ ✿ ❀ ❁ ❂ ❄ ❅ ❆ ❝ ❞ ❣ ❤ ❥ ❦ ❧ ➤ ツ ㋡ 卍 웃 Ⓐ Ⓑ Ⓒ Ⓓ Ⓔ Ⓕ Ⓖ Ⓗ Ⓘ Ⓙ Ⓚ Ⓛ Ⓜ Ⓝ Ⓞ Ⓟ Ⓠ Ⓡ Ⓢ Ⓣ Ⓤ Ⓥ Ⓦ Ⓧ Ⓨ Ⓩ

დ ღ ♡ ❣ ❤ ❥ ❦ ❧ ♥

☚ ☛ ☜ ☝ ☞ ☟ ✌ ✍

♔ ♕ ♖ ♗ ♘ ♙ ♚ ♛ ♜ ♝ ♞ ♟

♩ ♪ ♫ ♬ ♭ ♮ ♯

ϟ ☀ ☁ ☂ ☃ ☄ ☉ ☼ ☽ ☾ ♁ ♨ ❄ ❅ ❆

☠ ☤ ☥ ☦ ☧ ☨ ☩ ☪ ☫ ☬ ☮ ☭ ☯ ☸ ☽ ☾ ♕ ♚ ♛ ✙ ✚ ✛ ✜ ✝ ✞ ✟ ✠ ✡ ✢ 卍 卐

‱ № ℗ ℠ ℡ ℀ ℁ ℅ ℆ ⅍ ⌚ ⌛ ☊ ☎ ☏ ✁ ✂ ✃ ✄ ✆ ✇ ✈ ✉ ✍ ✎ ✏ ✐ ✑ ✒ ™ © ® ‰ § ¶

⏎ ⇧ ⇪ ⌂ ⌘ ☢ ☣ ⌥ ⎋ ⌫  ᴴᴰ

♈ ♉ ♊ ♋ ♌ ♍ ♎ ♏ ♐ ♑ ♒ ♓

ˇ ∛ ∜ ☐ ☑ ☒ ✓ ✔ ✗ ✘ ∨ √

♡ ♢ ♤ ♧ ♣ ♦ ♥ ♠
##表格
markdown支持制作表格



```
First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell
```

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

上边这种可以成为表格不是因为对的齐，而是因为竖线`|`两边是有空格的。如果没有空格那么就不能成功的显示为空格了。
```
表格标题 | 第一列 | 第二列
--------|-------|-------
name | wanglala | liumiaomiao
age | 19 | 20
```
表格标题 | 第一列    |   第二列
--------| -------   |  -------
name    | wanglala  | liumiaomiao
age     | 19        | 20

并且表格内容左对齐、右对齐、居中对齐这个也是可以调整的。那么怎么调嘞？
```
First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right
```
First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right



哇，实现了，然而这些东西没什么神奇的，不过是制定的规则而已。只要当我们想要实现的时候能够实现这个效果，大家好沟通，那么就是最大的正义了。

##流程图、时序图、甘特图

关于这个流程图怎么画：我觉得这个[mermaid](https://mermaidjs.github.io/)不错.
如果是单纯的`gitbook`那么不支持这个`mermaid`,但是如果可以引入这个meamaidjs，那么就可以在网页上绘制流程图了。当然，并没有觉得比目前最流行的思维导图好在哪里。我还是觉得思维导图的工具比marmaidjs好用。


>markdown语法暂时了解到这里，以后如果遇到新的，可以随时更新。这里就是我的技能仓库了。


关于touch事件的那些个参数----e

target与currentTarget傻傻分不清楚。

target是触发这个事件的那个组件的一些属性值的集合，

currentTarget是当前组件的一些属性值集合

touches与changedTouches也傻傻分不清楚



catch事件是这样起作用的：

```
<view class="out" bindtap="handleEventOut">
    <view class="in" catchtap="handleEventIn">
    </view>
</view>
这种时候，内部view就不会触发外部的out事件。如果用bindtap，那么就会触发外部的out事件。
```




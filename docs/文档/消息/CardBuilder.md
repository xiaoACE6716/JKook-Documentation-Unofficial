# CardBuilder

`CardBuilder`可用的方法有`setSize`,`setTheme`,`setColor`,`addModule`,`newCard`,`build`。

## setSize

`setSize`方法作用为设置卡片大小,`Size`枚举中存放了可用的大小设置，卡片本身仅支持 `LG` 与 `SM`，其余的大小是给卡片模块用的。

!> 使用错误的Size会导致卡片消息无法通过KOOK消息验证，卡片在移动端 KOOK 只会使用 `SM` 大小。~~适配移动端是一件很痛苦的事。~~

## setTheme 与 setColor

`setTheme`与`setColor`方法作用为设置卡片边框风格颜色,其中`Theme`枚举存放了可用的Theme设置，而`setColor`可用具体颜色的十六进制代码来设置颜色。

## addModule

`addModule`方法顾名思义为往卡片里添加模块，具体用法在[卡片模块](文档/消息/CardModule.md)里，这里会给出所有的例子。

!>注意，**一条卡片消息**里最多添加**50个模块**。
虽然**一条卡片消息**最多可分为**5张卡片**，但是**5张卡片**一共最多只能有**50个模块**。

## newCard

**一条卡片消息**可以分为5张卡片，而`newCard`方法则是结束前一张卡片的`setXXX`与`addModule`然后开始对下一张卡片进行操作。

!> 调用了此方法后，build出来的对象应该是 `MultipleCardComponent` 对象

## build

`build`方法作用为结束卡片消息的构建，转化为`CardComponent`或`MultipleCardComponent`对象。
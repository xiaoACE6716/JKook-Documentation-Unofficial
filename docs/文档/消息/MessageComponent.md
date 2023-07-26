## 消息组件

消息组件（英文 `Component`）一词同样借鉴于游戏 Minecraft ，用于存放消息的内容。
* _为什么实体和消息组件的名称都借鉴于 Minecraft ？因为 JKook 的作者[ZX夏夜之风](https://github.com/SNWCreations)就是个 Minecraft 玩家。_

JKook API 中的消息组件全部放在了 `snw.jkook.message.component` 包下。

`BaseComponent` 为消息组件的顶级父类。

`TextComponent` 为纯文本消息组件。
* **KOOK 官方已经弃用纯文本消息。** 所有的纯文本消息会在 KOOK 的服务端转换为 Markdown 之后再发送。

`MarkdownComponent` 为 Markdown 消息组件。继承自 `TextComponent` 类。

`FileComponent` 表示一个文件消息组件。

`FileComponent` 类下提供了一个 `Type` 枚举，表明文件的类型，支持 `AUDIO`（音乐），`VIDEO`（视频），`IMAGE`（图片），`FILE`（普通文件）。

你可以根据文件的类型，在构造它的时候指定类型。不同的类型在 KOOK 客户端中渲染的效果不一样。

**发送音乐文件时更推荐使用卡片消息中的 `FileModule` ，可以指定封面图片。**

## 发送消息

通常地，向一个文字频道发送一个消息组件只需要使用 `TextChannel#sendComponent` 方法即可。

向一个用户的私信发送一个消息组件？使用 `User#sendPrivateMessage` 方法即可。

### 回复消息

回复消息有两种方式。

1. 获取消息的来源（在私信中指用户，在文字频道中就是文字频道本身），然后调用相应的发送消息的方法
2. 直接使用 `Message#reply` 。

使用第一个方法可以这么写:
```java
BaseComponent component;
Message message;
if (message instanceof TextChannelMessage) {
    ((TextChannelMessage) message).getChannel().sendComponent(component, message, null);    
} else {
    message.getSender().sendPrivateMessage(component, message);
}
```

但这种方法如果想要大量使用必须封装，否则会造成很多重复代码。

但是，第二个方法是由 API 直接提供封装。

只需要一行代码:
```java
message.reply(component);
```

### 发送消息到消息来源

如果你不是想回复某个消息、命令的，而是直接把消息发送出来

你可以使用另一个由 `Message` 提供的便利方法: `Message#sendToSource` 。

只需要一行代码:
```java
message.sendToSource(component);
```

### 临时消息

这是一个神奇的东西。

一个临时消息具有如下特性：
* 只能出现在文字频道中
* 仅有指定的用户可以看见
* 如果你指定了用户对象，临时消息会在指定的用户的 KOOK 客户端的消息缓存刷新(最快触发的方法是直接重启KOOK客户端)后消失(变回原来的内容)
* 不可更新

因为第一条特性，发送一个临时消息需要将 `Message` 对象转为 `TextChannelMessage` 对象，然后再调用相关方法。
* 请务必先对消息对象进行 `instanceof` 检查。 **永远不要做未经检查的向下转换。**

我们支持回复消息的同时把消息作为临时消息，也支持直接发送到消息来源的同时设置为临时消息。

对于前者的情况，使用 `TextChannelMessage#replyTemp` 方法，对于后者的情况，使用 `TextChannelMessage#sendToSourceTemp` 方法。

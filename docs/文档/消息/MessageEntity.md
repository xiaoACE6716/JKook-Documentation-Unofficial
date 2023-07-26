## 消息对象

消息对象目前有两种：`TextChannelMessage` 和 `PrivateMessage` 。它们有一个共同的父类是 `Message` 接口。

### Message

完整限定名为 `snw.jkook.message.Message` 。

作为对一个消息的基本抽象，此接口可以获取的内容比较多。其子类主要是提供一些功能扩展。

通过 `Message#getId` 方法可以获得此消息的 ID 。

消息 ID 是一个 UUID 。

通过 `Message#getSender` 方法可以获得此消息的发送者。

通过 `Message#getTimeStamp` 方法可以获得此消息被发送时的时间戳。

通过 `Message#getComponent` 方法可以获得此消息包含的消息组件。通过消息组件对象，你可以得知用户发送的内容。消息组件相关内容将在后面讲解。

更新一条消息的内容可以使用 `Message#setComponent` 方法，但只支持更新 KMarkdown 消息以及卡片消息。   
**只能更新机器人自己发出的消息。**

删除一条消息可以使用 `Message#delete` 方法。在私信中只能删除自己的消息，在文字频道中删除其他人的消息需要自己有消息管理权限。

在一条消息被删除后，对其对应的消息对象进行更新等操作将失败，因此，已被删除的消息的消息对象不再具有可用性。

`TextChannelMessage` 主要提供了更多的功能，如向频道发送一个临时消息的快捷封装，以及获取消息所在的文字频道。


## 获取消息对象

### 通过事件去获取

在`ChannelMessageEvent`与`PrivateMessageReceivedEvent`中可通过`getMessage`方法获取消息对象。

### 通过命令系统去获取

在`CommandExecutor`与`UserCommandExecutor`中，`onCommand`方法均提供了`Message`对象，该对象为触发命令的消息的对象。

### 通过消息ID去获取

~~你可以拿着消息ID去使用`JKook.getCore().getUnsafe()`里的`getTextChannelMessage`与`getPrivateMessage`方法去获得一个**简单构造**的消息对象，  
该对象只能用于**更新消息**与**删除消息**~~

在KOOK更新了API与JKook API更新到0.49.0版本之后，上述方法已经弃用! ~~其实还可以用~~

现在，你可以拿着消息ID去使用`JKook.getHttpAPI()`里的`getTextChannelMessage`与`getPrivateMessage`方法去获得一个**完整**的消息对象了。  
另外`getPrivateMessage`还需要传入一个`User`用户对象。
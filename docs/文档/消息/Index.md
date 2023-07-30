# 消息

消息是由 KOOK 用户发送的，包含了一些内容的实体。  
**消息也是一种实体**，在[实体](文档/实体/Index.md#实体)中，我们讲过为什么他不在`entity`包下

## 消息对象

消息对象目前有两种：`TextChannelMessage` 和 `PrivateMessage` 。它们有一个共同的父类是 `Message` 接口。

## 消息对象从何而来

### 通过命令系统

在命令系统的 `CommandExecutor` 和 `UserCommandExecutor` 接口的 `onCommand` 方法均提供了 `Message` 对象，表示导致命令被执行的消息对象。

### 通过事件系统

可在事件系统中的 `ChannelMessageEvent` 与 `PrivateMessageReceivedEvent` 中的 `getMessage` 方法获得消息对象。

### 通过消息ID

#### 通过Unsafe接口

在KOOK官方没提供消息详情查询接口之前，我们可以通过Unsafe接口简单构建出一个消息对象。

!> 此处构建出来的消息对象只能用于**更新消息**、**删除消息**、**回复消息**、**添加回应**。

```java
// 获取文字频道信息
JKook.getCore().getUnsafe().getTextChannelMessage("1233211234567");
// 获取私信
JKook.getCore().getUnsafe().getPrivateMessage("1233211234567");
```

#### 通过HttpAPI接口

自 API 0.49.0开始，可以用**信息ID**去调用 `HttpAPI` 接口的 `getTextChannelMessage` 与 `getPrivateMessage` 方法去获取完整消息了。

```java
// 获取文字频道信息
JKook.getHttpAPI().getTextChannelMessage("1233211234567");
// 获取私信
// 注意，获取私信还需要传入该私信来源的用户对象
JKook.getHttpAPI().getPrivateMessage(User,"1233211234567");
```

# 实体

实体 (英文 `Entity`) 一词借鉴于游戏 Minecraft ，这里表示一个可以产生交互的对象。  
JKook API 将对于 KOOK 软件中的"实体"及其附属内容的抽象放在 `snw.jkook.entity` 包下。  
消息实体除外，因为包名太长了，[ZX夏夜之风](https://github.com/SNWCreations)将它放到了根包下。~~然而还是很长~~ 

## 获取实体

你可以通过`JKook.getHttpAPI()`接口来获取**实体**的实例，比如: `User`、`Guild`、`Channel`的实例。  
还有一些附属于某些实体的实体可以通过实体的一些相关方法来获得。  
还可以通过事件系统、或者命令系统来获得某些实体实例。

## 具体内容

### 消息

消息的体系较大，所以我们独立出来放到了[消息](文档/消息/Index.md)。

### 用户

`User`: 表示一个用户。  
而机器人也是一种用户。

### [服务器](文档/实体/Guild.md)

`Guild`: 表示一个服务器。

### 游戏

`game`: 表示一个游戏(也可能是一个软件，还有可能是一个vup)。

### 表情

`CustomEmoji`: 表示一个表情。  
可以是 KOOK 原生的Emoji。也可以是个人上传的表情或服务器的表情。  

获取原生Emoji实例需要提供Emoji的Unicode，Unicode表可到[表情符号列表](附录/表情符号/emoji-list.md)查询。
```java
// 获取原生Emoji实例
JKook.getCore().getUnsafe().getEmoji(Unicode);
// 获取服务器自定义Emoji列表
Guild.getCustomEmojis()
```
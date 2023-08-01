# 消息组件

## 基本概念
> 消息组件（英文 `Component`）一词同样借鉴于游戏 **Minecraft** ，用于存放消息的内容。

分别为:  
 `BaseComponent`: 消息组件们的顶级父类。  

`TextComponent`: 纯文本消息组件。  

!> 注意！**KOOK 官方**已经弃用了纯文本消息。所有的纯文本消息会被 KOOK 转为 [KMarkdown](https://developer.kookapp.cn/doc/kmarkdown) 之后再发送。

`MarkdownComponent`: Markdown 消息组件。

`FileComponent`: 文件消息组件。

> `FileComponent` 类下提供了一个 `Type` 枚举，表明文件的类型，  
> 支持 `AUDIO`（音乐），`VIDEO`（视频），`IMAGE`（图片），`FILE`（普通文件）。  
> 你可以根据文件的类型，在构造它的时候指定类型。不同的类型在 KOOK 客户端中渲染的效果不一样。  
> **发送音乐文件时更推荐使用卡片消息中的 `FileModule` ，可以指定封面图片。**

```java
// 一个图片消息的实例
FileComponent fileComponent = new FileComponent("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg", "没见过这么萌的狗狗吗？", 1024, FileComponent.Type.IMAGE);
```

`CardComponent` 与 `MultipleCardComponent` : 卡片消息组件。前者为单张卡片，后者为多张卡片。  
可以通过[CardBuild](文档/消息/CardBuilder.md)去帮助构建卡片。

### 发送消息与回复消息

向一个频道发送消息只需调用`TextChannel#sendCompoent(component)`方法即可。  
向一个用户发私信只需调用`User#sendPrivateMessage(component)`方法即可。  
回复一条消息只需调用 API封装好的 `Message#reply(component)`方法即可。  
如果你想回复一条消息，但是又不想直接用回复而是直接发到频道(或私信)里，API也有封装好的`Message#sendToSource`方法。

### 更新消息

想要修改一条消息，只需调用`Message#setComponent(component)`方法即可。  

!> 注意，不要把非卡片消息更新成卡片消息，也不要把卡片消息更新成非卡片消息。  
无论你怎么做，结果都不会如你想象的一样。~~甚至还会报错~~

### 删除消息

调用 `Message#delete`方法即可。

!> 不要对着临时消息进行删除操作(虽然我不知道你是怎么拿到临时消息的对象的)。  
因为它根本不会存进 KOOK 数据库内，调用删除方法会返回消息不存在。

### 临时消息

临时消息具有以下特性: 
- 只能发送到文字频道中
- 可以指定仅目标用户可看见
- 临时消息会在 KOOK 客户端的消息缓存刷新后消失(最快的验证方法就是重启客户端)
- 无法更新临时消息(但是可以更新非临时消息为临时消息，刷新后会变回原来的消息)

至于如何发送临时消息，上述的方法中，一般在方法名后面加上**Temp**就是对于方法的临时消息版本，如:
`TextChannel#sendCompoentTemp(component)`.


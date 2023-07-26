## 消息概述

消息是由 KOOK 用户发送的，包含了一些内容的实体。

**消息也是一种实体。**
但它没有放在 `snw.jkook.entity` 包下，原因是因为[ZX夏夜之风](https://github.com/SNWCreations)在开发JKook的时候，觉得诸如`snw.jkook.entity.message.component.card.structure`的包名过长，于是夏夜把它放到了根包下。  
~~虽然还是很长，但聊胜于无。~~

## 总览包结构

<details>
<summary>点击展开</summary>

```text
snw.jkook.message
|   Message
|   PrivateMessage
|   TextChannelMessage
|   
\---component
    |   BaseComponent
    |   FileComponent
    |   MarkdownComponent
    |   TextComponent
    |   
    \---card
        |   CardBuilder
        |   CardComponent
        |   CardScopeElement
        |   MultipleCardComponent
        |   Size
        |   Theme
        |   
        +---element
        |       BaseElement
        |       ButtonElement
        |       ImageElement
        |       InteractElement
        |       MarkdownElement
        |       PlainTextElement
        |       
        +---module
        |       ActionGroupModule
        |       BaseModule
        |       ContainerModule
        |       ContextModule
        |       CountdownModule
        |       DividerModule
        |       FileModule
        |       HeaderModule
        |       ImageGroupModule
        |       InviteModule
        |       package-info
        |       SectionModule
        |       
        \---structure
                BaseStructure
                Paragraph
```

</details>
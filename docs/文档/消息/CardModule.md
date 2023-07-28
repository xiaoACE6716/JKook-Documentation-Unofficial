这里将会给出[卡片消息编辑器](https://www.kookapp.cn/tools/message-builder.html#/card)可用的模块与JKook添加这些模块时候的代码案例

## 内容模块

<!-- tabs:start -->

### **纯文本**
plain-text
```java
//不使用kmarkdown,不使用emoji短码转换
cardBuilder.addModule(new SectionModule("Hello world", false));
//不使用kmarkdown,使用emoji短码转换
cardBuilder.addModule(new SectionModule("Hello world", false, true));
```

### **kmarkdown文本**
kmarkdown
```java
//不使用emoji短码转换
cardBuilder.addModule(new SectionModule("Hello world"));
//使用emoji短码转换
cardBuilder.addModule(new SectionModule("Hello world", true, true));
```

### **多列文本**
paragraph
```java
//Paragraph.Builder(int columns)中columns为列数，最大为3
//Paragraph中可用的元素有MarkdownElement与PlainTextElement

// 你也可以用new Paragraph(Arrays.asList(Some MarkdownElement or PlainTextElement))
// 但是有Builder当然用Builder啦

cardBuilder.addModule(new SectionModule(new Paragraph.Builder(3)
                .addField(new MarkdownElement("01"))
                .addField(new PlainTextElement("02"))
                .addField(new MarkdownElement("03"))
                .build()));
```

### **彩色文本**
实际上彩色文本是KMarkdown的一个语法，然而它只能用于卡片消息里，并不能用到文字消息里，官方也没写到KMarkdown语法文档里。

> 可用的颜色有: **primary**, **success**, **danger**, **warning**, **info**, **secondary**, **body**, **tips**, **pink**, **purple**

!> 在PC、移动端上各颜色显示可能不一样，另外客户端主题也会影响颜色的显示

```java
cardBuilder.addModule(new SectionModule("(font)安全免费(font)[success] (font)没有广告(font)[purple] (font)低资源占用(font)[warning] (font)高通话质量(font)[pink]"));
```

### **文本+图片 与 文本+按钮**

```java
//文本加图片 文本可以用PlainTextElement也可以MarkdownElement
cardBuilder.addModule(new SectionModule(new PlainTextElement("这是文本"),
                new ImageElement("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg",null, Size.LG,true),
                Accessory.Mode.RIGHT));

//文本加按钮 
cardBuilder.addModule(new SectionModule(new MarkdownElement("这是文本"),
                new ButtonElement(Theme.PRIMARY,"点击按钮后返回发给bot的value",ButtonElement.EventType.RETURN_VAL,new PlainTextElement("按钮上的文字")),
                Accessory.Mode.RIGHT));
```

> ImageElement与ButtonElement详细的说明如下: 

<!-- tabs:start -->

### **ImageElement**

`ImageElement`对象的构造参数有: 

String `src`: 图片的链接地址

!> 注意，请用`JKook.getHttpAPI().uploadFile()`上传图片后用返回的链接作为图片链接，因为KOOK为了安全只允许使用KOOK自己的图床。

String `alt`: 鼠标放到图片上的提示文本。~~(实际上毫无作用?)~~

!> 笔者在此的建议是传null进去，因为它目前没有用的同时还可能导致无法通过消息验证。

Size `size`: 图片的大小

> 请使用`Size`枚举中存放的可用的大小设置

boolean `circle`: 图片是否显示为圆形


### **ButtonElement**

`ButtonElement`对象的构造参数有: 

Theme `theme`: 按钮的主题颜色，如同卡片主题颜色一样，但是没法像卡片一样自定义颜色，其中`Theme`枚举中存放了可用的Theme设置。

String `value`:   
如果`EventType`设置的是`ButtonElement.EventType.RETURN_VAL`，点击按钮将会把这个值发送给bot且在`UserClickButtonEvent`中得到处理；  
如果`EventType`设置的是`ButtonElement.EventType.LINK`，点击按钮将会打开设置的链接地址；  
如果`EventType`设置的是`ButtonElement.EventType.NO_ACTION`，点击按钮将不会有任何操作；  

EventType `type`: `value`处已经说明清楚，不再过多复述。

BaseElement `element`: 此处可传入PlainTextElement或MarkdownElement，内容为按钮上显示的文字内容。

<!-- tabs:end -->

!> 注意！文本加图片时Accessory.Mode.可为LEFT或RIGHT，文本加按钮时只能为RIGHT

<!-- tabs:end -->

## 图片模块

<!-- tabs:start -->
### **container**
1到9张图片的组合，与图片组模块不同，多张图片会纵向排列。
```java
// 你也可以用new ContainerModule(Arrays.asList(Some ImageElement))
// 但是有Builder当然用Builder啦
cardBuilder.addModule(new ContainerModule.Builder()
                .add(new ImageElement("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg",null, Size.LG,true))
                .add(new ImageElement("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg",null, Size.LG,true))
                ...
                .build());
```

### **image-group**
1到9张图片的组合，图片呈九宫格显示。
```java
// 你也可以用new ImageGroupModule(Arrays.asList(Some ImageElement))
// 但是有Builder当然用Builder啦
cardBuilder.addModule(new ImageGroupModule.Builder()
                .add(new ImageElement("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg",null, Size.LG,true))
                .add(new ImageElement("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg",null, Size.LG,true))
                ...
                .build());
```

<!-- tabs:end -->

!> 在这两个模块中图片的`"circle": true`都不起作用

## 标题模块
标题模块只能支持展示标准文本，突出标题样式。
```java
cardBuilder.addModule(new HeaderModule("这里是文本内容"));
```

## 分割线模块
展示分割线。
```java
cardBuilder.addModule(DividerModule.INSTANCE);
```

## 交互模块
交互模块中包含交互控件元素，目前有且只有的交互控件为按钮（button）一个交互模块中最多放4个按钮
```java
// 你也可以用new ActionGroupModule(arrays.asList(Some ButtonElement))
// 但是有Builder当然用Builder啦
cardBuilder.addModule(new ActionGroupModule.Builder()
                .add(new ButtonElement(Theme.PRIMARY, "value", ButtonElement.EventType.RETURN_VAL, new PlainTextElement("按钮上的文字")))
                .add(new ButtonElement(Theme.PRIMARY, "value", ButtonElement.EventType.RETURN_VAL, new PlainTextElement("按钮上的文字")))
                ...
                .build());
```
## 备注模块
展示图文混合的内容。

> 此处图片的`"circle": true`起作用

```java
cardBuilder.addModule(new ContextModule.Builder()
                .add(new MarkdownElement("这是文本"))
                .add(new ImageElement("https://img.kaiheila.cn/assets/2021-01/7kr4FkWpLV0ku0ku.jpeg", null, Size.LG, true))
                .add(new MarkdownElement("这是文本"))
                .build());
```

## 文件模块
展示文件，目前有三种，文件，视频和音频。
```java
// 文件
cardBuilder.addModule(new FileModule(FileComponent.Type.FILE,
                "https://img.kaiheila.cn/attachments/2021-01/21/600972b5d0d31.txt",
                "KOOK介绍.txt",
                null));
// 音频
cardBuilder.addModule(new FileModule(FileComponent.Type.FILE,
                "https://img.kaiheila.cn/attachments/2021-01/21/600975671b9ab.mp3",
                "命运交响曲",
                "https://img.kaiheila.cn/assets/2021-01/rcdqa8fAOO0hs0mc.jpg"));
// 视频
cardBuilder.addModule(new FileModule(FileComponent.Type.FILE,
                "https://img.kaiheila.cn/attachments/2021-01/20/6008127e8c8de.mp4",
                "有本事别笑",
                null));
```

## 倒计时模块
展示倒计时。

!> 注意，此处的startTime与endTime均为时间戳

!> 不传startTime默认为从发送卡片那一刻开始

<!-- tabs:start -->
### **常规倒计时**
```java
cardBuilder.addModule(new CountdownModule(CountdownModule.Type.DAY,endTime));
// 或者
cardBuilder.addModule(new CountdownModule(CountdownModule.Type.DAY,startTime,endTime));
```
### **小时倒计时**
```java
cardBuilder.addModule(new CountdownModule(CountdownModule.Type.HOUR,endTime));
// 或者
cardBuilder.addModule(new CountdownModule(CountdownModule.Type.HOUR,startTime,endTime));
```
### **读秒倒计时**
```java
cardBuilder.addModule(new CountdownModule(CountdownModule.Type.SECOND,endTime));
// 或者
cardBuilder.addModule(new CountdownModule(CountdownModule.Type.SECOND,startTime,endTime));
```
<!-- tabs:end -->

## 邀请模块
提供服务器邀请/语音频道邀请。  
该模块没有在卡片编辑器中提供，但是在文档中有说明
```java
// 可以是服务器或者是频道的短码
cardBuilder.addModule(new InviteModule("aecCr6"));
// 也可以是完整的邀请链接
cardBuilder.addModule(new InviteModule("https://kook.top/aecCr6"));

// 搭配createInvite方法(其中3600为过期时间，单位：秒 100为邀请可用次数)
cardBuilder.addModule(new InviteModule(Channel.createInvite(3600, 100)));
cardBuilder.addModule(new InviteModule(Guild.createInvite(3600, 100)));
```
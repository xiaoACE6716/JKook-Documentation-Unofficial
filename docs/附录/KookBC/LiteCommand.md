# 什么是LiteCommand
维护者[huanmeng-qwq](https://github.com/huanmeng-qwq)给KookBC引入的一个命令框架[LiteCommands](https://github.com/Rollczi/LiteCommands)

可以使用框架提供的各个注解来使得命令的编写更加轻松

!> 想要在插件中使用 LiteCommand，请将KookBC作为项目依赖引入  
(因为你没必要打包一份KookBC进入您的插件，所以请将scope设置为provided)

而且在IDEA中安装[LiteCommands](https://plugins.jetbrains.com/plugin/20799-litecommands)插件后，可以自动识别LiteCommands的注解，并能够很好的辅助开发。

## 一个简单的例子

```java
@Command(name = "myFistLiteCommand")
@Description({"一个用LiteCommand编写的命令的例子"})
public class myFistLiteCommand {

    // 此时指令为: /myFistLiteCommand
    @Execute
    String execute(@Context CommandSender sender, @Context Message message) {

        // ...
        return "你使用了/myFistLiteCommand";

    }

    // 子命令 /myFistLiteCommand subCommand <parm1>
    @Execute(name = "subCommand")
    public void subCommand(@Context CommandSender sender, @Context Message message, @Arg("parm1") String parm1) {

        sender.reply("你使用了/myFistLiteCommand subCommand");
        // ...

    }
}

// 不要忘记注册命令
// 在你的插件主类的 onEnable() 中
@Override
public void onEnable() {

    LiteKookFactory.builder(this)
            .commands(new myFistLiteCommand(this))
            .build();
        
}

```



##  简单易用的注解们

 - @Arg 表示必选参数
 - @OptionalArg 表示可选参数，当未提供参数时，该参数将设置`null`为默认值

示例: 
```java
@Command(name = "give")
public class GiveCommand {
    @Execute
    void give(@Arg Player target, @Arg Material type, @OptionalArg int amount) {
        // Command implementation
        if (amount == null) {
            amount = 1;
        }
    }
}
```

- @Flag 用于定义命令方法的标志，标志是修改命令行为的可选参数。
示例:
```java
@Command(name = "mute")
public class MuteCommand {
    @Execute
    public void mute(
        @Arg Player player,
        @Flag("-s") boolean isSilent
    ) {
        // ..
    }
}
```
在示例中，如果在使用命令时输入了参数`-s`，则布尔变量`isSilent`为`true`，否则为`false`。

- @Join 用于将多个参数连接成单个字符串
示例:
```java
@Command(name = "ban")
public class BanCommand {
    @Execute
    public void ban(
        @Arg Player target,
        @Join String reason
    ) {
        // Command implementation
    }
}
```
在示例中，当你输入: `/ban xiaoACE Just a example`  
此时`reason`的结果为: `Just a example`

另外，你可能想要限制参数拼接的数量
```java
// 只会连接两个
@Join(limit = 2)
```
或者你不想用空格作为分隔符
```java
// 此时分隔符为: -
@Join(separator = "-")
```
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

        sender.reply("你使用了/myFistLiteCommand");
        // ...

    }

    // 子命令 /myFistLiteCommand subCommand <parm1>
    @Execute(name = "subCommand")
    public void subCommand(@Context CommandSender sender, @Context Message message, @Arg("parm1") String parm1) {

        sender.reply("你使用了/myFistLiteCommand subCommand");
        // ...

    }
}
```
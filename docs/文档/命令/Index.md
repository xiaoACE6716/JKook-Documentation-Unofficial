# 命令

> 命令是 Bot 和用户的重要交流渠道。  
> 其实所谓命令，只是一种规范化的消息。

## JKookCommand

这是 JKook API 命令系统的核心类。表示一个命令。采用建造者模式。

在 JKook API 命令系统中，一个命令可以拥有以下属性:  
- 名称
- 前缀
- 别称
- 简介
- 帮助信息
- 执行器
- 参数类型 (自 API 0.38 开始)

**JKookCommand**有如下的多种构造方法:  

!> 其中，命令名称、别称、前缀不可以有空格。前缀可以是空字符串，其他两个不能。

```java
public final class JKookCommand {
    
    // 最简单的构造器，只需要一个名称。
    // 前缀此时使用默认值 "/"
    public JKookCommand(String rootName) {
    }

    // 在提供命令名称的同时提供一个 char 作为此命令的前缀。
    // 此时命令的前缀只有给定的 char
    public JKookCommand(String rootName, char prefix) {
    }

    // 与 JKookCommand(String, char) 类似，但是因为第二个参数是 String
    // 所以你可以指定一个无空格的字符串作为命令前缀
    public JKookCommand(String rootName, String prefix) {
    }
    
    // 主构造方法
    // 因为第二个参数是 Collection<String> ，所以你可以提供多个字符串作为命令前缀
    public JKookCommand(String rootName, Collection<String> prefixes) {
    }
    
    // ...
    // 更多方法已忽略
}
```

### 命令前缀

命令前缀有助于将用户的正常发言与命令区分开。  

命令前缀可以通过构造方法指定，也可以通过`JKookCommand#addPrefix`方法添加更多的前缀。

```java
// 构造方法中设置前缀为"."
// 通过addPrefix方法添加更多前缀
new JKookCommand("test", ".")
        .addPrefix("/")
        .addPrefix("#")
    // ...
```

### 命令别称

命令别称可以通过 `JKookCommand#addAlias` 方法添加。  
命令别称的作用正如其名，对命令的另一种称呼，比如:  

```java
new JKookCommand("test01")
        .addAlias("test02")
        // ...
```

以上代码表示的命令既可以通过发送 `/test01` 执行，也可以通过发送 `/test02` 执行。

### 简介 & 帮助信息

简介和帮助信息不同的是，简介应该在 /help 命令 (由 JKook API 的实现提供) 的结果中展示，并且应该尽可能的简短。

帮助信息应该在用户使用 /help 命令的同时指定了此命令的名称 (如 /help eg 即 eg 命令被指定) 时展示。

```java
new JKookCommand("eg")
        .setHelpContent("使用/help eg时展示")
        .setDescription("使用/help 时展示")
```

### 子命令

对于一个命令对象，其可以有无数个不重名的子命令。  
子命令的前缀将被忽略。

对一个命令注册子命令，调用其对象的 `addSubcommand` ，将子命令对象传入即可。

你可以嵌套子命令，如:

```java
new JKookCommand("eg")
        .addSubcommand(
                new JKookCommand("sub")
                        .addSubcommand(
                                new JKookCommand("anothersub")
                                // subcommand code here
                        )
        )
        // more command code
```

调用其中的 `anothersub` 命令只需要执行 `/eg sub anothersub` 即可。

### 注册命令

!> 在你对命令对象完成各项设置后，请务必调用 `JKookCommand#register` 方法！

!> 注意:   
在 API 0.37 中，`register` 方法不需要参数。  
**在 API 0.48 中，`register` 方法需要一个 `Plugin` 作为命令的所有者。**  

!> 命令的属性在注册后不能更改。

```java
// API 0.48前
new JKookCommand("test")
        //...
        .register();
//  API 0.48后      
new JKookCommand("test")
        //...
        .register(Plugin);
```

### 执行器

WIP!

### 参数解析系统

!> 本节的内容需要 JKook API 版本为 0.38+ 。

WIP!

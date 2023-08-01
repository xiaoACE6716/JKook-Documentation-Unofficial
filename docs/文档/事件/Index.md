# 事件
> 在这个世界上，每一分，每一秒，都在发生一些事情，传递这些事情"发生了"这个信息的东西我们称之为事件。
> <div align="right"><a href='https://github.com/SNWCreations'>——ZX夏夜之风</a></div>

例如: 机器人发送了一个带有按钮的卡片消息，而事件可以用来使KOOK用户点击按钮的时候执行一个行为。

一个事件监听器是一个包含一个或者多个 `public void` 成员方法，并且每一个方法都有 `@EventHandler` 注解的类。

# 开始监听事件

## 创建一个事件监听器
首先你需要 `implements Listener` 。其完整限定名为 `snw.jkook.event.Listener` 。  
这是一个例子:
```java
public class MyListener implements Listener {
    @EventHandler
    public void onEvent(UserClickButtonEvent event) { 
        event.getChannel().sendComponent(event.getUser().getName() + "点击了按钮");
    }
}
```
该例子监听了点击按钮事件，当有人点击按钮，机器人就会发送一条消息。

当然，光有监听器类还不够，我们还需要在插件主类里注册监听器。  
这是一个例子:
```java
public class MyPlugin extends BasePlugin {
    @Override
    public void onEnable() {
        getCore().getEventManager().registerHandlers(this, new MyListener());
    }
}
```

!> 注意，监听的事件类型不能是抽象的（即 `abstract` 的）。

## 自定义事件

JKook支持自定义事件！  
编写一个继承 `Event` 的类即可，当你的事件发生时，可通过 `new` 一个事件对象然后通过 `EventManager#callEvent` 方法发布事件。

!> 注意：`callEvent` 方法是同步的。  
这意味着这个方法会在所有监听了你提交的事件的代码返回之后才返回，如果你只需要发布一个事件，而不需要关心后续，可以考虑用任务调度器发布事件，以提升代码性能。

例子将在未来补充
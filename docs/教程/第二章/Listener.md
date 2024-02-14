# 人生的第一个事件监听器

KOOK有着许多的事件，机器人可以监听这些事件来完成各种各样的操作。  
事件列表大全请看[事件列表](文档/事件/EventList.md)。

### 监听器的具体编写方法

要编写一个监听器首先你得在类里实现Listener接口。  
此接口没有任何需要你实现的方法，它自己本就没有定义任何方法。

所以，一个监听器类可以这么写:
```java
public class myListener implements Listener {

}
```

然后在监听器类方法上使用@EventHandler注解，用于标记你的方法是一个用于处理事件的方法。  

```java
public class myListener implements Listener {
    @EventHandler
    public void onEvent(XXXEvent event) { // 将 XXXEvent 替换为事件列表中一种具体的事件
        // code here
    }
}
```

然后在主类的 onEnable() 方法中注册你的监听器。  

!> 写了监听器类一定要记得注册！

```java
public void onEnable() {
    getCore().getEventManager().registerHandlers(this,new myListener());
}
```
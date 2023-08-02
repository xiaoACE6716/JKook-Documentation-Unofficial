# 配置系统

JKook 采用YAML作为`plugin.yml`以及配置文件的格式。

YAML 是以键值对的形式存储数据的。这点和 JSON 很像，也很像 `java.util.Map` 。

如 `foo: bar` 中，foo 是键，bar是值。

以下为一个实例 (注释会解释这些值的类型):
```yml
a: 1 # int
b: 1.1 # double, 也可以是 float
c: # ConfigurationSection
  d: 1.1.1 # String (因为不是一个有效数字), 此配置项的路径是 c.d
e: true # boolean
f: ["a", "b", "c"] # List<String>
```
!> 请注意: YAML 对缩进要求很严格。

在插件中调用 `saveDefaultConfig` 方法，将会从插件的 JAR 包中释放名为 `config.yml` 的文件到插件的数据文件夹中。

!> 请在生命周期`onLoad`中调用`saveDefaultConfig`，此时配置会被加载到内存中，然后走向下一个生命周期`onEnable`。

## 获取值
在插件中调用`getConfig#getXXX(key)`以获取key对应的value。如: 
```java
// 从当前插件的配置中获取 "msg" 键的值并返回。
getConfig.getStr("msg");
```

## 设置值
在插件中调用`setConfig#set(key,value)`方法即可，此处value接受的类型为`Object`。  
如果想删掉一个配置项，`value`处传null即可。
```java
getConfig.set("msg","114514");
```

## 保存配置

如果在程序执行过程中，内存中的配置被修改，请在生命周期`onDisale`中调用`saveConfig`。  
否则修改过的配置不会被保存。
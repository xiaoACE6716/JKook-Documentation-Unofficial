# 📦安装

## 在 JitPack 上使用预编译的库（推荐）
<details>
<summary>点击展开</summary>

> 来到[JitPack](https://jitpack.io/#SNWCreations/JKook)，寻找到你想要的版本，点击按钮**Get it**,你就会拿到你需要添加东西

<!-- tabs:start -->

### **使用Maven**

> 将Jitpack仓库地址添加到`pom.xml`中的`repositories`中，然后将依赖添加到`dependencies`中，这是一个例子: 

```comment
	<repositories>
		<repository>
		    <id>jitpack.io</id>
		    <url>https://jitpack.io</url>
		</repository>
	</repositories>

    <dependencies>
        <dependency>
	        <groupId>com.github.SNWCreations</groupId>
	        <artifactId>JKook</artifactId>
	        <version>Tag</version>
	    </dependency>
    </dependencies>
```

### **使用Gradle**

> 将Jitpack仓库地址添加到`build.gradle`中的`repositories`中，然后将依赖添加到`dependencies`中，这是一个例子: 

```gradle
repositories {
    ...
    maven { url "https://jitpack.io" }
}

dependencies {
    ...
    implementation 'com.github.SNWCreations:JKook:{version}'
}
```

<!-- tabs:end -->
</details>

## 自行编译

<details>
<summary>点击展开</summary>

> JKook 是一个 Java“程序”, 它使用 [Maven 3](https://maven.apache.org) 进行编译.
> 要编译和安装它，您应该执行以下步骤:
> * 安装 Maven 和 Git
> * 克隆此存储库 (`git clone https://github.com/SNWCreations/JKook.git`)
> * `mvn clean install`
> 最后，将编译出来的组件作为依赖项添加到您的项目中。

</details>

!> 如果你使用的是来自 JitPack 的库, 则 `groupId` 为 `com.github.SNWCreations`, `artifactId` 为 `JKook`.  
如果你选择自己编译, 则 `groupId` 为 `snw`, `artifactId` 为 `jkook`.

> 安装完成! 现在可以开始编写代码啦!
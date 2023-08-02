# 服务器

## 分组与频道

`Channel`: 表示一个频道。  
`Category`: 表示一个分组。  

`NonCategoryChannel`: 表示一个不在分组内的频道。  
`TextChannel`与`VoiceChannel`都是它的子类。  

`TextChannel`: 表示一个文字频道。  
`VoiceChannel`: 表示一个语音频道。  

### TextChannel

获取一个文字频道中的历史消息可以使用 `TextChannel#getMessages` 方法。  

对一个文字频道发送消息组件可以使用 `TextChannel#sendComponent` 方法。  

具体用法将在[消息](文档/消息/Index.md)处讲解。

### VoiceChannel

`VoiceChannel#getUsers` 方法可以获取由所有已加入此语音频道的用户组成的列表。  

`VoiceChannel#moveToHere` 方法可以将另一个语音频道中的用户移动到此语音频道。  

`VoiceChannel#getMaxSize` 方法可以获取此语音频道最大可以容纳的用户数。  

## 角色与权限

### 角色

`Role`: 表示一个角色。可以为不同的角色配置不同的权限，以实现权限管理的功能。  

!> 对 `Role` 进行任何操作的前提是你的机器人在角色对应服务器中有角色管理的权限。

可以通过 `User#grantRole` 和 `User#revokeRole` 方法实现用户角色的授予与剥夺。

在一个服务器中新建一个角色？调用 `Guild#createRole` 方法。

获取一个服务器已有的所有角色？调用 `Guild#getRoles` 方法。

你可以通过 `Role#isPermissionSet` 方法检查此角色是否有特定权限。

### 权限

`Permission`: 对一个服务器进行一些操作会需要机器人拥有特定的权限。

> 权限是一个 unsigned int 值，由比特位代表是否拥有对应的权限。
> 
> 权限值与对应比特位进行按位与操作，判断是否拥有该权限。
> 
> <div align="right"><a href='https://developer.kookapp.cn/doc/http/guild-role'>---KOOK 开发者文档</a></div>

## 邀请

`InviteHolder`: 表示一个可创建邀请链接的对象。  
`Guild`与`NonCategoryChannel`都是它的子类，只需调用对象的`createInvite(int validSeconds, int validTimes)`方法，即可创建邀请链接。

```java
// 给服务器创建一个永不过期且无使用次数上限的邀请链接
// validTimes设置为-1时为无使用次数上限，其余设置为多少则邀请链接能用多少次
Guild.createInvite(0,-1);
```
这里给出一个计算好的过期时间列表: 

| 单位：秒   | 过期时间   |
|--------|--------|
| 0      | 永不过期   |
| 1800   | 0.5 小时 |
| 3600   | 1 个小时  |
| 21600  | 6 个小时  |
| 43200  | 12 个小时 |
| 86400  | 1 天    |
| 604800 | 7 天    |


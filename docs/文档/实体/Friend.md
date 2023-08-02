# 好友系统 

> 感谢 [DeeChael](https://github.com/DeeChael) 发掘的好友系统 API 。
> 
>这部分 API 加入于 JKook API 0.49.0 。

你的机器人可以和普通用户成为好友了！

相关方法放在 `HttpAPI` 中，但是因为这些方法与用户联系更为密切，所以我们放在这里来讲。

`HttpAPI#getFriendState` 方法可以让你获取当前机器人账号下的好友列表状态，它只是一个快照，这意味着当你需要最新数据时，你应该调用此方法重新请求数据。

`HttpAPI#addFriend` 方法可以让你向指定用户发出一个好友请求。

`HttpAPI#deleteFriend` 方法可以让你删除一个好友。

`HttpAPI#handleFriendRequest` 方法与 `HttpAPI.FriendRequest#handle` 效果一致，决定是否同意好友请求。
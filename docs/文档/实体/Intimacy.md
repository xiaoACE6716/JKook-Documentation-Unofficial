# 亲密度系统

这是一个KOOK 为机器人设计的用户亲密度系统。

> 机器人可以在应用后台配置默认的初始亲密度和形象。机器人可以根据一些逻辑来更新与该用户的亲密度，从而更新形象展示(注: 包含在社交信息中)。"
> 
> <div align="right"><a href='https://developer.kookapp.cn/doc/http/intimacy'>---KOOK 开发者文档</a></div>

查询用户亲密度的方法为 `User#getIntimacy()`。

查询用户亲密度等级详细内容的方法为 `User#getIntimacyInfo()`。

修改用户亲密度的方法为 `User#setIntimacy()`。

亲密度的有效范围为 0 -- 2200 ，因此，若传递此范围以外的数字，方法将抛出异常。

> 正常亲密度是 0-2000 ，在 1000-2000 的范围中每 100 分为 1 颗红心，0-1000 是负分，显示灰色的裂心。
>
> <div align="right"><a href=''>---不鲲 (KOOK 员工)</a></div>

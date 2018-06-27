``` sequence
Title: Know-Your-Customer
participant  IdentityProvider
participant  Ethereum 
participant  User
participant  PDS/PDC
participant  ServiceProvider 
User-->Ethereum: 注册proxy
IdentityProvider-->Ethereum: 注册proxy
PDS/PDC-->Ethereum: 注册proxy
ServiceProvider-->Ethereum: 注册proxy
PDS/PDC-->ServiceProvider: 公开服务协议
ServiceProvider-->PDS/PDC: 授权信任关系
User-->IdentityProvider: 身份信息认证申请
IdentityProvider-->User: 身份信息规格
Note over User: 编辑身份信息 
User-->PDS/PDC: 身份信息
Note over PDS/PDC: 存储身份信息并提供服务接口 
PDS/PDC-->User: 数据服务接口
User-->Ethereum: 数据服务接口
User-->IdentityProvider: 身份信息
Note over IdentityProvider: 身份信息认证中 
IdentityProvider-->Ethereum: 身份信息Hash上链
User-->ServiceProvider: 通过proxy请求特定服务
ServiceProvider-->Ethereum: 通过proxy查询数据服务接口
Ethereum-->ServiceProvider: 数据服务接口
ServiceProvider-->User: 请求授权数据服务接口
User-->ServiceProvider: 授权信息
ServiceProvider-->PDS/PDC: 授权信息
Note over PDS/PDC: 校验授权信息
PDS/PDC-->Ethereum: 身份信息Hash
Ethereum-->PDS/PDC: 认证信息
Note over PDS/PDC: 校验认证信息
PDS/PDC-->ServiceProvider: 返回用户信息或所需信息的校验结果
Note over ServiceProvider: KYC数据处理
ServiceProvider-->User: 拒绝或提供特定服务
```






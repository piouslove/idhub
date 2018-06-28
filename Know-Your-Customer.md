```sequence
Title: Know-Your-Customer Static Public Data Authentication
participant  IdentityProvider
participant  User
participant  Ethereum
participant  ServiceProvider
User-->IdentityProvider: 请求认证[proxy_address]
IdentityProvider-->User: 身份信息规格[data_schema]
Note over User: 填写身份信息并签名
User-->IdentityProvider: User签名的身份信息[user_sig data]
User-->IdentityProvider: 认证费用[token transaction]
Note over IdentityProvider: 信息认证中
Note over IdentityProvider: key管理分配
IdentityProvider-->User: Idp签名的认证信息[idp_sig data]
User-->Ethereum: 开放的身份信息[idp_sig data]
```

```sequence
Title: Know-Your-Customer Dynamic Data Authentication
participant  IdentityProvider
participant  User
participant  Ethereum
participant  ServiceProvider
User-->IdentityProvider: 请求认证[proxy_address]
IdentityProvider-->User: 身份信息规格[data_schema]
Note over User: 填写身份信息并签名 
User-->IdentityProvider: User签名的身份信息[user_sig data]
Note over IdentityProvider: 信息认证中
Note over IdentityProvider: 开启pds服务接口
IdentityProvider-->User: idp授权开通的pds服务信息[idp_sig pds_url schema]
Note over User: 验证idp授权真实性
User-->Ethereum: pds服务信息[pds_url schema]
```

```sequence
Title: Know-Your-Customer Static Public Data Usecase
participant  IdentityProvider
participant  Ethereum 
participant  User
participant  ServiceProvider

User-->ServiceProvider: 请求服务[proxy_address]
ServiceProvider-->User: KYC数据规格[schema]
Note over User: 选择可以使用的idp
User-->Ethereum: 查询被认证过的Public Data[schema idp_proxy]
Ethereum-->User: 被认证过的Public Data[data idp_sig]
Note over User: 校验Public Data
User-->ServiceProvider: 被认证过的Public Data[data idp_sig]
Note over ServiceProvider: 校验Public Data
ServiceProvider-->User: 已签名的KYC通过信息[sp_sig kyc_info]
User-->ServiceProvider: 提交kyc通过信息获取服务[kyc_info user_sig]
Note over ServiceProvider: 开启服务接口
ServiceProvider->Ethereum: KYC记录[idp_sig data_hash user_sig sp_sig](optional)

```

```sequence
Title: Know-Your-Customer Dynamic Data Usecase
participant  IdentityProvider
participant  Ethereum 
participant  User
participant  ServiceProvider

User-->ServiceProvider: 请求服务[proxy_address]
ServiceProvider-->User: KYC数据规格[schema]
Note over User: 选择可以使用的idp
User-->Ethereum: 查询可以使用的PDS服务接口[schema idp_proxy]
Ethereum-->User: PDS服务接口[pds_url idp_sig]
Note over User: 校验PDS服务接口
User-->IdentityProvider: 获取动态数据认证[schema user_sig]
User-->IdentityProvider: 认证费用[token transaction]
Note over IdentityProvider: 校验用户身份
Note over IdentityProvider: 处理并认证动态数据
IdentityProvider-->User: idp签名的动态数据[dynamic_data idp_sig]
User-->ServiceProvider: user签名的已认证动态数据[user_sig dynamic_data idp_sig]
Note over ServiceProvider: 校验用户身份
Note over ServiceProvider: 校验动态数据
ServiceProvider-->User: sp签名的KYC通过信息[sp_sig kyc_info]
User-->ServiceProvider: 提交kyc通过信息获取服务[kyc_info user_sig]
Note over ServiceProvider: 开启服务接口
ServiceProvider->Ethereum: KYC记录[idp_sig dynamic_data_hash user_sig sp_sig](optional)
```


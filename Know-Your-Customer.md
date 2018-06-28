```sequence
Title: Know-Your-Customer Authentication
participant  IdentityProvider
participant  Ethereum 
participant  User
participant  ServiceProvider
User-->IdentityProvider: 请求认证[proxy_address]
IdentityProvider-->User: 身份信息规格[data_schema]
Note over User: 填写身份信息并签名 
User-->IdentityProvider: 已签名的身份信息[user_sig data]
Note over IdentityProvider: 信息认证中
User-->IdentityProvider: 认证费用[transaction]
IdentityProvider-->Ethereum: 已签名的认证信息[idp_sig data/hash user_sig]
User-->IdentityProvider: 代管费用[transaction]
IdentityProvider-->Ethereum: 服务及数据抵押金[transaction]
Note over IdentityProvider: 开启pds服务接口
IdentityProvider-->Ethereum: 已开通的pds服务接口[idp_sig pds_url user_sig]
```

```sequence
Title: Know-Your-Customer Authorization
participant  IdentityProvider
participant  Ethereum 
participant  User
participant  ServiceProvider
ServiceProvider-->Ethereum: KYC支持的Idp[Idps_list]
User-->ServiceProvider: 请求服务[proxy_address]
ServiceProvider-->User: KYC要求或规格[question/schema]
User-->Ethereum: 查询被支持的Idp[sp_proxy service_name]
Ethereum-->User: KYC所需数据或者pds服务接口[data/hash/pds_url]
User-->IdentityProvider: 已签名的pds服务接口和KYC要求或规格[pds_url question/schema user_sig]
IdentityProvider-->User: 已签名的KYC所需信息[answer/data idp_sig]
Note over User: 校验数据
User-->ServiceProvider: 已签名的KYC所需信息[user_sig answer/data idp_sig]
Note over ServiceProvider: 校验信息
ServiceProvider-->User: 已签名的KYC通过信息[sp_sig kyc_info]
User-->ServiceProvider: 提交kyc通过信息获取服务[kyc_info user_sig]
Note over ServiceProvider: 开启服务接口
ServiceProvider->Ethereum: KYC记录[idp_sig answer/data user_sig sp_sig](optional)
```

```sequence
Title: Know-Your-Customer
participant  IdentityProvider
participant  Ethereum 
participant  User
participant  ServiceProvider
User-->IdentityProvider: 请求认证[proxy_address]
IdentityProvider-->User: 身份信息规格[data_schema]
Note over User: 填写身份信息并签名 
User-->IdentityProvider: 已签名的身份信息[user_sig data]
Note over IdentityProvider: 信息认证中
User-->IdentityProvider: 认证费用[transaction]
IdentityProvider-->Ethereum: 已签名的认证信息[idp_sig data/hash user_sig]
User-->IdentityProvider: 代管费用[transaction]
IdentityProvider-->Ethereum: 服务及数据抵押金[transaction]
Note over IdentityProvider: 开启pds服务接口
IdentityProvider-->Ethereum: 已开通的pds服务接口[idp_sig pds_url user_sig]

ServiceProvider-->IdentityProvider: 合作费用[transaction]
IdentityProvider-->ServiceProvider: 已签名的合作信息[idp_sig sp_sig cooperation]

ServiceProvider-->Ethereum: KYC支持的Idp[Idps_list idp_sigs sp_sig cooperation]
User-->ServiceProvider: 请求服务[proxy_address]
ServiceProvider-->User: KYC要求或规格[question/schema]
User-->Ethereum: 查询被支持的Idp[sp_proxy service_name]
Ethereum-->User: KYC所需数据或者pds服务接口[data/hash/pds_url]
User-->IdentityProvider: 已签名的pds服务接口和KYC要求或规格[pds_url question/schema user_sig]
IdentityProvider-->User: 已签名的KYC所需信息[answer/data idp_sig]
Note over User: 校验数据
User-->ServiceProvider: 已签名的KYC所需信息[user_sig answer/data idp_sig]
Note over ServiceProvider: 校验信息
ServiceProvider-->User: 已签名的KYC通过信息[sp_sig kyc_info]
User-->ServiceProvider: 提交kyc通过信息获取服务[kyc_info user_sig]
Note over ServiceProvider: 开启服务接口
ServiceProvider->Ethereum: KYC记录[idp_sig answer/data user_sig sp_sig](optional)
```


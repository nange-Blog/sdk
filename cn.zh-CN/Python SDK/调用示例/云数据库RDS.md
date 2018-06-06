# 云数据库RDS {#concept_zxw_xjk_zdb .concept}

本示例介绍如何使用阿里云Python SDK调用RDS的CreateDBInstance接口创建一个RDS实例。

阿里云关系型数据库（Relational Database Service，简称RDS）是一种稳定可靠、可弹性伸缩的在线数据库服务。基于阿里云分布式文件系统和高性能存储，RDS 支持MySQL、SQL Server、PostgreSQL和PPAS（Postgre Plus Advanced Server，一种高度兼容 Oracle 的数据库）引擎，并且提供了容灾、备份、恢复、监控和迁移等方面的全套解决方案，彻底解决数据库运维的烦恼。

## 示例代码 {#section_lq5_3kk_zdb .section}

**注：** 运行该示例代码将创建RDS实例，并产生实际费用。

```
from aliyunsdkcore.client import AcsClient
from aliyunsdkrds.request.v20140815 import CreateDBInstanceRequest
# 创建 AcsClient 实例
client = AcsClient(
"<your-access-key-id>",
"<your-access-key-secret>",
"<your-region-id>"
);
request = CreateDBInstanceRequest.CreateDBInstanceRequest()
request.set_Engine("MySQL")
request.set_EngineVersion("5.7")
request.set_DBInstanceClass("mysql.n1.micro.1")
request.set_DBInstanceStorage("20")
request.set_DBInstanceNetType("Intranet")
request.set_SecurityIPList("0.0.0.0/0")
request.set_PayType("Postpaid")
request.set_DBInstanceDescription("MyRds")
request.set_ClientToken("<uuid>")
response = client.do_action_with_exception(request)
print response
```


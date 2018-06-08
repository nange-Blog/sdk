# 云数据库RDS {#concept_zxw_xjk_zdb .concept}

本示例介绍如何使用阿里云C++ SDK调用RDS的CreateDBInstance接口创建一个RDS实例。

阿里云关系型数据库（Relational Database Service，简称RDS）是一种稳定可靠、可弹性伸缩的在线数据库服务。基于阿里云分布式文件系统和高性能存储，RDS 支持MySQL、SQL Server、PostgreSQL和PPAS（Postgre Plus Advanced Server，一种高度兼容 Oracle 的数据库）引擎，并且提供了容灾、备份、恢复、监控和迁移等方面的全套解决方案，彻底解决数据库运维的烦恼。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建RDS实例，并产生实际费用。

```
#include <iostream>
#include <alibabacloud/core/AlibabaCloud.h>
#include <alibabacloud/rds/RdsClient.h>

using namespace AlibabaCloud;
using namespace AlibabaCloud::Rds;

int main(int argc, char** argv)
{
    // 初始化 SDK
    AlibabaCloud::InitializeSdk();

    // 创建客户端实例
    ClientConfiguration configuration("<your-region-id>");
    RdsClient client("<your-access-key-id>", "<your-access-key-secret>", configuration);

    // 创建API请求并设置参数
    Model::CreateDBInstanceRequest request;
    request.setRegionId("cn-hangzhou");
    request.setEngine("MySQL");
    request.setEngineVersion("5.6");
    request.setDBInstanceClass("rds.mys2.small");
    request.setDBInstanceStorage(5);
    request.setDBInstanceNetType("Internet");
    request.setSecurityIPList("11.11.11.11");
    request.setPayType("Postpaid");
    request.setClientToken("ETnLKlblzczshOTUbOCziJZNwHlYBQ");

    // 请求并打印处理结果
    auto outcome = client.createDBInstance(request);
    if(outcome.isSuccess())
        std::cout << "DBInstanceId: " << outcome.result().getDBInstanceId() << std::endl;

    // 关闭 SDK
    AlibabaCloud::ShutdownSdk();
    return 0;
}
```


# 云数据库RDS {#concept_zxw_xjk_zdb .concept}

本示例介绍如何使用阿里云Go SDK调用RDS的CreateDBInstance接口创建一个RDS实例。

阿里云关系型数据库（Relational Database Service，简称RDS）是一种稳定可靠、可弹性伸缩的在线数据库服务。基于阿里云分布式文件系统和高性能存储，RDS 支持MySQL、SQL Server、PostgreSQL和PPAS（Postgre Plus Advanced Server，一种高度兼容 Oracle 的数据库）引擎，并且提供了容灾、备份、恢复、监控和迁移等方面的全套解决方案，彻底解决数据库运维的烦恼。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建RDS实例，并产生实际费用。

```
package main

import (
    "github.com/aliyun/alibaba-cloud-sdk-go/services/rds"
    "github.com/aliyun/alibaba-cloud-sdk-go/sdk/utils"
    "fmt"
)

func main() { 
    // 创建client实例
    client, err := rds.NewClientWithAccessKey(
        "<your-region-id>",             // 您的地域ID
        "<your-access-key-id>",         // 您的AccessKey ID
        "<your-access-key-secret>")        // 您的AccessKey Secret
    if err != nil {
        // 异常处理
        panic(err)
    }
    // 创建请求并设置参数
    request := rds.CreateCreateDBInstanceRequest()
    request.Engine = "MySQL"
    request.EngineVersion = "5.7"
    request.DBInstanceClass = "mysql.n1.micro.1"
    request.DBInstanceStorage = "20"
    request.DBInstanceNetType = "Intranet"
    request.SecurityIPList = "0.0.0.0/0"
    request.PayType = "Postpaid"
    request.DBInstanceDescription = "MyRds"
    request.ClientToken = utils.GetUUIDV4() 
    response, err := client.CreateDBInstance(request)
    if err != nil {
        // 异常处理
        panic(err)
    }
    fmt.Printf("success(%d)! DBInstanceId = %s\n", response.GetHttpStatus(), response.DBInstanceId)
}
```


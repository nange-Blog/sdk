# 云数据库RDS {#concept_zxw_xjk_zdb .concept}

本示例介绍如何使用阿里云.NET SDK调用RDS的CreateDBInstance接口创建一个RDS实例。

阿里云关系型数据库（Relational Database Service，简称RDS）是一种稳定可靠、可弹性伸缩的在线数据库服务。基于阿里云分布式文件系统和高性能存储，RDS 支持MySQL、SQL Server、PostgreSQL和PPAS（Postgre Plus Advanced Server，一种高度兼容 Oracle 的数据库）引擎，并且提供了容灾、备份、恢复、监控和迁移等方面的全套解决方案，彻底解决数据库运维的烦恼。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建RDS实例，并产生实际费用。

```
import C#.util.UUID;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.rds.model.v20140815.CreateDBInstanceRequest;
import com.aliyuncs.rds.model.v20140815.CreateDBInstanceResponse;
public class Demo {
    public static void main(String[] args) {

        // 创建DefaultAcsClient实例并初始化
        DefaultProfile profile = DefaultProfile.getProfile(
            "<your-region-id>",                     // 您的可用区ID
            "<your-access-key-id>",             // 您的AccessKey ID
            "<your-access-key-secret>");        // 您的AccessKey Secret
        IAcsClient client = new DefaultAcsClient(profile);
        // 创建API请求并设置参数

        CreateDBInstanceRequest request = new CreateDBInstanceRequest();
        request.setEngine("MySQL");
        request.setEngineVersion("5.7");
        request.setDBInstanceClass("mysql.n1.micro.1");
        request.setDBInstanceStorage(20);
        request.setDBInstanceNetType("Intranet");
        request.setSecurityIPList("0.0.0.0/0");
        request.setPayType("Postpaid");
        request.setDBInstanceDescription("MyRds");
        request.setClientToken(UUID.randomUUID().toString());

        // 发起请求并处理应答或异常
        CreateDBInstanceResponse response;
        try {
            response = client.getAcsResponse(request);
            String dbInstanceId = response.getDBInstanceId();
            System.out.println("Create dbInstance success, instanceId = " + dbInstanceId);
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            e.printStackTrace();
        }
    }
}
```


# 云服务器ECS {#concept_zxw_xjk_zdb .concept}

本示例介绍如何使用阿里云Python SDK调用ECS的CreateInstance接口创建一个ECS实例。

云服务器（Elastic Compute Service，简称ECS）是阿里云提供的一种基础云计算服务。使用云服务器ECS就像使用水、电、煤气等资源一样便捷、高效。您无需提前采购硬件设备，而是根据业务需要，随时创建所需数量的云服务器实例。如果不再需要云服务器，也可以方便的释放资源，节省费用。

在创建ECS实例前，您需要获取以下信息：

-   镜像 ID

    调用DescribeImages接口查看要使用的镜像 ID。

-   实例规格

    查看ECS实例规格族选择要创建的ECS实例的规格。


## 示例代码 {#section_lq5_3kk_zdb .section}

**注：** 运行该示例代码将创建ECS实例，并产生实际费用。

```
from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkecs.request.v20140526 import CreateInstanceRequest
# 创建 AcsClient 实例
client = AcsClient(
   "<your-access-key-id>",
   "<your-access-key-secret>",
   "<your-region-id>"
);
# 创建 request，并设置参数
request = CreateInstanceRequest.CreateInstanceRequest()
request.set_ImageId("alinux_17_01_64_20G_cloudinit_20171222.vhd")
request.set_InstanceName("MyInstance")
request.set_SecurityGroupId("<your-security-group-id>")
request.set_InstanceType("ecs.t1.small")
request.set_ClientToken("<uuid>")
# 发起 API 请求并打印返回
response = client.do_action_with_exception(request)
print response
```


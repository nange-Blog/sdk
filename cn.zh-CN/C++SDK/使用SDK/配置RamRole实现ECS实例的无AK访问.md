# 配置RamRole实现ECS实例的无AK访问 {#concept_ewz_h3k_zdb .concept}

为了提高应用部署的安全性的同时提升便利性，阿里云SDK支持通过[实例元数据](../cn.zh-CN/用户指南/实例/实例自定义/元数据/实例元数据.md#)服务来获取ECS RAM角色的授权信息来访问阿里云资源和服务。使用这种方式，您部署在ECS上的应用程序，无需在SDK上配置授权信息即可访问阿里云API（即不需要配置AccessKey）。通过这种方式授权的SDK，可以拥有这个ECS RAM角色的权限。

**说明：** 确保ECS实例已经配置了RAM角色。

## 示例 {#section_th2_n3k_zdb .section}

```
#include <iostream>
#include <alibabacloud/core/AlibabaCloud.h>
#include <alibabacloud/core/InstanceProfileCredentialsProvider.h>
#include <alibabacloud/ecs/EcsClient.h>

using namespace AlibabaCloud;
using namespace AlibabaCloud::Ecs;
int main(int argc, char** argv)
{
    // 初始化 SDK
    AlibabaCloud::InitializeSdk();
    ClientConfiguration configuration("<your-region-id>");
    EcsClient client(std::make_shared<InstanceProfileCredentialsProvider>("<your-role-name>"), configuration);

    // 创建API请求并设置参数
    Model::DescribeInstancesRequest request;
    request.setPageSize(10);
    auto outcome = client.describeInstances(request);
    if (!outcome.isSuccess())
    {
        // 异常处理
        std::cout << outcome.error().errorCode() << std::endl;
        AlibabaCloud::ShutdownSdk();
        return -1;
    }
    std::cout << "totalCount: " << outcome.result().getTotalCount() << std::endl;

    // 关闭 SDK
    AlibabaCloud::ShutdownSdk();
    return 0;
}
```

其中：

-   role-name是与ECS实例关联的RAM角色名称。

-   region-id是您正在使用的地域的ID，你可以通过调用DescribeRegions接口查看地域ID。

**说明：** 示例中的region-id是目标服务\(RAM角色有访问权限\)的API所在地域，不一定等于这个ECS实例的地域。



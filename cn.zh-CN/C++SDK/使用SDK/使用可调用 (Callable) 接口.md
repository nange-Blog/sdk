# 使用可调用 \(Callable\) 接口 {#concept_pfp_plm_zdb .concept}

阿里云C++ SDK为您提供了可调用\(Callable\)接口，以满足您的灵活性需求。某个请求动作的可调用接口通常为：请求动作+Callable，如 `describeInstancesCallable`。

以下代码展示了如何调用`DescribeInstances`的可调用\(Callable\)接口获取指定地域所有ECS实例的详细信息。

```
#include <iostream>
#include <alibabacloud/core/AlibabaCloud.h>
#include <alibabacloud/ecs/EcsClient.h>

using namespace AlibabaCloud;
using namespace AlibabaCloud::Ecs;

int main(int argc, char** argv)
{
    // 初始化SDK
    AlibabaCloud::InitializeSdk();
    // 配置ECS实例
    ClientConfiguration configuration("<your-region-id>");
    EcsClient client("<your-access-key-id>", "<your-access-key-secret>", configuration);
    // 创建API请求并设置参数
    Model::DescribeInstancesRequest request;
    request.setPageSize(10);
    auto call = client.describeInstancesCallable(request);
    auto outcome = call.get();
    if (!outcome.isSuccess())
    {
        // 异常处理
        std::cout << outcome.error().errorCode() << std::endl;
        AlibabaCloud::ShutdownSdk();
        return -1;
    }
    std::cout << "totalCount: " << outcome.result().getTotalCount() << std::endl;
    // 关闭SDK
    AlibabaCloud::ShutdownSdk();
    return 0;
}
```


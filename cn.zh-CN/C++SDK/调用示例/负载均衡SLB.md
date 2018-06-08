# 负载均衡SLB {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云C++ SDK调用SLB的CreateLoadBalancer接口创建一个SLB实例。

负载均衡（Server Load Balancer）是将访问流量根据转发策略分发到后端多台云服务器（ECS实例）的流量分发控制服务。负载均衡扩展了应用的服务能力，增强了应用的可用性。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建SLB实例，并产生实际费用。

```
#include <iostream>
#include <alibabacloud/core/AlibabaCloud.h>
#include <alibabacloud/slb/SlbClient.h>

using namespace AlibabaCloud;
using namespace AlibabaCloud::Slb;

int main(int argc, char** argv)
{
    // 初始化SDK
    AlibabaCloud::InitializeSdk();
	
    // 创建客户端实例
    ClientConfiguration configuration("<your-region-id>");
    SlbClient client("<your-access-key-id>", "<your-access-key-secret>", configuration);
	
    // 创建API请求并设置参数
    Model::CreateLoadBalancerRequest request;
    request.setLoadBalancerName("my-sample-slb");
    request.setAddressType("internet");
    request.setInternetChargeType("paybytraffic");
	
    // 请求并打印处理结果
    auto outcome = client.createLoadBalancer(request);
    if(outcome.isSuccess())
        std::cout << "LoadBalancerId: " << outcome.result().getLoadBalancerId() << std::endl;
		
    // 关闭SDK
    AlibabaCloud::ShutdownSdk();
    return 0;
}
```


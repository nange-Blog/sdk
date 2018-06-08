# 负载均衡SLB {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云Go SDK调用SLB的CreateLoadBalancer接口创建一个SLB实例。

负载均衡（Server Load Balancer）是将访问流量根据转发策略分发到后端多台云服务器（ECS实例）的流量分发控制服务。负载均衡扩展了应用的服务能力，增强了应用的可用性。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建SLB实例，并产生实际费用。

```
package main

import (
    "github.com/aliyun/alibaba-cloud-sdk-go/services/slb"
    "github.com/aliyun/alibaba-cloud-sdk-go/sdk/utils"
    "fmt"
)

func main() { 
    // 创建slbClient实例
    client, err := slb.NewClientWithAccessKey(
        "<your-region-id>",             // 您的地域ID
        "<your-access-key-id>",         // 您的AccessKey ID
        "<your-access-key-secret>")        // 您的AccessKey Secret
    if err != nil {
        // 异常处理
        panic(err)
    }
    // 创建请求并设置参数
    request := slb.CreateCreateLoadBalancerRequest()
    request.LoadBalancerName = "MyLoadBalancer"
    request.AddressType = "internet"
    request.ClientToken = utils.GetUUIDV4() 
    response, err := client.CreateLoadBalancer(request)    
    if err != nil {
        // 异常处理
        panic(err)
    }
    fmt.Printf("success(%d)! loadBalancerId = %s\n", response.GetHttpStatus(), response.LoadBalancerId)
}
```


# 负载均衡SLB {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云Python SDK调用SLB的CreateLoadBalancer接口创建一个SLB实例。

负载均衡（Server Load Balancer）是将访问流量根据转发策略分发到后端多台云服务器（ECS实例）的流量分发控制服务。负载均衡扩展了应用的服务能力，增强了应用的可用性。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建SLB实例，并产生实际费用。

```
from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkslb.request.v20140515 import CreateLoadBalancerRequest
# 创建 AcsClient 实例
client = AcsClient(
   "<your-access-key-id>",
   "<your-access-key-secret>",
   "<your-region-id>"
);
# 创建负载均衡实例
request = CreateLoadBalancerRequest.CreateLoadBalancerRequest()
request.set_LoadBalancerName('MyLoadBalancer')
request.set_AddressType('internet')
request.set_InternetChargeType('paybytraffic')
response = client.do_action_with_exception(request)
print response
```


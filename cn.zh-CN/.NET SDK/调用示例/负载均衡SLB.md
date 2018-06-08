# 负载均衡SLB {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云.NET SDK调用SLB的CreateLoadBalancer接口创建一个SLB实例。

负载均衡（Server Load Balancer）是将访问流量根据转发策略分发到后端多台云服务器（ECS实例）的流量分发控制服务。负载均衡扩展了应用的服务能力，增强了应用的可用性。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建SLB实例，并产生实际费用。

```
using System;
using Aliyun.Acs.Core;
using Aliyun.Acs.Core.Profile;
using Aliyun.Acs.Core.Exceptions;
using Aliyun.Acs.Slb.Model.V20140515;

class Sample
{
    static void Main(string[] args)
    {
        // 创建客户端实例
        IClientProfile clientProfile = DefaultProfile.GetProfile("<your-region-id>", "<your-access-key-id>", "<your-access-key-secret>");
        DefaultAcsClient client = new DefaultAcsClient(clientProfile);
		
        try
        {
            // 创建API请求并设置参数
            CreateLoadBalancerRequest request = new CreateLoadBalancerRequest();
            request.LoadBalancerName = "my-sample-slb";
            request.AddressType = "internet";
            request.InternetChargeType = "paybytraffic
			
            // 请求并打印处理结果
            CreateLoadBalancerResponse response = client.GetAcsResponse(request);
            Console.WriteLine("LoadBalancerId: {0}", response.LoadBalancerId);
        }
        catch (ServerException e)
        {
            Console.WriteLine(e.ErrorCode);
            Console.WriteLine(e.ErrorMessage);
        }
        catch (ClientException e)
        {
            Console.WriteLine(e.ErrorCode);
            Console.WriteLine(e.ErrorMessage);
        }
    }
}
```


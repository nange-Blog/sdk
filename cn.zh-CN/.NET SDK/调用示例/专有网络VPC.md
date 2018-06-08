# 专有网络VPC {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云.NET SDK调用VPC的CreateVpc接口创建一个VPC。

专有网络VPC（Virtual Private Cloud）是用户基于阿里云创建的自定义私有网络, 不同的专有网络之间二层逻辑隔离，用户可以在自己创建的专有网络内创建和管理云产品实例，比如ECS、负载均衡、RDS等。

## 示例代码 {#section_lq5_3kk_zdb .section}

```
using System;
using Aliyun.Acs.Core;
using Aliyun.Acs.Core.Profile;
using Aliyun.Acs.Core.Exceptions;
using Aliyun.Acs.Vpc.Model.V20160428;

class Sample
{
    static void Main(string[] args)
    {
        // 创建客户端实例
        IClientProfile clientProfile = DefaultProfile.GetProfile("<your-region-id>", "<your-access-key-id>", "<your-access-key-secret>");
        DefaultAcsClient client = new DefaultAcsClient(clientProfile);
        try
        {
            // 创建并发起CreateVpcRequest请求
            CreateVpcRequest createRequest = new CreateVpcRequest();
            CreateVpcResponse createResponse = client.GetAcsResponse(createRequest);
			
            // 创建并发起DescribeVpcAttributeRequest请求
            DescribeVpcAttributeRequest describeRequest = new DescribeVpcAttributeRequest();
            describeRequest.VpcId = createResponse.VpcId;
            DescribeVpcAttributeResponse describeResponse = client.GetAcsResponse(describeRequest);
            Console.WriteLine("vpcId: {0}", describeResponse.VpcId);
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


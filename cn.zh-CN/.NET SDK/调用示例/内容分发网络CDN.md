# 内容分发网络CDN {#concept_sfl_3rm_zdb .concept}

本示例介绍如何使用阿里云,NET SDK调用CDN的AddCdnDomainRequest接口添加加速域名。

内容分发网络（Content Delivery Network，简称CDN）是建立并覆盖在承载网之上、由分布在不同区域的边缘节点服务器群组成的分布式网络。

在调用该接口时，注意：

-   创建加速域名之前, 必须先开通CDN服务。

-   加速域名必须已备案完成。

-   源站内容如果不在阿里云平台上，需要进行审核，审核工作会在下一工作日前完成。


```
using System;
using Aliyun.Acs.Core;
using Aliyun.Acs.Core.Profile;
using Aliyun.Acs.Core.Exceptions;
using Aliyun.Acs.Cdn.Model.V20141111;

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
            AddCdnDomainRequest request = new AddCdnDomainRequest();
            request.CdnType = "web";
            request.DomainName = "test.com";
            request.Sources = "test.com";
            request.SourceType = "domain";
			
            // 发起请求
            AddCdnDomainResponse response = client.GetAcsResponse(request);
            Console.WriteLine("Success");
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


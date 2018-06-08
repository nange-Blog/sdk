# 内容分发网络CDN {#concept_sfl_3rm_zdb .concept}

本示例介绍如何使用阿里云C++SDK调用CDN的AddCdnDomainRequest接口添加加速域名。

内容分发网络（Content Delivery Network，简称CDN）是建立并覆盖在承载网之上、由分布在不同区域的边缘节点服务器群组成的分布式网络。

在调用该接口时，注意：

-   创建加速域名之前, 必须先开通CDN服务。

-   加速域名必须已备案完成。

-   源站内容如果不在阿里云平台上，需要进行审核，审核工作会在下一工作日前完成。


```
#include <iostream>
#include <alibabacloud/core/AlibabaCloud.h>
#include <alibabacloud/cdn/CdnClient.h>

using namespace AlibabaCloud;
using namespace AlibabaCloud::Cdn;

int main(int argc, char** argv)
{
    // 初始化 SDK
    AlibabaCloud::InitializeSdk();
	
    // 创建客户端实例
    ClientConfiguration configuration("<your-region-id>");
    CdnClient client("<your-access-key-id>", "<your-access-key-secret>", configuration);
	
    // 创建API请求并设置参数
    Model::AddCdnDomainRequest request;
    request.setCdnType("web");
    request.setDomainName("test.com");
    request.setSources("test.com");
    request.setSourceType("domain");
	
    // 发起请求
    auto outcome = client.addCdnDomain(request);
    if(outcome.isSuccess())
        std::cout << "Success" << std::endl;
		
    // 关闭 SDK
    AlibabaCloud::ShutdownSdk();
    return 0;
}
```


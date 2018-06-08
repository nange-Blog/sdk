# 专有网络VPC {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云C++ SDK调用VPC的CreateVpc接口创建一个VPC。

专有网络VPC（Virtual Private Cloud）是用户基于阿里云创建的自定义私有网络, 不同的专有网络之间二层逻辑隔离，用户可以在自己创建的专有网络内创建和管理云产品实例，比如ECS、负载均衡、RDS等。

## 示例代码 {#section_lq5_3kk_zdb .section}

```
#include <iostream>
#include <alibabacloud/core/AlibabaCloud.h>
#include <alibabacloud/vpc/VpcClient.h>

using namespace AlibabaCloud;
using namespace AlibabaCloud::Vpc;

int main(int argc, char** argv)
{

    // 初始化 SDK
    AlibabaCloud::InitializeSdk();
	
    // 创建客户端实例
    ClientConfiguration configuration("<your-region-id>");
    VpcClient client("<your-access-key-id>", "<your-access-key-secret>", configuration);
	
    // 创建并发起CreateVpcRequest请求
    Model::CreateVpcRequest createRequest;
    auto createOutcome = client.createVpc(createRequest);
    if (createOutcome.isSuccess())
    {
        std::string vpcId = createOutcome.result().getVpcId();
		
        // 创建并发起DescribeVpcAttributeRequest请求
        Model::DescribeVpcAttributeRequest describeRequest;
        describeRequest.setVpcId(vpcId);
        auto describeOutcome = client.describeVpcAttribute(describeRequest);
        if (describeOutcome.isSuccess())
            std::cout << "vpcId:" << vpcId << std::endl;
    }
	
    // 关闭 SDK
    AlibabaCloud::ShutdownSdk();
    return 0;
}
```


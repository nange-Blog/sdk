# 专有网络VPC {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云Go SDK调用VPC的CreateVpc接口创建一个VPC。

专有网络VPC（Virtual Private Cloud）是用户基于阿里云创建的自定义私有网络, 不同的专有网络之间二层逻辑隔离，用户可以在自己创建的专有网络内创建和管理云产品实例，比如ECS、负载均衡、RDS等。

## 示例代码 {#section_lq5_3kk_zdb .section}

```
package main

import (
    "github.com/aliyun/alibaba-cloud-sdk-go/services/vpc"
    "github.com/aliyun/alibaba-cloud-sdk-go/sdk/utils"
    "fmt"
)

func main() { 
    // 创建client实例
    client, err := vpc.NewClientWithAccessKey(
        "<your-region-id>",             // 您的地域ID
        "<your-access-key-id>",         // 您的AccessKey ID
        "<your-access-key-secret>")        // 您的AccessKey Secret
    if err != nil {
        // 异常处理
        panic(err)
    }
    // 创建请求并设置参数
    request := vpc.CreateCreateVpcRequest()
    request.VpcName = "MyVpc"
    request.CidrBlock = "192.168.0.0/16"
    request.ClientToken = utils.GetUUIDV4()
    response, err := client.CreateVpc(request)
    if err != nil {
        // 异常处理
        panic(err)
    }
    fmt.Printf("success(%d)! vpcId = %s\n", response.GetHttpStatus(), response.VpcId)
}
```


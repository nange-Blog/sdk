# 专有网络VPC {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云Python SDK调用VPC的CreateVpc接口创建一个VPC。

专有网络VPC（Virtual Private Cloud）是用户基于阿里云创建的自定义私有网络, 不同的专有网络之间二层逻辑隔离，用户可以在自己创建的专有网络内创建和管理云产品实例，比如ECS、负载均衡、RDS等。

## 示例代码 {#section_lq5_3kk_zdb .section}

```
import json
from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkvpc.request.v20160428 import CreateVpcRequest
from aliyunsdkvpc.request.v20160428 import DescribeVpcAttributeRequest
# 创建 AcsClient 实例
client = AcsClient(
   "<your-access-key-id>",
   "<your-access-key-secret>",
   "<your-region-id>"
);
# 创建 VPC
request = CreateVpcRequest.CreateVpcRequest()
response = client.do_action_with_exception(request)
vpc_id = json.loads(response)['VpcId']
print "VPC ID is", vpc_id
# 获取并打印 VPC 的属性信息
request = DescribeVpcAttributeRequest.DescribeVpcAttributeRequest()
request.set_VpcId(vpc_id)
response = client.do_action_with_exception(request)
print response
```


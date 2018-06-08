# 专有网络VPC {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云Java SDK调用VPC的CreateVpc接口创建一个VPC。

专有网络VPC（Virtual Private Cloud）是用户基于阿里云创建的自定义私有网络, 不同的专有网络之间二层逻辑隔离，用户可以在自己创建的专有网络内创建和管理云产品实例，比如ECS、负载均衡、RDS等。

## 示例代码 {#section_lq5_3kk_zdb .section}

```
import java.util.UUID;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.vpc.model.v20160428.CreateVpcRequest;
import com.aliyuncs.vpc.model.v20160428.CreateVpcResponse;
public class Demo {
    public static void main(String[] args) {
        // 创建DefaultAcsClient实例并初始化
        DefaultProfile profile = DefaultProfile.getProfile(
            "<your-region-id>",                 // 您的可用区ID
            "<your-access-key-id>",         // 您的AccessKey ID
            "<your-access-key-secret>");    // 您的AccessKey Secret
        IAcsClient client = new DefaultAcsClient(profile);
        // 创建API请求并设置参数
        CreateVpcRequest request = new CreateVpcRequest();
        request.setVpcName("MyVpc");
        request.setCidrBlock("192.168.0.0/16");
        request.setClientToken(UUID.randomUUID().toString());
        // 发起请求并处理应答或异常
        CreateVpcResponse response;
        try {
            response = client.getAcsResponse(request);
            String vpcId = response.getVpcId();
            System.out.println("Create vpc success, vpcId = " + vpcId);
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            e.printStackTrace();
        }
    }
}
```


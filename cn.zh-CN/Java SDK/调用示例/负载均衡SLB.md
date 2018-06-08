# 负载均衡SLB {#concept_swc_2lk_zdb .concept}

本示例介绍如何使用阿里云Java SDK调用SLB的CreateLoadBalancer接口创建一个SLB实例。

负载均衡（Server Load Balancer）是将访问流量根据转发策略分发到后端多台云服务器（ECS实例）的流量分发控制服务。负载均衡扩展了应用的服务能力，增强了应用的可用性。

## 示例代码 {#section_lq5_3kk_zdb .section}

**说明：** 运行该示例代码将创建SLB实例，并产生实际费用。

```
import java.util.UUID;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.slb.model.v20140515.CreateLoadBalancerRequest;
import com.aliyuncs.slb.model.v20140515.CreateLoadBalancerResponse;
public class Demo {
    public static void main(String[] args) {
        // 创建DefaultAcsClient实例并初始化
        DefaultProfile profile = DefaultProfile.getProfile(
            "<your-region-id>",                     // 您的可用区ID
            "<your-access-key-id>",             // 您的AccessKey ID
            "<your-access-key-secret>");        // 您的AccessKey Secret        
        IAcsClient client = new DefaultAcsClient(profile);
        // 创建API请求并设置参数
        CreateLoadBalancerRequest request = new CreateLoadBalancerRequest();
        request.setLoadBalancerName("MyLoadBalancer");
        request.setAddressType("internet");
        request.setClientToken(UUID.randomUUID().toString());
        // 发起请求并处理应答或异常
        CreateLoadBalancerResponse response;
        try {
            response = client.getAcsResponse(request);
            String loadBalancerId = response.getLoadBalancerId();
            System.out.println("Create loadBalancer success, loadBalancerId = " + loadBalancerId);
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            e.printStackTrace();
        }
    }
}
```


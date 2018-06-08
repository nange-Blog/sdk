# 配置RamRole实现ECS实例的无AK访问 {#concept_ewz_h3k_zdb .concept}

为了提高应用部署的安全性的同时提升便利性，阿里云SDK支持通过[实例元数据](../cn.zh-CN/用户指南/实例/实例自定义/元数据/实例元数据.md#)服务来获取ECS RAM角色的授权信息来访问阿里云资源和服务。使用这种方式，您部署在ECS上的应用程序，无需在SDK上配置授权信息即可访问阿里云API（即不需要配置AccessKey）。通过这种方式授权的SDK，可以拥有这个ECS RAM角色的权限。

**说明：** 确保ECS实例已经配置了RAM角色。

## 示例 {#section_th2_n3k_zdb .section}

-   不使用自定义配置：

    ```
    // 如果您不需要自定义config，我们提供了一个快捷入口来构建client
    client, err = ecs.NewClientWithEcsRamRole("region-id", "role-name")
    ```

-   使用自定义配置：

    ```
    // 如果您需要自定义config，您可以使用下列代码来构建client
    config := sdk.NewConfig().WithEnableAsync(true)
    // 创建credential对象
    credential := credentials.NewEcsRamRoleCredential("role-name")
    // 初始化client
    client, err := ecs.NewClientWithOptions("region-id", config, credential)
    ```


其中：

-   role-name是与ECS实例关联的RAM角色名称。

-   region-id是您正在使用的地域的ID，你可以通过调用DescribeRegions接口查看地域ID。

**说明：** 示例中的region-id是目标服务\(RAM角色有访问权限\)的API所在地域，不一定等于这个ECS实例的地域。



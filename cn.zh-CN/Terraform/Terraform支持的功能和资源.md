# Terraform支持的功能和资源

资源编排服务ROS（Resource Orchestration Service）为Terraform提供了托管的能力，本文为您介绍Terraform对ROS功能和资源的支持情况。

ROS当前支持的Terraform版本和Provider版本如下表所示。

|Terraform版本|Provider版本|
|-----------|----------|
|0.12.28|-   alicloud：1.121.2
-   aws：3.37.0
-   azurerm：2.56.0 |
|0.15.3|-   alicloud：1.123.0
-   aws：3.42.0
-   azurerm：2.59.0 |

**说明：** ROS会持续更新支持的Terraform版本和Provider版本。

## ROS控制台功能支持情况

|功能|说明|
|--|--|
|资源栈|-   支持预览、创建、更新、删除、查询资源栈。
-   支持查询资源、事件、输出、模板。
-   支持超时时间（10~120分钟）、状态通知、删除保护、删除保留所有资源、标签管理。
-   不支持参数设置、失败回滚、资源栈策略、RAM角色、删除保留部分资源、替换更新、更改集、失败继续创建、取消更新、偏差检测、信号通知、资源导入、风险检查。

**说明：** Terraform不支持通过ROS控制台进行参数设置，建议您直接在`.tf`文件里定义参数。 |
|模板|-   支持创建、更新、删除、查询、校验模板。
-   不支持对模板中涉及的收费资源进行询价。 |
|其他|不支持资源栈组、资源类型查询、STS（Security Token Service）。|

## ROS API支持情况

|功能|说明|
|--|--|
|资源栈|支持PreviewStack、CreateStack、UpdateStack、DeleteStack、GetStack、ListStacks、ListStackResources、GetStackResource、ListStackEvents和SetDeletionProtection。**说明：** GetStack和ListStacks中StackType取值为Terraform时，说明资源栈类型是Terraform。 |
|模板|支持CreateTemplate、UpdateTemplate、DeleteTemplate、GetTemplate、ListTemplates和ValidateTemplate。|
|标签|支持TagResources、UntagResources、ListTagKeys、ListTagValues和ListTagResources。|

## ROS资源支持情况

在ROS中，Terraform支持的资源如下：

-   [阿里云资源](https://registry.terraform.io/providers/aliyun/alicloud/latest/docs)

    **说明：**

    -   支持[Terraform在线调试工具](https://api.aliyun.com/#/cli?tool=Terraform)。
    -   ROS提供了一个默认的Provider，使用当前账号的临时AccessKey以及资源栈所属的地域ID。
-   [AWS资源](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
-   [Azure资源](https://www.terraform.io/docs/providers/azurerm/index.html)


# ROS features and resources supported by Terraform

Resource Orchestration Service \(ROS\) allows you to manage resources by using Terraform. This topic describes the ROS features and resources supported by Terraform.

The following table lists current Terraform and provider versions supported by ROS.

|Terraform version|Provider version|
|-----------------|----------------|
|0.12.28|-   alicloud: 1.121.2
-   aws: 3.37.0
-   azurerm: 2.56.0 |
|0.15.3|-   alicloud: 1.123.0
-   aws: 3.42.0
-   azurerm: 2.59.0 |

**Note:** ROS updates the supported Terraform and provider versions on a regular basis.

## ROS console features supported by Terraform

|Feature|Description|
|-------|-----------|
|Stack|-   You can preview, create, update, delete, and query stacks.
-   You can query resources, events, outputs, and templates.
-   You can configure the timeout period, status notification, deletion protection, and tag management settings. The timeout period can range from 10 minutes to 120 minutes. You can enable deletion protection to retain all resources of a stack when the stack is deleted.
-   You cannot configure template parameters or specify stack parameters such as Rollback on Failure, Stack Policy, and RAM Role. You cannot retain some resources of a stack when the stack is deleted or create a new stack based on the template of the previous stack that fails to be created. You cannot perform replacement update or drift detection, create change sets, cancel the update of a stack, signal the occurrence of an event, import resources, or check for risks.

**Note:** You cannot configure parameters in the ROS console. We recommend that you use a `.tf` file to define parameters. |
|Template|-   You can create, update, delete, query, and validate templates.
-   You cannot query the prices of paid resources in templates. |
|Others|You cannot create stack groups, query resource types, or use Security Token Service \(STS\).|

## ROS API operations supported by Terraform

|Feature|Description|
|-------|-----------|
|Stack|PreviewStack, CreateStack, UpdateStack, DeleteStack, GetStack, ListStacks, ListStackResources, GetStackResource, ListStackEvents, and SetDeletionProtection are supported. **Note:** When Terraform is returned for the StackType parameter in GetStack or ListStacks, Terraform stacks are queried. |
|Template|CreateTemplate, UpdateTemplate, DeleteTemplate, GetTemplate, ListTemplates, and ValidateTemplate are supported.|
|Tag|TagResources, UntagResources, ListTagKeys, ListTagValues, and ListTagResources are supported.|

## ROS resources supported by Terraform

The following resources are supported by Terraform in ROS:

-   [Alibaba Cloud resources](https://registry.terraform.io/providers/aliyun/alicloud/latest/docs)

    **Note:**

    -   Alibaba Cloud Terraform modules are available for online debugging. For more information, see [Alicloud Terraform Modules](https://api.aliyun.com/#/cli?tool=Terraform).
    -   ROS provides a default provider that uses the temporary AccessKey pair of the current account and the region ID of a stack.
-   [AWS resources](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
-   [Azure resources](https://www.terraform.io/docs/providers/azurerm/index.html)


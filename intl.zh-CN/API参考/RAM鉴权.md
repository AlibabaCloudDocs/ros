# RAM鉴权

在RAM用户调用API前，需要阿里云账号通过创建授权策略对RAM用户进行授权。

## 资源授权

默认情况下，RAM用户没有权限通过调用API去创建、修改阿里云资源。RAM用户调用API时，需要先创建一个授权策略，然后将这个授权策略关联给对应的RAM用户以完成资源授权。

在创建授权策略时，您可以通过资源描述符ARN（Alibaba Cloud Resource Name）指定要授权的资源。ARN是阿里云为每个资源定义的一个全局的阿里云资源名称。ARN格式如下：

```
acs:service-name:region:account-id:resource-relative-id
```

ARN字段含义如下：

-   acs：Alibaba Cloud Service的首字母缩写，表示阿里云的公共云平台。
-   service-name：阿里云服务的名称，例如：ECS、OSS、ROS等。
-   region：地域信息。如果不支持该项，可以使用通配符星号（`*`）来代替。

-   account-id：阿里云账号ID，例如：123456789012\*\*\*\*。
-   resource-relative-id：具体的资源描述，不同的阿里云服务的资源描述也不同。更多信息，请参见各阿里云服务的开发文档。

    例如：`acs:oss:123456789012****:sample_bucket/file1.txt`表示OSS服务中对象名称是sample\_bucket/file1.txt的资源，对象的所有者UID为`123456789012****`。


## 可授权的资源编排资源类型

|资源类型|授权策略中的资源描述方法|
|----|------------|
|Stack|acs:ros:$regionid:$accountid:stack/$stackid|
|acs:ros:$regionid:$accountid:stack/\*|
|Template|acs:ros:$regionid:$accountid:template/$templateid|
|acs:ros:$regionid:$accountid:template/\*|
|StackGroup|acs:ros:$regionid:$accountid:stack\_group/\*|

## 可授权的资源编排接口

-   **资源栈相关接口**

    |API|Action|资源描述|
    |---|------|----|
    |PreviewStack|ros:PreviewStack|acs:ros:cn-hangzhou:$accountid:stack/\*|
    |CreateStack|ros:CreateStack|cs:ros:cn-hangzhou:$accountid:stack/\*|
    |ContinueCreateStack|ros:ContinueCreateStack|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |SetDeletionProtection|ros:SetDeletionProtection|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |UpdateStack|ros:UpdateStack|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |CancelUpdateStack|ros:CancelUpdateStack|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |GetStack|ros:GetStack|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |ListStacks|ros:ListStacks|acs:ros:cn-hangzhou:$accountid:stack/\*|
    |ListStackEvents|ros:ListStackEvents|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |ListStackOperationRisks|ros:ListStackOperationRisks|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |DeleteStack|ros:DeleteStack|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |CreateChangeSet|ros:CreateChangeSet|    -   当ChangeSetType取值为CREATE时：acs:ros:cn-hangzhou:$accountid:stack/\*
    -   当ChangeSetType取值为UPDATE时：acs:ros:cn-hangzhou:$accountid:stack/$stackid
    -   当ChangeSetType取值为IMPORT时：acs:ros:cn-hangzhou:$accountid:stack/\* |
    |ExecuteChangeSet|ros:ExecuteChangeSet|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |GetChangeSet|ros:GetChangeSet|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |ListChangeSets|ros:ListChangeSets|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |DeleteChangeSet|ros:DeleteChangeSet|acs:ros:cn-hangzhou:$accountid:stack/$stackid|

-   **资源相关接口**

    |API|Action|资源描述|
    |---|------|----|
    |GetResourceTypeTemplate|ros:GetResourceTypeTemplate|不鉴权|
    |ListStackResources|ros:ListStackResources|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |GetStackResource|ros:GetStackResource|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |GetResourceType|ros:GetResourceType|不鉴权|
    |ListResourceTypes|ros:SetStackPolicy|不鉴权|
    |MoveResourceGroup|ros:MoveResourceGroup|    -   当ResourceType取值为stack时：acs:ros:cn-hangzhou:$accountid:stack/\*
    -   当ResourceType取值为stackgroup时：acs:ros:cn-hangzhou:$accountid:stack\_group/\*
    -   当ResourceType取值为template时：acs:ros:cn-hangzhou:$accountid:template/\* |

-   **资源栈组相关接口**

    |API|Action|资源描述|
    |---|------|----|
    |CreateStackGroup|ros:CreateStackGroup|acs:ros:cn-hangzhou:$accountid:stack\_group/\*|
    |UpdateStackGroup|ros:UpdateStackGroup|acs:ros:cn-hangzhou:$accountid:stack\_group/$stackid|
    |GetStackGroup|ros:GetStackGroup|acs:ros:cn-hangzhou:$accountid:stack\_group/$stackid|
    |ListStackGroups|ros:ListStackGroups|acs:ros:cn-hangzhou:$accountid:stack\_group/\*|
    |DeleteStackGroup|ros:DeleteStackGroup|acs:ros:cn-hangzhou:$accountid:stack\_group/$stackid|
    |CreateStackInstances|ros:CreateStackInstances|acs:ros:cn-hangzhou:$accountid:stack\_instance/\*|
    |UpdateStackInstances|ros:UpdateStackInstances|acs:ros:cn-hangzhou:$accountid:stack\_instance/\*|
    |GetStackInstance|ros:GetStackInstance|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |ListStackInstances|ros:ListStackInstances|acs:ros:cn-hangzhou:$accountid:stack\_instance/\*|
    |DeleteStackInstances|ros:DeleteStackInstances|acs:ros:cn-hangzhou:$accountid:stack\_instance/\*|
    |GetStackGroupOperation|ros:GetStackGroupOperation|acs:ros:cn-hangzhou:$accountid:stack\_group\_operation/\*|
    |ListStackGroupOperations|ros:ListStackGroupOperations|acs:ros:cn-hangzhou:$accountid:stack\_group\_operation/\*|
    |ListStackGroupOperationResults|ros:ListStackGroupOperationResults|acs:ros:cn-hangzhou:$accountid:stack\_group\_operation/\*|
    |StopStackGroupOperation|ros:StopStackGroupOperation|acs:ros:cn-hangzhou:$accountid:stack\_group\_operation/\*|

-   **模板相关接口**

    |API|Action|资源描述|
    |---|------|----|
    |GenerateTemplatePolicy|ros:GenerateTemplatePolicy|acs:ros:cn-hangzhou:$accountid:template/$templateid**说明：** 如果指定参数TemplateId，则需要鉴权。 |
    |CreateTemplate|ros:CreateTemplate|acs:ros:cn-hangzhou:$accountid:template/\*|
    |ValidateTemplate|ros:ValidateTemplate|不鉴权|
    |UpdateTemplate|ros:UpdateTemplate|acs:ros:cn-hangzhou:$accountid:template/$templateid|
    |GetTemplate|ros:GetTemplate|    -   acs:ros:cn-hangzhou:$accountid:stack/$stackid
    -   acs:ros:$regionid:$accountid:stack\_group/\*
    -   acs:ros:cn-hangzhou:$accountid:template/$templateid |
    |GetTemplateEstimateCost|ros:GetTemplateEstimateCost|acs:ros:cn-hangzhou:$accountid:\*|
    |GetTemplateSummary|ros:GetTemplateSummary|acs:ros:cn-hangzhou:$accountid:template/$templateid**说明：** 如果指定参数TemplateId，则需要鉴权。 |
    |ListTemplates|ros:ListTemplates|acs:ros:cn-hangzhou:$accountid:template/\*|
    |ListTemplateVersions|ros:ListTemplateVersions|acs:ros:cn-hangzhou:$accountid:template/$templateid|
    |SetTemplatePermission|ros:SetTemplatePermission|acs:ros:cn-hangzhou:$accountid:\*|
    |DeleteTemplate|ros:DeleteTemplate|acs:ros:cn-hangzhou:$accountid:template/$templateid|

-   **标签相关接口**

    |API|Action|资源描述|
    |---|------|----|
    |ListTagResources|ros:ListTagResources|acs:ros:cn-hangzhou:$accountid:tag/\*|
    |ListTagKeys|ros:ListTagKeys|acs:ros:cn-hangzhou:$accountid:tag/\*|
    |ListTagValues|ros:ListTagValues|acs:ros:cn-hangzhou:$accountid:tag/\*|
    |UntagResources|ros:UntagResources|acs:ros:cn-hangzhou:$accountid:tag/\*|

-   **其他接口**

    |API|Action|资源描述|
    |---|------|----|
    |DescribeRegions|ros:DescribeRegions|不鉴权|
    |SignalResource|ros:SignalResource|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |GetStackPolicy|ros:GetStackPolicy|acs:ros:cn-hangzhou:$accountid:stack/$stackid|
    |SetStackPolicy|ros:SetStackPolicy|acs:ros:cn-hangzhou:$accountid:stack/$stackid|



# GetTemplate

调用GetTemplate接口查询资源栈、资源栈组、更改集、自定义模板的模板详情。

本文将提供一个示例，为您查询杭州地域`cn-hangzhou`模板ID为`5ecd1e10-b0e9-4389-a565-e4c15efc****`的模板详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetTemplate&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTemplate|要执行的操作，取值：GetTemplate。 |
|RegionId|String|是|cn-hangzhou|模板所属资源栈或资源栈组的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|StackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。

 **说明：** 您仅能指定StackId、ChangeSetId、StackGroupName、TemplateId其中一个参数。 |
|ChangeSetId|String|否|1f6521a4-05af-4975-afe9-bc4b45ad\*\*\*\*|更改集ID。

 **说明：** 您仅能指定StackId、ChangeSetId、StackGroupName、TemplateId其中一个参数。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。

 支持共享的模板和私有模板。共享模板TemplateId与TemplateARN相同，使用该值查询。

 **说明：** 您仅能指定StackId、ChangeSetId、StackGroupName、TemplateId其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。

 若为共享模板，当且仅当VersionOption为AllVersions时，支持指定该参数。

 取值范围：v1～v100。 |
|TemplateStage|String|否|Processed|模板阶段。仅在指定StackId、ChangeSetId或StackGroupName时生效。

 取值：

 -   Processed（默认值）：返回解析转换后的模板。
-   Original：返回用户指定的原始模板。 |
|IncludePermission|String|否|Enabled|是否查询模板共享信息。取值：

 -   Enabled：查询。
-   Disabled（默认值）：不查询。

**说明：** 仅限模板拥有者查询。 |
|StackGroupName|String|否|MyStackGroup|资源栈组名称。

 **说明：** 您仅能指定StackId、ChangeSetId、StackGroupName、TemplateId其中一个参数。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ChangeSetId|String|e85abe0c-6528-43fb-ae93-fdf8de22\*\*\*\*|更改集ID。仅在指定ChangeSetId时返回该参数。 |
|CreateTime|String|2020-11-18T08:49:26.000000|模板创建时间。仅在指定TemplateId时返回该参数。

 **说明：**

-   如果指定了TemplateVersion，则返回指定版本模板的创建时间。
-   如果未指定TemplateVersion，则返回模板的创建时间。 |
|Description|String|ROS template for create ECS instance.|模板描述。仅在指定TemplateId时返回该参数。 |
|OwnerId|String|151266687691\*\*\*\*|模板所属阿里云账号ID。仅在指定TemplateId时返回该参数。 |
|Permissions|Array of Permission| |模板的共享状态。仅在指定TemplateId，且IncludePermission为Enabled时返回该参数。

 **说明：**

-   如果未指定TemplateVersion，或者TemplateVersion不生效，则返回模板的共享状态。
-   如果指定了TemplateVersion，并且TemplateVersion生效，则返回版本关联模板的共享状态。 |
|AccountId|String|142437958638\*\*\*\*|共享的阿里云账号。 |
|ShareOption|String|ShareToAccounts|共享选项。

 取值为ShareToAccounts，表示共享给其他阿里云账号。 |
|TemplateVersion|String|v1|共享的模板版本。当ShareOption为ShareToAccounts，且VersionOption为Specified或Current时返回该参数。

 取值范围：v1~v100。 |
|VersionOption|String|AllVersions|共享版本选项。当ShareOption为ShareToAccounts时返回该参数。

 取值：

 -   AllVersions：共享模板所有版本。
-   Latest：只共享模板最新版本。模板版本增加时，共享的版本也随之变化，始终保持最新版本。
-   Current：只共享模板当前最新版本。模板版本增加时，共享的版本不变。
-   Specified：只共享模板指定的单个版本。 |
|RegionId|String|cn-hangzhou|模板所属资源栈或资源栈组的地域ID。仅在指定StackId、ChangeSetId或StackGroupName时返回该参数。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84\*\*\*\*|请求ID。 |
|ResourceGroupId|String|rg-acfmxazb4ph6aiy\*\*\*\*|资源组ID。 |
|ShareType|String|Private|模板的共享类型。仅在指定TemplateId时返回该参数。

 取值：

 -   Private：模板为用户自己所拥有。
-   Shared：模板由其他用户所共享。 |
|StackGroupName|String|MyStackGroup|资源栈组名称。仅在指定StackGroupName时返回该参数。 |
|StackId|String|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|资源栈ID。仅在指定StackId时返回该参数。 |
|TemplateARN|String|acs:ros:\*:151266687691\*\*\*\*:template/a52f81be-496f-4e1c-a286-8852ab54\*\*\*\*|模板ARN。仅在指定TemplateId时返回该参数。 |
|TemplateBody|String|\{"ROSTemplateFormatVersion": "2015-09-01"\}|模板内容。 |
|TemplateId|String|a52f81be-496f-4e1c-a286-8852ab54\*\*\*\*|模板的ID。仅在指定TemplateId时返回。

 如果是共享模板，返回结果与TemplateARN相同。 |
|TemplateName|String|MyTemplate|模板的名称。仅在指定TemplateId时返回。

 **说明：**

-   如果指定了TemplateVersion，则返回版本关联的模板名称。
-   如果未指定TemplateVersion，则返回模板的名称。 |
|TemplateVersion|String|v1|模板版本。仅在指定TemplateId时返回该参数。

 如果未指定TemplateVersion，或TemplateVersion未生效，则该参数表示模板当前版本。

 若为共享模板，当且仅当VersionOption为AllVersions时，支持返回该参数。 |
|UpdateTime|String|2020-12-07T06:11:48.000000|模板的最后更新时间。仅在指定TemplateId时返回该参数。

 **说明：**

-   如果指定了TemplateVersion，则返回指定版本模板的最后更新时间。
-   如果未指定TemplateVersion，则返回模板的最后更新时间。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetTemplate
&RegionId=cn-hangzhou
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&IncludePermission=Enabled
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetTemplateResponse>
      <TemplateARN>acs:ros:*:151266687691****:template/a52f81be-496f-4e1c-a286-8852ab54****</TemplateARN>
      <ResourceGroupId>rg-acfmxazb4ph6aiy****</ResourceGroupId>
      <Description>ROS template for create ECS instance.</Description>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84****</RequestId>
      <CreateTime>2020-11-18T08:49:26.000000</CreateTime>
      <TemplateVersion>v1</TemplateVersion>
      <TemplateBody>{"ROSTemplateFormatVersion": "2015-09-01"}</TemplateBody>
      <OwnerId>151266687691****</OwnerId>
      <UpdateTime>2020-12-07T06:11:48.000000</UpdateTime>
      <Permissions>
            <ShareOption>ShareToAccounts</ShareOption>
            <TemplateVersion>v1</TemplateVersion>
            <AccountId>142437958638****</AccountId>
            <VersionOption>AllVersions</VersionOption>
      </Permissions>
      <TemplateName>MyTemplate</TemplateName>
      <TemplateId>a52f81be-496f-4e1c-a286-8852ab54****</TemplateId>
      <ShareType>Private</ShareType>
</GetTemplateResponse>
```

`JSON`格式

```
{
  "TemplateARN": "acs:ros:*:151266687691****:template/a52f81be-496f-4e1c-a286-8852ab54****",
  "ResourceGroupId": "rg-acfmxazb4ph6aiy****",
  "Description": "ROS template for create ECS instance.",
  "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84****",
  "CreateTime": "2020-11-18T08:49:26.000000",
  "TemplateVersion": "v1",
  "TemplateBody": "{\"ROSTemplateFormatVersion\": \"2015-09-01\"}",
  "OwnerId": "151266687691****",
  "UpdateTime": "2020-12-07T06:11:48.000000",
  "Permissions": [
    {
      "ShareOption": "ShareToAccounts",
      "TemplateVersion": "v1",
      "AccountId": "142437958638****",
      "VersionOption": "AllVersions"
    }
  ],
  "TemplateName": "MyTemplate",
  "TemplateId": "a52f81be-496f-4e1c-a286-8852ab54****",
  "ShareType": "Private"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|ChangeSetNotFound

|The ChangeSet \(\{name\}\) of Stack \(\{stack\}\) could not be found.

|更改集不存在。name为更改集名称或ID，stack为资源栈名称或ID。 |
|404

|ChangeSetNotFound

|The ChangeSet \{ID\} could not be found.

|更改集不存在。ID为更改集ID。 |
|404

|StackNotFound

|The Stack \(\{name\}\) could not be found.

|资源栈不存在。name为资源栈名称或ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |
|404

|StackGroupNotFound

|The StackGroup \(\{name\}\) could not be found.

|资源栈组不存在。name为资源栈组名称。 |


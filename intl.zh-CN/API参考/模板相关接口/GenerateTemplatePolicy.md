# GenerateTemplatePolicy

调用GenerateTemplatePolicy接口生成模板所需的策略信息。

如果模板所需的策略中包含企业级分布式应用服务EDAS（Enterprise Distributed Application Service），您需要登录阿里云账号，对需要授权的RAM用户进行RAM权限升级。

本文将提供一个示例，为您介绍如何为模板ID为`5ecd1e10-b0e9-4389-a565-e4c15efc****`的模板生成权限策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GenerateTemplatePolicy&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GenerateTemplatePolicy|要执行的操作，取值：GenerateTemplatePolicy。 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为524,288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您仅能指定TemplateBody、TemplateURL、TemplateId其中一个参数。

 URL的最大长度为：1024个字节。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|模板的结构。长度为1~524,288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您仅能指定TemplateBody、TemplateURL、TemplateId其中一个参数。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 您仅能指定TemplateBody、TemplateURL、TemplateId其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Policy|Struct| |权限策略信息。 |
|Statement|Array of Statement| |具体权限策略信息。 |
|Action|List|\[ "apigateway:CreateApi", "apigateway:DeleteApi","apigateway:DescribeApi","apigateway:ModifyApi"\]|对具体资源的操作。 |
|Effect|String|Allow|授权效力。取值：

 -   Allow：允许。
-   Deny：拒绝。 |
|Resource|String|\*|被授权的具体对象。星号（\*）表示所有资源。 |
|Version|String|1|版本号。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GenerateTemplatePolicy
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<Policy>
    <Version>1</Version>
    <Statement>
        <Action>ecs:DescribeVpcs</Action>
        <Action>ecs:DeleteVpc</Action>
        <Resource>*</Resource>
        <Effect>Allow</Effect>
    </Statement>
    <Statement>
        <Action>vpc:CreateVpc</Action>
        <Action>vpc:DescribeVpcs</Action>
        <Action>vpc:ModifyVpcAttribute</Action>
        <Action>vpc:TagResources</Action>
        <Resource>*</Resource>
        <Effect>Allow</Effect>
    </Statement>
</Policy>
<RequestId>16AAEDEB-6273-405E-97D3-023EFD95DE03</RequestId>
```

`JSON`格式

```
{
    "Policy": {
        "Version": 1,
        "Statement": [
            {
                "Action": [
                    "ecs:DescribeVpcs",
                    "ecs:DeleteVpc"
                ],
                "Resource": "*",
                "Effect": "Allow"
            },
            {
                "Action": [
                    "vpc:CreateVpc",
                    "vpc:DescribeVpcs",
                    "vpc:ModifyVpcAttribute",
                    "vpc:TagResources"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ]
    },
    "RequestId": "16AAEDEB-6273-405E-97D3-023EFD95DE03"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|StackValidationFailed

|\{reason\}.

|资源栈校验失败。reason为具体原因。 |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |


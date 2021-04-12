# GenerateTemplatePolicy

You can call this operation to generate the policy information for a template.

If the policy information involves Enterprise Distributed Application Service \(EDAS\), you must log on to your Alibaba Cloud account and grant corresponding permissions to the involved RAM user.

In this example, a policy is generated for a template whose ID is `5ecd1e10-b0e9-4389-a565-e4c15efc****`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GenerateTemplatePolicy&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GenerateTemplatePolicy|The operation that you want to perform. Set the value to GenerateTemplatePolicy. |
|TemplateURL|String|No|oss://ros/template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 524,288 bytes in length, and the URL can be up to 1,024 bytes in length.

**Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion":"2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

You can specify only one of TemplateBody, TemplateURL, and TemplateId. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Policy|Struct| |The information of the policy. |
|Statement|Array of Statement| |Details about the policy information. |
|Action|List|\[ "apigateway:CreateApi", "apigateway:DeleteApi","apigateway:DescribeApi","apigateway:ModifyApi"\]|The operation on the specified resource. |
|Effect|String|Allow|The permission effect. Valid values:

-   Allow
-   Deny |
|Resource|String|\*|The authorization object. An asterisk \(\*\) indicates all resources. |
|Version|String|1|The version number. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GenerateTemplatePolicy
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|StackValidationFailed

|\{reason\}.

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or template version does not exist. ID indicates the template ID, and version indicates the template version. |


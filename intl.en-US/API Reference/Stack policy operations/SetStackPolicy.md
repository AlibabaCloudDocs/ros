# SetStackPolicy

You can call this operation to configure a stack policy.

In this example, a stack policy is configured for a stack deployed in the `China (Hangzhou)` region whose ID is `4a6c9851-3b0f-4f5f-b4ca-a14bf691****`. The URL to the stack policy body is `oss://ros/stack-policy/demo`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=SetStackPolicy&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetStackPolicy|The operation that you want to perform. Set the value to SetStackPolicy. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |
|StackPolicyBody|String|No|\{"Statement":\[\{"Effect":"Allow","Action":"Update:\*","Principal":"\*","Resource":"\*"\}\]\}|The structure that contains the stack policy body. The stack policy body must be 1 to 16,384 bytes in length.

 You can specify one of the StackPolicyBody and StackPolicyURL parameters, but you cannot specify both of them. |
|StackPolicyURL|String|No|oss://ros/stack-policy/demo|The URL for the file that contains the stack policy. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 16,384 bytes in length, and the URL can be up to 1,350 bytes in length.

 **Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

 You can specify one of the StackPolicyBody and StackPolicyURL parameters, but you cannot specify both of them.

  |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=SetStackPolicy
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&StackPolicyURL=oss://ros/stack-policy/demo
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetStackPolicyResponse>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</SetStackPolicyResponse>
```

`JSON` format

```
{
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|StackValidationFailed

|\{reason\}.

|400

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |


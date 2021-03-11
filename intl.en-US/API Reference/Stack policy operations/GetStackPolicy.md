# GetStackPolicy

You can call this operation to query information about a stack policy.

In this example, the stack policy of a stack whose ID is `4a6c9851-3b0f-4f5f-b4ca-a14bf691****` is queried. The stack is deployed in the China \(Hangzhou\) region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetStackPolicy&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetStackPolicy|The operation that you want to perform. Set the value to GetStackPolicy. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|StackId|String|Yes|4a6c9851-3b0f-4f5f-b4ca-a14bf691\*\*\*\*|The ID of the stack. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|StackPolicyBody|Map|\{"Statement": \[\{"Action": "Update:\*", "Effect": "Allow","Principal": "\*","Resource": "\*"\}\]\}|The structure that contains the stack policy body. The policy body must be 1 to 16,384 bytes in length. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=GetStackPolicy
&StackId=4a6c9851-3b0f-4f5f-b4ca-a14bf691****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetStackPolicyResponse> 
    <StackPolicyBody> 
        <Statement> 
            <Statement> 
                <Resource>*</Resource>  
                <Principal>*</Principal>  
                <Action>Update:*</Action>  
                <Effect>Allow</Effect> 
            </Statement>  
            <Statement> 
                <Resource>LogicalResourceId/WebServer</Resource>  
                <Principal>*</Principal>  
                <Action>Update:*</Action>  
                <Effect>Deny</Effect> 
            </Statement> 
        </Statement> 
    </StackPolicyBody>  
    <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId> 
</GetStackPolicyResponse>
```

`JSON` format

```
{
  "StackPolicyBody": {
    "Statement": [
      {
        "Action": "Update:*",
        "Effect": "Allow",
        "Principal": "*",
        "Resource": "*"
      },
      {
        "Action": "Update:*",
        "Effect": "Deny",
        "Principal": "*",
        "Resource": "LogicalResourceId/WebServer"
      }
    ]
  },
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
|StackNotFound

|The Stack \(\{name\}\) could not be found.

|404

|The error message returned because the specified stack does not exist. name indicates the name or ID of the stack. |


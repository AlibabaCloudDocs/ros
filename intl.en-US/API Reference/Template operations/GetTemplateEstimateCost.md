# GetTemplateEstimateCost

You can call this operation to query estimated prices of resources to be created based on a template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=GetTemplateEstimateCost&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTemplateEstimateCost|The operation that you want to perform. Set the value to GetTemplateEstimateCost. |
|Parameters.N.ParameterKey|String|Yes|InstanceId|The key of parameter N. If the key and value of the parameter are not specified, the key and value specified in the template are used.

Maximum value of N: 200. |
|Parameters.N.ParameterValue|String|Yes|i-m5e3tfdbinchnexh\*\*\*\*|The value of parameter N.

Maximum value of N: 200. |
|RegionId|String|Yes|cn-beijing|The region ID of the stack. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|TemplateURL|String|No|oss://ros-template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 524,288 bytes in length, and the URL can be up to 1,024 bytes in length.

**Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

You must specify one of the TemplateBody, TemplateURL, and TemplateId parameters, but you cannot specify all of them. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion": "2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

You must specify one of the TemplateBody, TemplateURL, and TemplateId parameters, but you cannot specify all of them. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests.

The token can be up to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\).

For more information, see [How to ensure idempotence](~~134212~~). |
|TemplateId|String|No|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|The ID of the template. This parameter applies to shared and private templates.

You must specify one of the TemplateBody, TemplateURL, and TemplateId parameters, but you cannot specify all of them. |
|TemplateVersion|String|No|v1|The version of the template. This parameter takes effect only when the TemplateId parameter is specified. |

For more information about common request parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Resources|Map|The parameters in the Resources section|The details about resources. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|The ID of the request. |

The following table describes the parameters in the Resources section.

|Parameter

|Type

|Example

|Description |
|-----------|------|---------|-------------|
|Order

| | |Details about the order. |
|Currency

|String

|CNY

|The currency unit. |
|DiscountAmount

|Long

|100

|The discount. |
|HandlingFeeAmount

|Long

|0

|The service fee. |
|OptionalMixPromotions

|Array

|\[\]

|The available mixed discounts. |
|OptionalPromotions

|Array

|\[\]

|The available discounts. |
|OrderLines

|String

| |The order information. |
|OriginalAmount

|Long

|200

|The original price of the service. |
|RiCycleAmount

|Long

|0

|The deducted amount of money. |
|RuleIds

|Array

|\[100000\*\*\*\*\]

|The list of one or more IDs of the discount rules. |
|TaxAmount

|Long

|0

|The amount of tax. |
|TradeAmount

|Long

|100

|The final price after the discount. |
|Rules

| | |Details about the discount rules. |
|Name

|String

|Discount on membership

|The name of the discount rule. |
|RuleDescId

|Long

|100000\*\*\*\*

|The ID of the discount rule. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/? Action=GetTemplateEstimateCost
&RegionId=cn-beijing
&Parameters.1.ParameterKey=InstanceId
&Parameters.1.ParameterValue=i-m5e3tfdbinchnexh****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<Resources>
    <NewEip>
        <Result>
            <Order>
                <Currency>CNY</Currency>
                <DiscountAmount>2.4</DiscountAmount>
                <HandlingFeeAmount>0</HandlingFeeAmount>
                <OrderLines/>
                <OriginalAmount>2.4</OriginalAmount>
                <RiCycleAmount>0</RiCycleAmount>
                <RuleIds>100000****</RuleIds>
                <TaxAmount>0</TaxAmount>
                <TradeAmount>0</TradeAmount>
            </Order>
            <Rules>
                <Rule>
                    <Name>Discount on membership</Name>
                    <RuleDescId>100000****</RuleDescId>
                </Rule>
            </Rules>
        </Result>
        <Success>true</Success>
        <Type>ALIYUN::VPC::EIP</Type>
    </NewEip>
</Resources>
<RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
```

`JSON` format

```
{
    "Resources": {
        "NewEip": {
            "Result": {
                "Order": {
                    "Currency": "CNY",
                    "DiscountAmount": 2.4,
                    "HandlingFeeAmount": 0,
                    "OptionalMixPromotions": [],
                    "OptionalPromotions": [],
                    "OrderLines": null,
                    "OriginalAmount": 2.4,
                    "RiCycleAmount": 0,
                    "RuleIds": [
                        100000****
                    ],
                    "TaxAmount": 0,
                    "TradeAmount": 0
                },
                "Rules": {
                    "Rule": [
                        {
                            "Name": "Discount on membership",
                            "RuleDescId": 100000****
                        }
                    ]
                }
            },
            "Success": true,
            "Type": "ALIYUN::VPC::EIP"
        }
    },
    "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"    
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|400

|CircularDependency

|Circular Dependency Found: \{reason\}.

|The error message returned because the template contains a circular dependency. reason indicates the specific reason. |
|400

|InvalidSchema

|\{reason\}.

|The error message returned because the specified template format is invalid. reason indicates the specific reason. |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|The error message returned because the resource attribute referenced in the template is incorrect. resource indicates the resource name, and name indicates the attribute name. |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|The error message returned because the type of the specified resource section defined in the template is incorrect. resource indicates the resource name, and section indicates the section name. |
|400

|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|The error message returned because the template contains an invalid reference. name indicates the reference name, and referencer indicates the referencer name. |
|400

|InvalidTemplateSection

|The template section is invalid: \{section\}.

|The error message returned because the template contains an invalid section. section indicates the section name. |
|400

|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|The error message returned because the template version is incorrect. reason indicates the specific reason. |
|400

|StackValidationFailed

|\{reason\}.

|The error message returned because the stack validation failed. reason indicates the specific reason. |
|400

|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|The error message returned because the specified parameter is not defined in the template. name indicates the parameter key. |
|400

|UserParameterMissing

|The Parameter \{name\} was not provided.

|The error message returned because no value is passed into the specified parameter defined in the template. name indicates the parameter key. |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|The error message returned because the specified template does not exist. ID indicates the template ID. |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|The error message returned because the specified template or version does not exist. ID indicates the template ID, and version indicates the template version. |


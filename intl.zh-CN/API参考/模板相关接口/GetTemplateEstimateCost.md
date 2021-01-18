# GetTemplateEstimateCost

调用GetTemplateEstimateCost接口查询模板中创建资源的预估价格。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetTemplateEstimateCost&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTemplateEstimateCost|要执行的操作，取值：GetTemplateEstimateCost。 |
|Parameters.N.ParameterKey|String|是|InstanceId|参数的名称。如果未指定模板中定义的参数名称和参数值，ROS将使用模板中指定的默认值。

 N的最大值为：200。 |
|Parameters.N.ParameterValue|String|是|i-m5e3tfdbinchnexh\*\*\*\*|参数值。

 N的最大值为：200。 |
|RegionId|String|是|cn-beijing|资源栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为524,288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您仅能指定TemplateBody、TemplateURL、TemplateId其中一个参数。

 URL的最大长度为：1024个字节。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion": "2015-09-01"\}|模板的结构。长度为1~524,288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您仅能指定TemplateBody、TemplateURL、TemplateId其中一个参数。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求的幂等性。 该值由客户端生成，并且必须全局唯一。

 长度不超过64个字符。可包含英文字母、数字、短划线（-）和下划线（\_）。

 更多信息，请参见[如何保证幂等性](~~134212~~)。 |
|TemplateId|String|否|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。

 您仅能指定TemplateBody、TemplateURL、TemplateId其中一个参数。 |
|TemplateVersion|String|否|v1|模板版本。仅在指定TemplateId时生效。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Resources|Map|请参见返回示例中的Resources参数|资源详情。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |

Resources各参数含义如下所示。

|名称

|类型

|示例值

|描述 |
|----|----|-----|----|
|Order

| | |订单信息 |
|Currency

|String

|CNY

|货币单位 |
|DiscountAmount

|Long

|100

|折扣 |
|HandlingFeeAmount

|Long

|0

|手续费金额 |
|OptionalMixPromotions

|Array

|\[\]

|可选的混合促销 |
|OptionalPromotions

|Array

|\[\]

|可选促销 |
|OrderLines

|String

| |订单信息 |
|OriginalAmount

|Long

|200

|原价 |
|RiCycleAmount

|Long

|0

|抵扣金额 |
|RuleIds

|Array

|\[100000\*\*\*\*\]

|活动规则列表 |
|TaxAmount

|Long

|0

|税额 |
|TradeAmount

|Long

|100

|最终价，为原价减去折扣。 |
|Rules

| | |活动规则 |
|Name

|String

|会员享受折扣

|活动规则名称 |
|RuleDescId

|Long

|100000\*\*\*\*

|活动ID |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=GetTemplateEstimateCost
&RegionId=cn-beijing
&Parameters.1.ParameterKey=InstanceId
&Parameters.1.ParameterValue=i-m5e3tfdbinchnexh****
&<公共请求参数>
```

正常返回示例

`XML` 格式

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
                    <Name>会员享受折扣</Name>
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

`JSON` 格式

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
                            "Name": "会员享受折扣",
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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|CircularDependency

|Circular Dependency Found: \{reason\}.

|模板包含循环引用。reason为具体原因。 |
|400

|InvalidSchema

|\{reason\}.

|模板格式不正确。reason为具体原因。 |
|400

|InvalidTemplateAttribute

|The Referenced Attribute \(\{resource\} \{name\}\) is incorrect.

|模板包含不正确的资源属性（输出）引用。resource为资源名，name为属性名。 |
|400

|InvalidTemplatePropertyType

|The specified value type of \(\{resource\} \{section\}\) is incorrect.

|模板资源定义中的字段类型不正确。resource为资源名，section为字段名。 |
|400

|InvalidTemplateReference

|The specified reference "\{name\}" \(in \{referencer\}\) is incorrect.

|模板包含不正确的引用。name为引用名，referencer为引用者。 |
|400

|InvalidTemplateSection

|The template section is invalid: \{section\}.

|模板包含无效的字段。section为字段名。 |
|400

|InvalidTemplateVersion

|The template version is invalid: \{reason\}.

|模板版本不正确。reason为具体原因。 |
|400

|StackValidationFailed

|\{reason\}.

|资源栈校验失败。reason为具体原因。 |
|400

|UnknownUserParameter

|The Parameter \(\{name\}\) was not defined in template.

|传递的参数在模板中未定义。name为参数名。 |
|400

|UserParameterMissing

|The Parameter \{name\} was not provided.

|参数在模板中已定义，但未传递值。name为参数名。 |
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |


# GetTemplateEstimateCost {#doc_api_ROS_GetTemplateEstimateCost .reference}

查询模板中要创建的资源的预估价格。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetTemplateEstimateCost&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTemplateEstimateCost|系统规定参数。取值：GetTemplateEstimateCost。

 |
|RegionId|String|是|cn-beijing|堆栈所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|Parameters.N.ParameterKey|String|否|InstanceId|参数的名称。 如果未指定特定参数的名称和值，则ROS将使用模板中指定的默认值。

 N最大值为200。

 |
|Parameters.N.ParameterValue|String|否|i-xxxxxx|参数的值。

 N最大值为200。

 |
|TemplateURL|String|否|oss://ros-template/demo|包含模板主体的文件的位置。 URL必须指向位于http Web服务器（http，https），或阿里云OSS存储桶（例如oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou。oss地域如未指定，默认与接口参数RegionId相同。）中的模板（最大大小：524288字节）。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |
|TemplateBody|String|否|\{ "ROSTemplateFormatVersion": "2015-09-01" \}|包含模板体的结构，最小长度为1个字节，最大长度为51,200个字节。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求的幂等性。 该值由客户端生成，并且必须是全局唯一的。 仅允许使用字母数字字符（区分大小写），连字符和下划线。 它最多可包含64个字符。更多详情，请参见[如何保证幂等性](~~134212~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Resources|Map|参考返回示例中的Resources字段|资源详情。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetTemplateEstimateCost
&RegionId=cn-beijing
&Parameters.1.ParameterKey=InstanceId
&Parameters.1.ParameterValue=i-xxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetTemplateEstimateCostResponse>
      <Resources>
            <Resource>
                  <NewEip>
                        <Result>
                              <Order>
                                    <Currency>CNY</Currency>
                                    <DiscountAmount>2.4</DiscountAmount>
                                    <HandlingFeeAmount>0.0</HandlingFeeAmount>
                                    <OptionalMixPromotions></OptionalMixPromotions>
                                    <OptionalPromotions></OptionalPromotions>
                                    <OrderLines></OrderLines>
                                    <OriginalAmount>2.4</OriginalAmount>
                                    <RiCycleAmount>0.0</RiCycleAmount>
                                    <RuleIds>
                                          <RuleId>1000000000</RuleId>
                                    </RuleIds>
                                    <TaxAmount>0.0</TaxAmount>
                                    <TradeAmount>0.0</TradeAmount>
                              </Order>
                              <Rules>
                                    <Rule>
                                          <Name>xxxxx</Name>
                                          <RuleDescId>1000000000</RuleDescId>
                                    </Rule>
                              </Rules>
                        </Result>
                        <Success>true</Success>
                        <Type>ALIYUN::VPC::EIP</Type>
                  </NewEip>
            </Resource>
      </Resources>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>    
</GetTemplateEstimateCostResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"Resources":{
		"NewEip":{
			"Result":{
				"Order":{
					"RuleIds":[
						1001199213
					],
					"OriginalAmount":2.4,
					"TradeAmount":0,
					"OptionalMixPromotions":[],
					"OptionalPromotions":[],
					"RiCycleAmount":0,
					"HandlingFeeAmount":0,
					"TaxAmount":0,
					"DiscountAmount":2.4,
					"Currency":"CNY"
				},
				"Rules":{
					"Rule":[
						{
							"Name":"内部结算用户0元付",
							"RuleDescId":1001199213
						}
					]
				}
			},
			"Type":"ALIYUN::VPC::EIP",
			"Success":true
		}
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。


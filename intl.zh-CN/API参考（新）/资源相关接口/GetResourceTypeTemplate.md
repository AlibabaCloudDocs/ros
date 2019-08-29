# GetResourceTypeTemplate {#doc_api_ROS_GetResourceTypeTemplate .reference}

根据资源类型查询该资源的模板。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetResourceTypeTemplate&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetResourceTypeTemplate|系统规定参数。取值：GetResourceTypeTemplate。

 |
|ResourceType|String|是|ALIYUN::ECS::VPC|资源类型。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|87F54B2B-AEF0-4C33-A72A-3F8856A575E9|请求ID。

 |
|TemplateBody|Map|\{"ROSTemplateFormatVersion":"2015-09-01"\}|包含模板体的结构，最小长度为1个字节，最大长度为51,200个字节。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetResourceTypeTemplate
&ResourceType=ALIYUN::ECS::VPC
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetResourceTypeTemplateResponse>
       <RequestId type="string">87F54B2B-AEF0-4C33-A72A-3F8856A575E9</RequestId>
       <TemplateBody class="object">
              <Parameters class="object">
                     <CidrBlock class="object">
                            <Type type="string">String</Type>
                     </CidrBlock>
                     <Description class="object">
                            <Type type="string">String</Type>
                     </Description>
                     <ResourceGroupId class="object">
                            <Type type="string">String</Type>
                     </ResourceGroupId>
                     <VpcName class="object">
                            <Type type="string">String</Type>
                     </VpcName>
              </Parameters>
              <ROSTemplateFormatVersion type="string">2015-09-01</ROSTemplateFormatVersion>
              <Resources class="object">
                     <Vpc class="object">
                            <Properties class="object">
                                   <CidrBlock class="object">
                                          <Ref type="string">CidrBlock</Ref>
                                   </CidrBlock>
                                   <Description class="object">
                                          <Ref type="string">Description</Ref>
                                   </Description>
                                   <ResourceGroupId class="object">
                                          <Ref type="string">ResourceGroupId</Ref>
                                   </ResourceGroupId>
                                   <VpcName class="object">
                                          <Ref type="string">VpcName</Ref>
                                   </VpcName>
                            </Properties>
                            <Type type="string">ALIYUN::ECS::VPC</Type>
                     </Vpc>
              </Resources>
       </TemplateBody>
</GetResourceTypeTemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TemplateBody":{
		"Parameters":{
			"VpcName":{
				"Type":"String"
			},
			"CidrBlock":{
				"Type":"String"
			},
			"Description":{
				"Type":"String"
			},
			"ResourceGroupId":{
				"Type":"String"
			}
		},
		"ROSTemplateFormatVersion":"2015-09-01",
		"Resources":{
			"Vpc":{
				"Type":"ALIYUN::ECS::VPC",
				"Properties":{
					"VpcName":{
						"Ref":"VpcName"
					},
					"CidrBlock":{
						"Ref":"CidrBlock"
					},
					"Description":{
						"Ref":"Description"
					},
					"ResourceGroupId":{
						"Ref":"ResourceGroupId"
					}
				}
			}
		}
	},
	"RequestId":"87F54B2B-AEF0-4C33-A72A-3F8856A575E9"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。


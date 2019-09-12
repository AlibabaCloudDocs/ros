# ValidateTemplate {#doc_api_ROS_ValidateTemplate .reference}

验证将要创建资源栈的模板。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ValidateTemplate&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ValidateTemplate|系统规定参数。取值：ValidateTemplate。

 |
|RegionId|String|否|cn-hangzhou|资源栈模板所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|包含模板体的结构，最小长度为1个字节，最大长度为51,200个字节。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。 URL必须指向位于http Web服务器（http，https），或阿里云OSS存储桶（例如oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou。oss地域如未指定，默认与接口参数RegionId相同。）中的模板（最大大小：524288字节）。

 您必须指定TemplateBody或TemplateURL参数，但不能同时指定两者。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Description|String|No description|描述此堆栈模板的相关信息。

 |
|Parameters| |\[\{"Description": "", "Label": "param\_integer", "NoEcho": "false", "ParameterKey": "param\_integer", "Type": "Number"\},\{ "Description": "", "Label": "param\_float", "NoEcho": "false", "ParameterKey": "param\_float", "Type": "Number"\}\]|输入参数。输入参数中，定义了通过此模板创建资源栈时需要指定的参数，这些参数用来订制每次资源栈创建的细节，比如用户名、密码，环境相关的 ECS 规格等。

 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=ValidateTemplate
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ValidateTemplateResponse>
       <Description type="string">No description</Description>
       <Parameters class="array">
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_integer</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_integer</ParameterKey>
                     <Type type="string">Number</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_float</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_float</ParameterKey>
                     <Type type="string">Number</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_bool</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_bool</ParameterKey>
                     <Type type="string">Boolean</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_json_list</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_json_list</ParameterKey>
                     <Type type="string">Json</Type>
              </Parameter>
              <Parameter class="object">
                     <Default class="object">
                            <c class="array"></c>
                     </Default>
                     <Description type="string"></Description>
                     <Label type="string">param_has_default</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_has_default</ParameterKey>
                     <Type type="string">Json</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">UpdateVersion</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">UpdateVersion</ParameterKey>
                     <Type type="string">Number</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_str</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_str</ParameterKey>
                     <Type type="string">String</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_list</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_list</ParameterKey>
                     <Type type="string">CommaDelimitedList</Type>
              </Parameter>
              <Parameter class="object">
                     <Description type="string"></Description>
                     <Label type="string">param_json_dict</Label>
                     <NoEcho type="string">false</NoEcho>
                     <ParameterKey type="string">param_json_dict</ParameterKey>
                     <Type type="string">Json</Type>
              </Parameter>
       </Parameters>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</ValidateTemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Parameters":[
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"Number",
			"Label":"param_integer",
			"ParameterKey":"param_integer"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"Number",
			"Label":"param_float",
			"ParameterKey":"param_float"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"Boolean",
			"Label":"param_bool",
			"ParameterKey":"param_bool"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"Json",
			"Label":"param_json_list",
			"ParameterKey":"param_json_list"
		},
		{
			"Default":{
				"c":[]
			},
			"NoEcho":"false",
			"Description":"",
			"Type":"Json",
			"Label":"param_has_default",
			"ParameterKey":"param_has_default"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"Number",
			"Label":"UpdateVersion",
			"ParameterKey":"UpdateVersion"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"String",
			"Label":"param_str",
			"ParameterKey":"param_str"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"CommaDelimitedList",
			"Label":"param_list",
			"ParameterKey":"param_list"
		},
		{
			"NoEcho":"false",
			"Description":"",
			"Type":"Json",
			"Label":"param_json_dict",
			"ParameterKey":"param_json_dict"
		}
	],
	"Description":"No description",
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

访问[公共错误码](~~131033~~)查看更多错误码。

|错误代码

|错误信息

|Http状态码

|描述

|
|------|------|---------|----|
|InvalidTemplate

|\{reason\}.

|400

|模板不正确，reason为具体原因。

|


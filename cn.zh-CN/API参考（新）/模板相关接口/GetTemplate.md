# GetTemplate {#doc_api_ROS_GetTemplate .reference}

查询堆栈、更改集的详细信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=GetTemplate&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTemplate|系统规定参数。取值：GetTemplate。

 |
|RegionId|String|是|cn-hangzhou|模板所属堆栈的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。

 |
|StackId|String|否|4a6c9851-3b0f-4f5f-b4ca-a14bf691f2ff|资源栈ID。

 |
|ChangeSetId|String|否|1f6521a4-05af-4975-afe9-bc4b45ad5bd5|更改集ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |
|TemplateBody|String|\{\\"ROSTemplateFormatVersion\\": \\"2015-09-01\\"\}|包含模板体的结构，最小长度为1个字节，最大长度为51,200个字节。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=GetTemplate
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetTemplateResponse>
        <TemplateBody>{"ROSTemplateFormatVersion": "2015-09-01", "Resources": {"dummy2": {"Type": "ALIYUN::DEBUG::Dummy", "Properties": {"Map": {"Ref": "param_has_default"}, "List": {"Ref": "param_list"}}}, "dummy": {"Type": "ALIYUN::DEBUG::Dummy", "Properties": {"Map": {"Ref": "param_json_dict"}, "String": {"Ref": "param_str"}, "List": {"Ref": "param_json_list"}, "Number": {"Ref": "param_float"}, "Bool": {"Ref": "param_bool"}, "Integer": {"Ref": "param_integer"}}}, "nested": {"Type": "ALIYUN::ROS::Stack", "Properties": {"TemplateURL": "oss://nested-stack/simple/nested_demo", "TimeoutMins": 16}}, "WaitConditionHandle": {"Type": "ALIYUN::ROS::WaitConditionHandle", "Properties": {"UpdateVersion": {"Ref": "UpdateVersion"}}}}, "Parameters": {"param_integer": {"Type": "Number"}, "param_float": {"Type": "Number"}, "param_bool": {"Type": "Boolean"}, "param_json_list": {"Type": "Json"}, "param_has_default": {"Default": "{\"c\": []}", "Type": "Json"}, "UpdateVersion": {"Type": "Number"}, "param_str": {"Type": "String"}, "param_list": {"Type": "CommaDelimitedList"}, "param_json_dict": {"Type": "Json"}}, "Outputs": {"param_integer": {"Value": {"Ref": "param_integer"}}, "param_float": {"Value": {"Ref": "param_float"}}, "param_bool": {"Value": {"Ref": "param_bool"}}, "param_json_list": {"Value": {"Ref": "param_json_list"}}, "param_has_default": {"Value": {"Ref": "param_has_default"}}, "param_str": {"Value": {"Ref": "param_str"}}, "CurlCli": {"Value": {"Fn::GetAtt": ["WaitConditionHandle", "CurlCli"]}}, "param_list": {"Value": {"Ref": "param_list"}}, "param_json_dict": {"Value": {"Ref": "param_json_dict"}}}}</TemplateBody>
        <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</GetTemplateResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TemplateBody":"{\"ROSTemplateFormatVersion\": \"2015-09-01\", \"Resources\": {\"dummy2\": {\"Type\": \"ALIYUN::DEBUG::Dummy\", \"Properties\": {\"Map\": {\"Ref\": \"param_has_default\"}, \"List\": {\"Ref\": \"param_list\"}}}, \"dummy\": {\"Type\": \"ALIYUN::DEBUG::Dummy\", \"Properties\": {\"Map\": {\"Ref\": \"param_json_dict\"}, \"String\": {\"Ref\": \"param_str\"}, \"List\": {\"Ref\": \"param_json_list\"}, \"Number\": {\"Ref\": \"param_float\"}, \"Bool\": {\"Ref\": \"param_bool\"}, \"Integer\": {\"Ref\": \"param_integer\"}}}, \"nested\": {\"Type\": \"ALIYUN::ROS::Stack\", \"Properties\": {\"TemplateURL\": \"oss://nested-stack/simple/nested_demo\", \"TimeoutMins\": 16}}, \"WaitConditionHandle\": {\"Type\": \"ALIYUN::ROS::WaitConditionHandle\", \"Properties\": {\"UpdateVersion\": {\"Ref\": \"UpdateVersion\"}}}}, \"Parameters\": {\"param_integer\": {\"Type\": \"Number\"}, \"param_float\": {\"Type\": \"Number\"}, \"param_bool\": {\"Type\": \"Boolean\"}, \"param_json_list\": {\"Type\": \"Json\"}, \"param_has_default\": {\"Default\": \"{\\\"c\\\": []}\", \"Type\": \"Json\"}, \"UpdateVersion\": {\"Type\": \"Number\"}, \"param_str\": {\"Type\": \"String\"}, \"param_list\": {\"Type\": \"CommaDelimitedList\"}, \"param_json_dict\": {\"Type\": \"Json\"}}, \"Outputs\": {\"param_integer\": {\"Value\": {\"Ref\": \"param_integer\"}}, \"param_float\": {\"Value\": {\"Ref\": \"param_float\"}}, \"param_bool\": {\"Value\": {\"Ref\": \"param_bool\"}}, \"param_json_list\": {\"Value\": {\"Ref\": \"param_json_list\"}}, \"param_has_default\": {\"Value\": {\"Ref\": \"param_has_default\"}}, \"param_str\": {\"Value\": {\"Ref\": \"param_str\"}}, \"CurlCli\": {\"Value\": {\"Fn::GetAtt\": [\"WaitConditionHandle\", \"CurlCli\"]}}, \"param_list\": {\"Value\": {\"Ref\": \"param_list\"}}, \"param_json_dict\": {\"Value\": {\"Ref\": \"param_json_dict\"}}}}",
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。


# ValidateTemplate

调用ValidateTemplate接口验证将要创建资源栈的模板。

本文将提供一个示例，验证将要创建资源栈的模板，包含模板主体的文件的位置`TemplateURL`为`oss://ros/template/demo`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ValidateTemplate&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ValidateTemplate|要执行的操作，取值：ValidateTemplate。 |
|TemplateURL|String|否|oss://ros/template/demo|包含模板主体的文件的位置。URL必须指向位于Web服务器（HTTP或HTTPS）或阿里云OSS存储桶（例如：oss://ros/template/demo、oss://ros/template/demo?RegionId=cn-hangzhou）中的模板，模板最大为524,288个字节。

 **说明：** 如果OSS地域未指定，默认与接口参数RegionId相同。

 您可以指定TemplateBody或TemplateURL参数，但不能同时指定。

 URL的最大长度为：1024个字节。 |
|RegionId|String|否|cn-hangzhou|资源栈模板所属的地域ID。您可以调用[DescribeRegions](~~131035~~)查看最新的阿里云地域列表。 |
|TemplateBody|String|否|\{"ROSTemplateFormatVersion":"2015-09-01"\}|模板的结构。长度为1~524,288个字节。

 如果长度较大，建议通过HTTP POST+Body Param的方式，将参数放在请求体中进行传递，避免URL过长而导致请求失败。

 您可以指定参数TemplateBody或TemplateURL，但不能同时指定。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Description|String|No description|描述此资源栈模板的相关信息。 |
|Parameters|List|\[\{"Description": "", "Label": "param\_integer", "NoEcho": "false", "ParameterKey": "param\_integer", "Type": "Number"\},\{ "Description": "", "Label": "param\_float", "NoEcho": "false", "ParameterKey": "param\_float", "Type": "Number"\}\]|输入参数。

 输入参数中，定义了通过此模板创建资源栈时需要指定的参数，这些参数用来定制每次资源栈创建的细节，例如：用户名、密码、环境相关的ECS规格等。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ValidateTemplate
&TemplateURL=oss://ros/template/demo
&<公共请求参数>
```

正常返回示例

`XML`格式

```
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

`JSON`格式

```
{
   "Description": "No description",
   "Parameters": [
       {
           "Description": "",
           "Label": "param_integer",
           "NoEcho": "false",
           "ParameterKey": "param_integer",
           "Type": "Number"
       },
       {
           "Description": "",
           "Label": "param_float",
           "NoEcho": "false",
           "ParameterKey": "param_float",
           "Type": "Number"
       },
       {
           "Description": "",
           "Label": "param_bool",
           "NoEcho": "false",
           "ParameterKey": "param_bool",
           "Type": "Boolean"
       },
       {
           "Description": "",
           "Label": "param_json_list",
           "NoEcho": "false",
           "ParameterKey": "param_json_list",
           "Type": "Json"
       },
       {
           "Default": {
               "c": []
           },
           "Description": "",
           "Label": "param_has_default",
           "NoEcho": "false",
           "ParameterKey": "param_has_default",
           "Type": "Json"
       },
       {
           "Description": "",
           "Label": "UpdateVersion",
           "NoEcho": "false",
           "ParameterKey": "UpdateVersion",
           "Type": "Number"
       },
       {
           "Description": "",
           "Label": "param_str",
           "NoEcho": "false",
           "ParameterKey": "param_str",
           "Type": "String"
       },
       {
           "Description": "",
           "Label": "param_list",
           "NoEcho": "false",
           "ParameterKey": "param_list",
           "Type": "CommaDelimitedList"
       },
       {
           "Description": "",
           "Label": "param_json_dict",
           "NoEcho": "false",
           "ParameterKey": "param_json_dict",
           "Type": "Json"
       }
   ],
   "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|错误代码

|错误信息

|HTTP状态码

|描述 |
|------|------|---------|----|
|InvalidTemplate

|\{reason\}.

|400

|模板不正确，reason为具体原因。 |


# ValidateTemplate

You can call this operation to validate the template that is used to create stacks.

In this example, a template that is used to create stacks is validated. The URL to the template body is `oss://ros/template/demo`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ROS&api=ValidateTemplate&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ValidateTemplate|The operation that you want to perform. Set the value to ValidateTemplate. |
|TemplateURL|String|No|oss://ros/template/demo|The URL of the file that contains the template body. The URL must point to a template located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/template/demo and oss://ros/template/demo?RegionId=cn-hangzhou. The template can be up to 524,288 bytes in length, and the URL can be up to 1,024 bytes in length.

**Note:** If the region of the OSS bucket is not specified, the RegionId value is used.

You must specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them. |
|RegionId|String|No|cn-hangzhou|The region ID of the stack template. You can call the [DescribeRegions](~~131035~~) operation to query the most recent region list. |
|TemplateBody|String|No|\{"ROSTemplateFormatVersion":"2015-09-01"\}|The structure that contains the template body. The template body must be 1 to 524,288 bytes in length.

If the length of the template body is longer than required, we recommend that you add parameters to the HTTP POST request body to avoid request failures due to excessive length of URLs.

You must specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them. |

For more information about common parameters, see [Common parameters](~~131957~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Description|String|No description|The description of the stack template. |
|Parameters|List|\[\{"Description": "", "Label": "param\_integer", "NoEcho": "false", "ParameterKey": "param\_integer", "Type": "Number"\},\{ "Description": "", "Label": "param\_float", "NoEcho": "false", "ParameterKey": "param\_float", "Type": "Number"\}\]|The input parameters of the stack template.

The input parameters define the parameters that you must specify to create stacks based on the template. These parameters specify information about a stack, such as the username, password, and environment-related ECS instance type. |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|The ID of the request. |

## Examples

Sample requests

```
http(s)://ros.aliyuncs.com/?Action=ValidateTemplate
&TemplateURL=oss://ros/template/demo
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ROS).

|Error code

|Error message

|HTTP status code

|Description |
|------------|---------------|------------------|-------------|
|InvalidTemplate

|\{reason\}.

|400

|The error message returned because the specified template is invalid. reason indicates the specific reason. |


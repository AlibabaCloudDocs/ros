# ListTemplateVersions

调用ListTemplateVersions接口查询模板的版本列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListTemplateVersions&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTemplateVersions|要执行的操作，取值：ListTemplateVersions。 |
|TemplateId|String|是|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0\*\*\*\*|下一个查询开始的Token。 |
|MaxResults|Long|否|50|使用NextToken方式查询时，每次最多返回的结果数。

 取值范围：1~100。

 默认值：50。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0\*\*\*\*|本次调用返回的查询凭证值。 |
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6F|请求ID。 |
|Versions|Array of Version| |版本列表。 |
|CreateTime|String|2020-02-27T07:47:47|版本创建时间。 |
|Description|String|test|版本相关的模板描述。 |
|TemplateId|String|5ecd1e10-b0e9-4389-a565-e4c15efc\*\*\*\*|模板ID。支持共享模板和私有模板。若为共享模板，取值与模板ARN相同。 |
|TemplateName|String|test|版本相关的模板名称。 |
|TemplateVersion|String|v1|版本号。

 对于共享模板，仅当VersionOption为AllVersions时返回该参数。

 取值范围：v1~v100。 |
|UpdateTime|String|2020-02-27T07:47:47|版本最后更新时间。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListTemplateVersions
&TemplateId=5ecd1e10-b0e9-4389-a565-e4c15efc****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListTemplateVersionsResponse>
      <Versions>
            <Description>test</Description>
            <CreateTime>2020-02-27T07:47:47</CreateTime>
            <UpdateTime>2020-02-27T07:47:47</UpdateTime>
            <TemplateVersion>v1</TemplateVersion>
            <TemplateName>test</TemplateName>
            <TemplateId>5ecd1e10-b0e9-4389-a565-e4c15efc****</TemplateId>
      </Versions>
      <NextToken>caeba0bbb2be03f84eb48b699f0****</NextToken>
      <RequestId>B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
</ListTemplateVersionsResponse>
```

`JSON` 格式

```
{
  "Versions": [
    {
      "Description": "test",
      "CreateTime": "2020-02-27T07:47:47",
      "UpdateTime": "2020-02-27T07:47:47",
      "TemplateVersion": "v1",
      "TemplateName": "test",
      "TemplateId": "5ecd1e10-b0e9-4389-a565-e4c15efc****"
    }
  ],
  "NextToken": "caeba0bbb2be03f84eb48b699f0****",
  "RequestId": "B288A0BE-D927-4888-B0F7-B35EF84B6E6F"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|TemplateNotFound

|The Tempalte \(\{ ID \}\) could not be found.

|模板不存在。ID为模板ID。 |
|404

|TemplateNotFound

|The Template \{ ID \} with version \{ version \} could not be found.

|模板或指定版本不存在。ID为模板ID，version为模板版本。 |


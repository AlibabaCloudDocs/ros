# ListTemplates

调用ListTemplates接口查询模板列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListTemplates&type=RPC&version=2019-09-10)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTemplates|要执行的操作，取值：ListTemplates。 |
|TemplateName|String|否|MyTemplate|模板名称。仅在ShareType为Private时生效。

 长度不超过255个字符，必须以数字或英文字母开头，可包含数字、英文字母、短划线（-）和下划线（\_）。 |
|PageNumber|Long|否|1|模板列表的页码。

 起始值：1。

 默认值：1。 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 取值范围：1~50。

 默认值：10。 |
|Tag.N.Key|String|否|usage|标签键。仅在ShareType为Private时生效。

 N取值范围：1~20。 |
|Tag.N.Value|String|否|deploy|标签值。仅在ShareType为Private时生效。

 N取值范围：1~20。 |
|ShareType|String|否|Private|模板的共享类型。

 取值：

 -   Private（默认值）：模板为用户自己所拥有。
-   Shared：模板由其他用户所共享。 |

关于公共请求参数的详情，请参见[公共参数](~~131957~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C3A8413B-1F16-4DED-AC3E-61A00718DE8A|请求ID。 |
|PageSize|Integer|10|分页查询时设置的每页行数。 |
|PageNumber|Integer|1|模板列表的页码。

 起始值：1。 |
|TotalCount|Integer|1|模板总数。 |
|Templates|Array of Template| |模板列表。 |
|CreateTime|String|2019-10-15T08:17:14.000000|创建时间。 |
|Description|String|test-description|模板描述。 |
|OwnerId|String|123456789|模板所属阿里云账号ID。 |
|ShareType|String|Private|模板的共享类型。

 取值：

 -   Private：模板为用户自己所拥有。
-   Shared：模板由其他用户所共享。 |
|TemplateARN|String|acs:ros:\*:123456789:template/4d4f5aa2-3260-4e47-863b-763fbb12\*\*\*\*|模板的ARN。 |
|TemplateId|String|4d4f5aa2-3260-4e47-863b-763fbb12\*\*\*\*|模板ID。 |
|TemplateName|String|demo|模板名称。 |
|TemplateVersion|String|v1|模板最新版本名。 |
|UpdateTime|String|2019-10-15T08:17:14.000000|模板最后更新时间。 |

## 示例

请求示例

```
http(s)://ros.aliyuncs.com/?Action=ListTemplates
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListTemplatesResponse>
      <TotalCount>1</TotalCount>
      <RequestId>C3A8413B-1F16-4DED-AC3E-61A00718DE8A</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <Templates>
            <TemplateARN>acs:ros:*:123456789:template/4d4f5aa2-3260-4e47-863b-763fbb12****</TemplateARN>
            <Description>test-description</Description>
            <OwnerId>123456789</OwnerId>
            <CreateTime>2019-10-15T08:17:14.000000</CreateTime>
            <UpdateTime>2019-10-15T08:17:14.000000</UpdateTime>
            <TemplateVersion>v1</TemplateVersion>
            <TemplateName>demo</TemplateName>
            <TemplateId>4d4f5aa2-3260-4e47-863b-763fbb12****</TemplateId>
            <ShareType>Private</ShareType>
      </Templates>
</ListTemplatesResponse>
```

`JSON` 格式

```
{
  "TotalCount": "1",
  "RequestId": "C3A8413B-1F16-4DED-AC3E-61A00718DE8A",
  "PageSize": "10",
  "PageNumber": "1",
  "Templates": [
    {
      "TemplateARN": "acs:ros:*:123456789:template/4d4f5aa2-3260-4e47-863b-763fbb12****",
      "Description": "test-description",
      "OwnerId": "123456789",
      "CreateTime": "2019-10-15T08:17:14.000000",
      "UpdateTime": "2019-10-15T08:17:14.000000",
      "TemplateVersion": "v1",
      "TemplateName": "demo",
      "TemplateId": "4d4f5aa2-3260-4e47-863b-763fbb12****",
      "ShareType": "Private"
    }
  ]
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/ROS)查看更多错误码。


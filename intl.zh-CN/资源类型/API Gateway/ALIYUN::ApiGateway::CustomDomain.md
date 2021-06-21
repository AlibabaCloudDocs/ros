# ALIYUN::ApiGateway::CustomDomain

ALIYUN::ApiGateway::CustomDomain类型用于给指定分组绑定自定义域名和上传SSL证书。

**说明：**

-   SSL证书必须与自定义域名匹配。
-   绑定SSL证书后，可提供基于HTTPS的API服务。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::CustomDomain",
  "Properties": {
    "CertificateBody": String,
    "CertificateName": String,
    "GroupId": String,
    "CertificatePrivateKey": String,
    "DomainName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CertificateBody|String|否|是|证书内容|证书内容需要写到一行内，通过换行符`\n`进行换行。|
|CertificateName|String|否|是|SSL证书名称|无|
|GroupId|String|是|否|API分组ID|无|
|CertificatePrivateKey|String|否|是|证书私钥|无|
|DomainName|String|是|否|自定义域名|域名绑定失败时，请排查原因并重新绑定域名。更多信息，请参见[分组的域名绑定](https://www.alibabacloud.com/help/doc-detail/159014.html)。 |

## 返回值

Fn::GetAtt

CertificateId：证书ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "操作的分组"
    },
    "CertificateBody": {
      "Type": "String"
    },
    "CertificatePrivateKey": {
      "Type": "String"
    }
  },
  "Resources": {
    "CustomDomain": {
      "Type": "ALIYUN::ApiGateway::CustomDomain",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "DomainName": "mytest.api.domain",
        "CertificateName": "demo_cert",
        "CertificateBody": {
          "Ref": "CertificateBody"
        },
        "CertificatePrivateKey": {
          "Ref": "CertificatePrivateKey"
        }
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  GroupId:
    Type: String
    Description: 操作的分组
  CertificateBody:
    Type: String
  CertificatePrivateKey:
    Type: String
Resources:
  CustomDomain:
    Type: 'ALIYUN::ApiGateway::CustomDomain'
    Properties:
      GroupId:
        Ref: GroupId
      DomainName: mytest.api.domain
      CertificateName: demo_cert
      CertificateBody:
        Ref: CertificateBody
      CertificatePrivateKey:
        Ref: CertificatePrivateKey

```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/JSON/CustomDomain.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/YAML/CustomDomain.yml)。


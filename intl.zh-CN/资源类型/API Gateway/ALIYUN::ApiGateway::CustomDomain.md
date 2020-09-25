# ALIYUN::ApiGateway::CustomDomain

ALIYUN::ApiGateway::CustomDomain类型用于给指定分组绑定自定义域名和上传SSL证书。

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
|CertificateBody|String|否|是|证书内容|证书内容写到一行内，通过换行符`\n`进行换行。|
|CertificateName|String|否|是|SSL证书名称|无|
|GroupId|String|是|否|API分组ID|无|
|CertificatePrivateKey|String|否|是|证书私钥|无|
|DomainName|String|是|否|自定义域名|无|

## 返回值

Fn::GetAtt

CertificateId: 证书ID。

## 示例

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
    },
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


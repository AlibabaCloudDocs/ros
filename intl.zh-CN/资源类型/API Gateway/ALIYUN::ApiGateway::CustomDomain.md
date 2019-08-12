# ALIYUN::ApiGateway::CustomDomain {#concept_61479_zh .concept}

ALIYUN::ApiGateway::CustomDomain 类型可用于给指定分组绑定自定义域名和上传 SSL 证书。

## 语法 {#section_hcz_d11_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
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

## 属性 {#section_qda_4rd_65s .section}

|属性名称|类型|必须|允许更新|描述|
|CertificateBody|string|是|是|证书内容。|
|CertificateName|string|是|是|SSL 证书名称。|
|GroupId|string|是|否|API 分组 ID，系统生成，全局唯一。|
|CertificatePrivateKey|string|是|是|证书私钥。|
|DomainName|string|是|否|自定义域名。|

## 返回值 {#section_g17_9v0_039 .section}

**Fn::GetAtt**

CertificateId: 证书 ID

## 示例 {#section_s25_nh7_3nq .section}

``` {#codeblock_efu_1eq_p6u .language-json}
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


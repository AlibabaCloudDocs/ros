# ALIYUN::SLB::Certificate

ALIYUN::SLB::Certificate类型用于上传证书，支持ServerCertificate和CACertificate两种证书。

**说明：**

-   一次只能上传一份CA证书内容（"CertificateType": "CA"）。
-   一次只能上传一份服务器证书和对应的私钥（"CertificateType": "Server"）。

## 语法

```
{
  "Type": "ALIYUN::SLB::Certificate",
  "Properties": {
    "CertificateName": String,
    "Certificate": String,
    "AliCloudCertificateName": String,
    "PrivateKey": String,
    "ResourceGroupId": String,
    "CertificateType": String,
    "AliCloudCertificateId": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无|
|CertificateName|String|否|是|证书名称。|无|
|Certificate|String|是|否|需要上传证书的内容。|无|
|AliCloudCertificateName|String|否|否|阿里云的云上证书名称。|无|
|PrivateKey|String|否|否|需要上传的私钥。|无|
|AliCloudCertificateId|String|否|否|阿里云的云上证书ID。|使用阿里云的云上证书时，此参数为必选参数。|
|CertificateType|String|否|否|证书类型。|取值： -   Server
-   CA |
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_z3s_r27_j2u)。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   CertificateId：证书ID。
-   Fingerprint：证书的指纹。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "CertificateType": {
      "Type": "String",
      "Description": "The type of the certificate.",
      "AllowedValues": [
        "Server",
        "CA"
      ],
      "Default": "Server"
    },
    "AliCloudCertificateName": {
      "Type": "String",
      "Description": "The name of the Alibaba Cloud certificate."
    },
    "PrivateKey": {
      "Type": "String",
      "Description": "The private key."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "CertificateName": {
      "Type": "String",
      "Description": "The name of the certificate."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Certificate": {
      "Type": "String",
      "Description": "The content of the certificate public key."
    },
    "AliCloudCertificateId": {
      "Type": "String",
      "Description": "The ID of the Alibaba Cloud certificate."
    }
  },
  "Resources": {
    "SLBCertificate": {
      "Type": "ALIYUN::SLB::Certificate",
      "Properties": {
        "CertificateType": {
          "Ref": "CertificateType"
        },
        "AliCloudCertificateName": {
          "Ref": "AliCloudCertificateName"
        },
        "PrivateKey": {
          "Ref": "PrivateKey"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "CertificateName": {
          "Ref": "CertificateName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "Certificate": {
          "Ref": "Certificate"
        },
        "AliCloudCertificateId": {
          "Ref": "AliCloudCertificateId"
        }
      }
    }
  },
  "Outputs": {
    "Fingerprint": {
      "Description": "The fingerprint of the certificate.",
      "Value": {
        "Fn::GetAtt": [
          "SLBCertificate",
          "Fingerprint"
        ]
      }
    },
    "CertificateId": {
      "Description": "The ID of the certificate.",
      "Value": {
        "Fn::GetAtt": [
          "SLBCertificate",
          "CertificateId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  AliCloudCertificateId:
    Description: The ID of the Alibaba Cloud certificate.
    Type: String
  AliCloudCertificateName:
    Description: The name of the Alibaba Cloud certificate.
    Type: String
  Certificate:
    Description: The content of the certificate public key.
    Type: String
  CertificateName:
    Description: The name of the certificate.
    Type: String
  CertificateType:
    AllowedValues:
    - Server
    - CA
    Default: Server
    Description: The type of the certificate.
    Type: String
  PrivateKey:
    Description: The private key.
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  SLBCertificate:
    Properties:
      AliCloudCertificateId:
        Ref: AliCloudCertificateId
      AliCloudCertificateName:
        Ref: AliCloudCertificateName
      Certificate:
        Ref: Certificate
      CertificateName:
        Ref: CertificateName
      CertificateType:
        Ref: CertificateType
      PrivateKey:
        Ref: PrivateKey
      ResourceGroupId:
        Ref: ResourceGroupId
      Tags:
        Ref: Tags
    Type: ALIYUN::SLB::Certificate
Outputs:
  CertificateId:
    Description: The ID of the certificate.
    Value:
      Fn::GetAtt:
      - SLBCertificate
      - CertificateId
  Fingerprint:
    Description: The fingerprint of the certificate.
    Value:
      Fn::GetAtt:
      - SLBCertificate
      - Fingerprint
```

更多示例，请参见创建负载均衡监听、克隆负载均衡实例、上传证书、创建扩展域名、创建虚拟服务器组并添加后端服务器到负载均衡实例、为HTTP或HTTPS监听添加转发规则和将后端服务器添加到虚拟服务器组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml)。


# ALIYUN::RAM::SAMLProvider

ALIYUN::RAM::SAMLProvider类型用于创建角色SSO身份提供商。

## 语法

```
{
  "Type": "ALIYUN::RAM::SAMLProvider",
  "Properties": {
    "SAMLProviderName": String,
    "Description": String,
    "SAMLMetadataDocumentURL": String,
    "SAMLMetadataDocument": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SAMLProviderName|String|是|否|身份提供商名称。|最大长度为128个字符，可包含英文字母、数字和特殊字符`.-_`。不能以特殊字符`.-_`开头或结尾。|
|Description|String|否|是|备注。|无|
|SAMLMetadataDocumentURL|String|否|是|元数据文档地址。|大小为1～1024字节。必须指定SAMLMetadataDocumentURL或SAMLMetadataDocument，但不能同时指定二者。 |
|SAMLMetadataDocument|String|否|是|元数据文档内容。|大小为1～102,400字节。必须指定SAMLMetadataDocumentURL或SAMLMetadataDocument，但不能同时指定二者。 |

## 返回值

Fn::GetAtt

-   SAMLProviderName：身份提供商名称。
-   Arn：身份提供商的ARN。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SAMLProviderName": {
      "Type": "String",
      "Description": "IdP Name. The IdP name can contain a maximum of 128 characters and only letters, numbers, and the following special characters are accepted: hyphens (-), periods (.), and underscores (_). It cannot start or end with a special character.",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Description": {
      "Type": "String",
      "Description": "The description can contain a maximum of 256 characters.",
      "MaxLength": 256
    },
    "SAMLMetadataDocumentURL": {
      "Type": "String",
      "Description": "The URL for the file that contains the SAML metadata document. The URL must point to a document located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/document/demo and oss://ros/document/demo?RegionId=cn-hangzhou. The URL can be up to 1,024 bytes in length.",
      "MinLength": 1,
      "MaxLength": 1024
    },
    "SAMLMetadataDocument": {
      "Type": "String",
      "Description": "SAML metadata document. The content must be 1 to 102,400 bytes in length.You must specify one of the SAMLMetadataDocument and SAMLMetadataDocumentURL properties, but you cannot specify both of them.",
      "MinLength": 1,
      "MaxLength": 102400
    }
  },
  "Resources": {
    "SAMLProvider": {
      "Type": "ALIYUN::RAM::SAMLProvider",
      "Properties": {
        "SAMLProviderName": {
          "Ref": "SAMLProviderName"
        },
        "Description": {
          "Ref": "Description"
        },
        "SAMLMetadataDocumentURL": {
          "Ref": "SAMLMetadataDocumentURL"
        },
        "SAMLMetadataDocument": {
          "Ref": "SAMLMetadataDocument"
        }
      }
    }
  },
  "Outputs": {
    "SAMLProviderName": {
      "Description": "IdP Name.",
      "Value": {
        "Fn::GetAtt": [
          "SAMLProvider",
          "SAMLProviderName"
        ]
      }
    },
    "Arn": {
      "Description": "ARN.",
      "Value": {
        "Fn::GetAtt": [
          "SAMLProvider",
          "Arn"
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
  SAMLProviderName:
    Type: String
    Description: >-
      IdP Name. The IdP name can contain a maximum of 128 characters and only
      letters, numbers, and the following special characters are accepted:
      hyphens (-), periods (.), and underscores (_). It cannot start or end with
      a special character.
    MinLength: 1
    MaxLength: 128
  Description:
    Type: String
    Description: The description can contain a maximum of 256 characters.
    MaxLength: 256
  SAMLMetadataDocumentURL:
    Type: String
    Description: >-
      The URL for the file that contains the SAML metadata document. The URL
      must point to a document located in an HTTP or HTTPS web server or an
      Alibaba Cloud OSS bucket. Examples: oss://ros/document/demo and
      oss://ros/document/demo?RegionId=cn-hangzhou. The URL can be up to 1,024
      bytes in length.
    MinLength: 1
    MaxLength: 1024
  SAMLMetadataDocument:
    Type: String
    Description: >-
      SAML metadata document. The content must be 1 to 102,400 bytes in
      length.You must specify one of the SAMLMetadataDocument and
      SAMLMetadataDocumentURL properties, but you cannot specify both of them.
    MinLength: 1
    MaxLength: 102400
Resources:
  SAMLProvider:
    Type: 'ALIYUN::RAM::SAMLProvider'
    Properties:
      SAMLProviderName:
        Ref: SAMLProviderName
      Description:
        Ref: Description
      SAMLMetadataDocumentURL:
        Ref: SAMLMetadataDocumentURL
      SAMLMetadataDocument:
        Ref: SAMLMetadataDocument
Outputs:
  SAMLProviderName:
    Description: IdP Name.
    Value:
      'Fn::GetAtt':
        - SAMLProvider
        - SAMLProviderName
  Arn:
    Description: ARN.
    Value:
      'Fn::GetAtt':
        - SAMLProvider
        - Arn
```


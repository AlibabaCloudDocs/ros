# ALIYUN::RAM::SAMLProvider

ALIYUN::RAM::SAMLProvider is used to create an identity provider \(IdP\) for role-based single sign-on \(SSO\).

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SAMLProviderName|String|Yes|No|The name of the IdP.|The name can be up to 128 characters in length and can contain letters, digits, `periods (.), hyphens (-), and underscores (_)`. It cannot start or end with `a period (.), a hyphen (-), or an underscore (_)`.|
|Description|String|No|Yes|The description of the IdP.|None.|
|SAMLMetadataDocumentURL|String|No|Yes|The URL of the metadata document.|The URL must be 1 to 1,024 bytes in size.You must specify one of the SAMLMetadataDocumentURL and SAMLMetadataDocument parameters. |
|SAMLMetadataDocument|String|No|Yes|The content of the metadata document.|The document content must be 1 to 102,400 bytes in size.You must specify one of the SAMLMetadataDocumentURL and SAMLMetadataDocument parameters. |

## Response parameters

Fn::GetAtt

-   SAMLProviderName: the name of the IdP.
-   Arn: the Alibaba Cloud Resource Name \(ARN\) of the IdP.

## Examples

`JSON` format

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
      "Description": "The URL for the file that contains the SAML metadata document. The URL must point to a document located in an HTTP or HTTPS web server or an Alibaba Cloud OSS bucket. Examples: oss://ros/document/demo and oss://ros/document/demo? RegionId=cn-hangzhou. The URL can be up to 1,024 bytes in length.",
      "MinLength": 1,
      "MaxLength": 1024
    },
    "SAMLMetadataDocument": {
      "Type": "String",
      "Description": "SAML metadata document. The content must be 1 to 102,400 bytes in length. You must specify one of the SAMLMetadataDocument and SAMLMetadataDocumentURL properties, but you cannot specify both of them.",
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

`YAML` format

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
      oss://ros/document/demo? RegionId=cn-hangzhou. The URL can be up to 1,024
      bytes in length.
    MinLength: 1
    MaxLength: 1024
  SAMLMetadataDocument:
    Type: String
    Description: >-
      SAML metadata document. The content must be 1 to 102,400 bytes in
      length. You must specify one of the SAMLMetadataDocument and
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


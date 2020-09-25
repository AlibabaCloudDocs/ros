# ALIYUN::ApiGateway::CustomDomain

ALIYUN::ApiGateway::CustomDomain is used to bind a custom domain name and upload an SSL certificate to a specified API group.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|CertificateBody|String|No|Yes|The content of the certificate.|Certificate content is written as a single line and you can break the line by using the `\n` line break.|
|CertificateName|String|No|Yes|The name of the SSL certificate.|None.|
|GroupId|String|Yes|No|The ID of the API group to which the API belongs.|None.|
|CertificatePrivateKey|String|No|Yes|The private key of the SSL certificate.|None.|
|DomainName|String|Yes|No|The custom domain name.|None.|

## Response parameters

Fn::GetAtt

CertificateId: the ID of the certificate.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "The API group ID"
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


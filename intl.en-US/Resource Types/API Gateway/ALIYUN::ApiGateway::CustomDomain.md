# ALIYUN::ApiGateway::CustomDomain

ALIYUN::ApiGateway::CustomDomain is used to bind a custom domain name and upload an SSL certificate to a specified API group.

**Note:**

-   The SSL certificate must match the custom domain name.
-   After the SSL certificate is bound, HTTPS-based API services become available.

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
|CertificateName|String|No|Yes|The name of the SSL certificate.|None|
|GroupId|String|Yes|No|The ID of the API group.|None|
|CertificatePrivateKey|String|No|Yes|The private key of the SSL certificate.|None|
|DomainName|String|Yes|No|The custom domain name.|When a domain name fails to be bound, find the reasons and bind the domain name again. For more information, see [Bind a wildcard domain name to an API group](https://www.alibabacloud.com/help/doc-detail/159014.html). |

## Response parameters

Fn::GetAtt

CertificateId: the ID of the certificate.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "the ID of the API group"
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  GroupId:
    Type: String
    Description: the ID of the API group
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

To view more examples, visit [CustomDomain.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/JSON/CustomDomain.json) and [CustomDomain.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/YAML/CustomDomain.yml).


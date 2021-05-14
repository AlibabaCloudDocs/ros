# ALIYUN::SLB::Certificate

ALIYUN::SLB::Certificate is used to upload a certificate to a Server Load Balancer \(SLB\) instance. Server certificates and CA certificates are supported.

**Note:**

-   You can upload only a single CA certificate at a time \("CertificateType": "CA "\).
-   You can upload only a single server certificate and its corresponding private key at a time \("CertificateType": "Server "\).

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|CertificateName|String|No|Yes|The name of the certificate.|None|
|Certificate|String|Yes|No|The CA certificate to be uploaded.|None|
|AliCloudCertificateName|String|No|No|The name of the Alibaba Cloud certificate.|None|
|PrivateKey|String|No|No|The private key to be uploaded.|None|
|AliCloudCertificateId|String|No|No|The ID of the Alibaba Cloud certificate.|This parameter is required if you use a certificate from Alibaba Cloud SSL Certificates Service.|
|CertificateType|String|No|No|The type of the certificate.|Valid values: -   Server
-   CA |
|Tags|List|No|Yes|The tags of the certificate.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_z3s_r27_j2u) section in this topic. |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   CertificateId: the ID of the certificate.
-   Fingerprint: the fingerprint of the certificate.

## Examples

`JSON` format

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

`YAML` format

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

For more examples, visit [Listener.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json) and [Listener.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml). In the examples, the ALIYUN::SLB::Listener, ALIYUN::SLB::LoadBalancerClone, ALIYUN::SLB::Certificate, ALIYUN::SLB::DomainExtension, ALIYUN::SLB::VServerGroup, ALIYUN::SLB::Rule, and ALIYUN::SLB::BackendServerToVServerGroupAddition resource types are involved.


# ALIYUN::CDN::Domain

ALIYUN::CDN::Domain is used to add a domain name for CDN.

**Note:**

-   Before you add a domain name for CDN, you must activate the Alibaba Cloud Content Delivery Network \(CDN\) service. For more information, see [Activate Alibaba Cloud CDN](/intl.en-US/Quick Start/Activate Alibaba Cloud CDN.md).
-   Your accelerated domain name must be ICP filed.
-   You can add only a single domain name to Alibaba Cloud CDN in each call. You can add a maximum of 50 domain names for CDN within each Alibaba Cloud account.
-   If the content of the origin server is not stored on Alibaba Cloud, the content must be reviewed. The review is completed by the end of the next business day after you submit the application.
-   The maximum number of times that each user can call this operation per second is 30.

## Syntax

```
{
  "Type": "ALIYUN::CDN::Domain",
  "Properties": {
    "CdnType": String,
    "Sources": String,
    "CheckUrl": String,
    "DomainName": String,
    "ResourceGroupId": String,
    "Scope": String,
    "TopLevelDomain": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|CdnType|String|Yes|No|The business type of the domain name.|Valid values: -   web: images and small files.
-   download: downloads of large files.
-   video: on-demand video and audio streaming. |
|Sources|String|No|Yes|The information about the origin server.|Example: `[{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80,"weight":"15"}]`.|
|CheckUrl|String|No|No|The URL that is used for health checks.|Example: `www.yourdomain.com/test.html`.|
|DomainName|String|Yes|No|The domain names that you want to add to Alibaba Cloud CDN.|Wildcard domain names are supported. A wildcard domain name must start with a period \(.\). Example: `.example.com`. |
|ResourceGroupId|String|No|Yes|The ID of the resource group.|None|
|Scope|String|No|No|The accelerated region.|Default value: domestic. Valid values:-   domestic: regions inside mainland China.
-   overseas: regions outside mainland China.
-   global: all regions both inside and outside mainland China. |
|TopLevelDomain|String|No|Yes|The top-level domain name.|Example: `www.yourTopLevelDomain`.|
|Tags|List|No|Yes|The tags of the domain name.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_ou8_h7a_6nx). |

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
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   DomainName: the domain name to be accelerated by CDN.
-   Cname: the alias of the domain name for CDN. A Canonical Name \(CNAME\) record is provided to the Domain Name System \(DNS\) to map the alias to the canonical name.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "CheckUrl": {
      "Type": "String",
      "Description": "The validation of the origin."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group. If this is left blank, the system automatically fills in the ID of the default resource group."
    },
    "Scope": {
      "Type": "String",
      "Description": "Valid values: domestic, overseas, and global. Default value: domestic. The setting is supported for users outside mainland China, users in mainland China of level 3 or above."
    },
    "DomainName": {
      "Type": "String",
      "Description": "The CDN domain name. Wildcard domain names that start with periods (.) are supported. For example, .a.com."
    },
    "CdnType": {
      "Type": "String",
      "Description": "The business type. Valid values: web, download, video, livestream, and httpsdelivery. web: acceleration of images and small files download. download: acceleration of large file downloads. video: live streaming acceleration. httpsdelivery: SSL acceleration for HTTPS.",
      "AllowedValues": [
        "video",
        "download",
        "web",
        "liveStream"
      ]
    },
    "TopLevelDomain": {
      "Type": "String",
      "Description": "The top-level domain, which can only be configured by users on the whitelist."
    },
    "Sources": {
      "Type": "String",
      "Description": "The list of origin URLs."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "Domain": {
      "Type": "ALIYUN::CDN::Domain",
      "Properties": {
        "CheckUrl": {
          "Ref": "CheckUrl"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "Scope": {
          "Ref": "Scope"
        },
        "DomainName": {
          "Ref": "DomainName"
        },
        "CdnType": {
          "Ref": "CdnType"
        },
        "TopLevelDomain": {
          "Ref": "TopLevelDomain"
        },
        "Sources": {
          "Ref": "Sources"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "DomainName": {
      "Description": "The CDN domain name. Wildcard domain names that start with periods (.) are supported. For example, .a.com.",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DomainName"
        ]
      }
    },
    "Cname": {
      "Description": "The CNAME generated for the CDN domain.You must add a CNAME record with your DNS provider to map the CDN domain name to the CNAME.",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "Cname"
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
  CdnType:
    AllowedValues:
    - video
    - download
    - web
    - liveStream
    Description: 'The business type. Valid values: web, download, video, livestream,
      and httpsdelivery. web: acceleration of images and small files download. download:
      acceleration of large file downloads. video: live streaming acceleration. httpsdelivery:
      SSL acceleration for HTTPS.'
    Type: String
  CheckUrl:
    Description: The validation of the origin.
    Type: String
  DomainName:
    Description: The CDN domain name. Wildcard domain names that start with periods
      (.) are supported. For example, .a.com.
    Type: String
  ResourceGroupId:
    Description: The ID of the resource group. If this is left blank, the system automatically
      fills in the ID of the default resource group.
    Type: String
  Scope:
    Description: 'Valid values: domestic, overseas, and global. Default value: domestic.
      The setting is supported for users outside mainland China, users in mainland
      China of level 3 or above.'
    Type: String
  Sources:
    Description: The list of origin URLs.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  TopLevelDomain:
    Description: The top-level domain, which can only be configured by users on the
      whitelist.
    Type: String
Resources:
  Domain:
    Properties:
      CdnType:
        Ref: CdnType
      CheckUrl:
        Ref: CheckUrl
      DomainName:
        Ref: DomainName
      ResourceGroupId:
        Ref: ResourceGroupId
      Scope:
        Ref: Scope
      Sources:
        Ref: Sources
      Tags:
        Ref: Tags
      TopLevelDomain:
        Ref: TopLevelDomain
    Type: ALIYUN::CDN::Domain
Outputs:
  Cname:
    Description: The CNAME generated for the CDN domain.You must add a CNAME record
      with your DNS provider to map the CDN domain name to the CNAME.
    Value:
      Fn::GetAtt:
      - Domain
      - Cname
  DomainName:
    Description: The CDN domain name. Wildcard domain names that start with periods
      (.) are supported. For example, .a.com.
    Value:
      Fn::GetAtt:
      - Domain
      - DomainName
```

For more examples, visit [Domain.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CDN/JSON/Domain.json) and [Domain.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CDN/YAML/Domain.yml). In the examples, the ALIYUN::CDN::Domain and ALIYUN::CDN::DomainConfig resources are involved.


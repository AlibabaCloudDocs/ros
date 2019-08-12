# ALIYUN::CDN::Domain {#concept_y23_vk3_fhb .concept}

ALIYUN::CDN::Domain is used to add an accelerated domain. You can submit only one accelerated domain at a time. You can add a maximum of 20 accelerated domains.

**Note:** 

Limits:

-   Before adding an accelerated domain, you must activate the CDN service.
-   Your accelerated domain must be ICP filed.
-   If the content of the origin site is not on the Alibaba Cloud platform, it will be reviewed. The review will be completed on the next working day after you submit the application.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CDN::Domain",
  "Properties": {
    "CdnType": String,
    "Sources": String,
    "CheckUrl": String,
    "DomainName": String,
    "ResourceGroupId": String,
    "Scope": String,
    "TopLevelDomain": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CdnType|String|Yes|No|The business type of the accelerated domain.|Valid values: -   web: the distribution of images and small files.
-   download: the acceleration of large file downloads.
-   video: the acceleration of videos and audios on demand.
-   liveStream: the acceleration of live streaming media.

 |
|Sources|String|No|Yes|The list of origin URLs.|None|
|CheckUrl|String|No|No|The origin validation URL.|None|
|DomainName|String|Yes|No|The domain name to be accelerated by CDN. Wildcard domain names that start with periods \(.\) are supported. For example, .a.com.|None|
|ResourceGroupId|String|No|Yes|The ID of the resource group.|None|
|Scope|String|No|No|Valid values: -   domestic
-   overseas
-   global

 Default value: domestic. This parameter is applicable to domestic users of level 3 or higher and international users.

 |None|
|TopLevelDomain|String|No|Yes|The top-level scheduling domain.|None|

## Response parameters {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

DomainName: the domain name to be accelerated by CDN. Wildcard domain names that start with periods \(.\) are supported. For example, .a.com.

## Examples {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Domain": {
      "Type": "ALIYUN::CDN::Domain",
      "Properties": {
        "CdnType": {
          "Ref": "CdnType"
        },
        "Sources": {
          "Ref": "Sources"
        },
        "CheckUrl": {
          "Ref": "CheckUrl"
        },
        "DomainName": {
          "Ref": "DomainName"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "Scope": {
          "Ref": "Scope"
        },
        "TopLevelDomain": {
          "Ref": "TopLevelDomain"
        }
      }
    }
  },
  "Parameters": {
    "CdnType": {
      "Type": "String",
      "Description": "The business type. Valid values: web, download, video, livestream, and httpsdelivery. web: the acceleration of images and small files download. download: the acceleration of large file downloads. video: live streaming acceleration. httpsdelivery: SSL acceleration for HTTPS. ",
      "AllowedValues": [
        "video",
        "download",
        "web",
        "liveStream"
      ]
    },
    "Sources": {
      "Type": "String",
      "Description": "The list of origin URLs."
    },
    "CheckUrl": {
      "Type": "String",
      "Description": "The validation of the origin."
    },
    "DomainName": {
      "Type": "String",
      "Description": "The CDN domain name. Wildcard domain names that start with periods (.) are supported. For example, .a.com."
    },
    "ResourceGroupId":"",
      "Type": "String",
      "Description": "The ID of the resource group. If this is left blank, the system automatically fills in the ID of the default resource group."
    },
    "Scope": {
      "Type": "String",
      "Description": "Valid values: domestic, overseas, and global. Default value: domestic. The setting is supported for users outside mainland China, users in mainland China of level 3 or above."
    },
    "TopLevelDomain": {
      "Type": "String",
      "Description": "The top-level domain, which can only be configured by users on the whitelist."
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
    }
  }
}
```


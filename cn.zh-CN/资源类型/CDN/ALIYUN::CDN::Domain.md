# ALIYUN::CDN::Domain {#concept_y23_vk3_fhb .concept}

ALIYUN::CDN::Domain 类型用于添加加速域名时，您一次只能提交一个加速域名。您最多可以添加20个域名。

**说明：** 

限制条件：

-   创建加速域名之前，请先开通CDN服务。
-   您的加速域名必须完成备案。
-   如果您的源站内容不在阿里云平台上，则需要审核。审核会在下一个工作日前完成。

## 语法 {#section_xyg_tn2_lfb .section}

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

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CdnType|String|是|否|加速域名的业务类型。|取值范围： -   web：图片及小文件分发。
-   download：大文件下载加速。
-   video：视音频点播加速。
-   liveStream：直播流媒体加速。

 |
|Sources|String|否|是|回源地址列表。|无。|
|CheckUrl|String|否|否|源站健康检查。|无。|
|DomainName|String|是|否|需要接入CDN的域名。支持泛域名，以符号“.”开头，如：.a.com。|无。|
|ResourceGroupId|String|否|是|资源组ID。|无。|
|Scope|String|否|否|取值范围： -   domestic
-   overseas
-   global

 默认值： domestic。国际用户、国内L3及以上用户设置有效。

 |无。|
|TopLevelDomain|String|否|是|顶级调度域。|无。|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

DomainName：需要接入CDN的域名。支持泛域名，以符号“.”开头，如：.a.com。

## 示例 {#section_klp_54n_4fb .section}

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
      "Description": "The business type. Valid values: web, download, video, livestream, and httpsdelivery. web: acceleration of images and small files download. download: acceleration of large file downloads. video: live streaming acceleration. httpsdelivery: SSL acceleration for HTTPS.",
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
    "ResourceGroupId": {
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


# ALIYUN::CDN::Domain

ALIYUN::CDN::Domain类型用于添加加速域名。

**说明：**

-   创建加速域名之前，请先开通CDN服务。具体操作，请参见[开通CDN服务](/cn.zh-CN/快速入门/开通CDN服务.md)。
-   您的加速域名必须完成备案。
-   每次只能添加一个加速域名，每个用户最多支持添加50个加速域名。
-   源站内容如果不在阿里云平台上，需进行审核，审核工作会在下一个工作日前完成。
-   单个用户的调用频率为30次/秒。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CdnType|String|是|否|加速域名的业务类型。|取值： -   web：图片小文件。
-   download：大文件下载。
-   video：视音频点播。 |
|Sources|String|否|是|回源地址列表。|示例值：`[{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80,"weight":"15"}]`。|
|CheckUrl|String|否|否|健康检测URL。|示例值：`www.yourdomain.com/test.html`。|
|DomainName|String|是|否|需要接入CDN的加速域名。|支持泛域名。以半角句号（.）开头。示例值：`.example.com`。 |
|ResourceGroupId|String|否|是|资源组ID。|无|
|Scope|String|否|否|加速区域。|取值：-   domestic（默认值）：仅中国内地。
-   overseas：全球（不包含中国内地）。
-   global：全球。 |
|TopLevelDomain|String|否|是|顶级接入域。|示例值：`www.yourTopLevelDomain`。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_ou8_h7a_6nx)。 |

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

-   DomainName：接入CDN的域名。
-   Cname：CDN域名的别名。向DNS提供CNAME，以便将CDN域名映射到CNAME。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见添加加速域名和批量配置域名的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CDN/JSON/Domain.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CDN/YAML/Domain.yml)。


# ALIYUN::DNS::Domain

ALIYUN::DNS::Domain类型用于添加域名。

## 语法

```
{
  "Type": "ALIYUN::DNS::Domain",
  "Properties": {
    "GroupId": String,
    "DomainName": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupId|String|否|是|域名分组ID。|无|
|DomainName|String|是|否|域名名称。|无|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_7dm_5pp_k5j)。 |

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

-   DomainId：域名ID。
-   DomainName：域名名称。
-   GroupId：域名分组ID。
-   GroupName：域名分组名称。
-   PunyCode：只针对中文域名返回punycode码。
-   DnsServers：域名在解析系统中的DNS列表。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DomainName": {
      "Type": "String",
      "Description": "Domain name"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "GroupId": {
      "Type": "String",
      "Description": "Domain name grouping, the default is the \"default grouping\" GroupId"
    }
  },
  "Resources": {
    "Domain": {
      "Type": "ALIYUN::DNS::Domain",
      "Properties": {
        "DomainName": {
          "Ref": "DomainName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "GroupId": {
          "Ref": "GroupId"
        }
      }
    }
  },
  "Outputs": {
    "GroupName": {
      "Description": "The name of the domain name group",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "GroupName"
        ]
      }
    },
    "DomainId": {
      "Description": "Domain ID",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DomainId"
        ]
      }
    },
    "DomainName": {
      "Description": "Domain name",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DomainName"
        ]
      }
    },
    "PunyCode": {
      "Description": "punycode returned only for a Chinese domain name",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "PunyCode"
        ]
      }
    },
    "DnsServers": {
      "Description": "The DNS list for the domain name under resolution",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DnsServers"
        ]
      }
    },
    "GroupId": {
      "Description": "Domain name group ID",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "GroupId"
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
  DomainName:
    Description: Domain name
    Type: String
  GroupId:
    Description: Domain name grouping, the default is the "default grouping" GroupId
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  Domain:
    Properties:
      DomainName:
        Ref: DomainName
      GroupId:
        Ref: GroupId
      Tags:
        Ref: Tags
    Type: ALIYUN::DNS::Domain
Outputs:
  DnsServers:
    Description: The DNS list for the domain name under resolution
    Value:
      Fn::GetAtt:
      - Domain
      - DnsServers
  DomainId:
    Description: Domain ID
    Value:
      Fn::GetAtt:
      - Domain
      - DomainId
  DomainName:
    Description: Domain name
    Value:
      Fn::GetAtt:
      - Domain
      - DomainName
  GroupId:
    Description: Domain name group ID
    Value:
      Fn::GetAtt:
      - Domain
      - GroupId
  GroupName:
    Description: The name of the domain name group
    Value:
      Fn::GetAtt:
      - Domain
      - GroupName
  PunyCode:
    Description: punycode returned only for a Chinese domain name
    Value:
      Fn::GetAtt:
      - Domain
      - PunyCode
```

更多示例，请参见添加域名和添加域名分组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DNS/JSON/Domain.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DNS/YAML/Domain.yml)。


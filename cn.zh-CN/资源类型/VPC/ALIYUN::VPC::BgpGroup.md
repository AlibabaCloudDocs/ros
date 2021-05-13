# ALIYUN::VPC::BgpGroup

ALIYUN::VPC::BgpGroup类型用于为指定的边界路由器（VBR）创建一个BGP（多线）组。

您可以通过BGP实现边界路由器与本地数据中心（IDC）的互通。每个BGP组关联一个VBR，您仅需将与VBR通信的BGP邻居添加到对应的BGP组中，然后在VBR中宣告BGP网络即可。BGP组主要用于简化BGP配置，您可以将需要不断重复的配置合并到一个组中，减少配置复杂度。您需根据AS号码建立一个BGP组。

**说明：**

-   BGP组支持的BGP版本为BGP4。
-   BGP组支持IPv4 BGP，不支持IPv6 BGP。

## 语法

```
{
  "Type": "ALIYUN::VPC::BgpGroup",
  "Properties": {
    "Description": String,
    "LocalAsn": Integer,
    "AuthKey": String,
    "RouterId": String,
    "PeerAsn": Integer,
    "IsFakeAsn": Boolean,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|BGP组的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|LocalAsn|Integer|否|是|云上设备的AS号码。|无|
|AuthKey|String|否|是|BGP组的认证密钥。|无|
|RouterId|String|是|否|边界路由器ID。|无|
|PeerAsn|Integer|是|是|本地设备的AS号码。|无|
|IsFakeAsn|Boolean|否|是|AS号码是否为假。|取值：-   true
-   false |
|Name|String|否|是|BGP组的名称。|长度为2~128个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|

## 返回值

Fn::GetAtt

-   BgpGroupId：BGP组的ID。
-   Name：BGP组的名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the BGP group. The description must be 2 to 256 characters in length.\nIt must start with a letter but cannot start with http:// or https://."
    },
    "LocalAsn": {
      "Type": "Number",
      "Description": "The AS number on the Alibaba Cloud side."
    },
    "AuthKey": {
      "Type": "String",
      "Description": "The authentication key of the BGP group."
    },
    "RouterId": {
      "Type": "String",
      "Description": "The ID of the VBR."
    },
    "PeerAsn": {
      "Type": "Number",
      "Description": "The AS number of the BGP peer."
    },
    "IsFakeAsn": {
      "Type": "Boolean",
      "Description": "A router that runs BGP typically belongs to only one AS. In some cases, for example,\nthe AS needs to be migrated or is merged with another AS, a new AS number replaces\nthe original one.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the BGP group. The name must be 2 to 128 characters in length and can\ncontain digits, periods (.), underscores (_), and hyphens (-). The name must start\nwith a letter but cannot start with http:// or https://."
    }
  },
  "Resources": {
    "BgpGroup": {
      "Type": "ALIYUN::VPC::BgpGroup",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "LocalAsn": {
          "Ref": "LocalAsn"
        },
        "AuthKey": {
          "Ref": "AuthKey"
        },
        "RouterId": {
          "Ref": "RouterId"
        },
        "PeerAsn": {
          "Ref": "PeerAsn"
        },
        "IsFakeAsn": {
          "Ref": "IsFakeAsn"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "BgpGroupId": {
      "Description": "The ID of the BGP group.",
      "Value": {
        "Fn::GetAtt": [
          "BgpGroup",
          "BgpGroupId"
        ]
      }
    },
    "Name": {
      "Description": "The name of the BGP group.",
      "Value": {
        "Fn::GetAtt": [
          "BgpGroup",
          "Name"
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
  AuthKey:
    Description: The authentication key of the BGP group.
    Type: String
  Description:
    Description: 'The description of the BGP group. The description must be 2 to 256
      characters in length.

      It must start with a letter but cannot start with http:// or https://.'
    Type: String
  IsFakeAsn:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'A router that runs BGP typically belongs to only one AS. In some
      cases, for example,

      the AS needs to be migrated or is merged with another AS, a new AS number replaces

      the original one.'
    Type: Boolean
  LocalAsn:
    Description: The AS number on the Alibaba Cloud side.
    Type: Number
  Name:
    Description: 'The name of the BGP group. The name must be 2 to 128 characters
      in length and can

      contain digits, periods (.), underscores (_), and hyphens (-). The name must
      start

      with a letter but cannot start with http:// or https://.'
    Type: String
  PeerAsn:
    Description: The AS number of the BGP peer.
    Type: Number
  RouterId:
    Description: The ID of the VBR.
    Type: String
Resources:
  BgpGroup:
    Properties:
      AuthKey:
        Ref: AuthKey
      Description:
        Ref: Description
      IsFakeAsn:
        Ref: IsFakeAsn
      LocalAsn:
        Ref: LocalAsn
      Name:
        Ref: Name
      PeerAsn:
        Ref: PeerAsn
      RouterId:
        Ref: RouterId
    Type: ALIYUN::VPC::BgpGroup
Outputs:
  BgpGroupId:
    Description: The ID of the BGP group.
    Value:
      Fn::GetAtt:
      - BgpGroup
      - BgpGroupId
  Name:
    Description: The name of the BGP group.
    Value:
      Fn::GetAtt:
      - BgpGroup
      - Name
```


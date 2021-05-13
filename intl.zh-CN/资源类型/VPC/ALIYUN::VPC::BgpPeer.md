# ALIYUN::VPC::BgpPeer

ALIYUN::VPC::BgpPeer类型用于向指定的BGP组中添加BGP邻居。

## 语法

```
{
  "Type": "ALIYUN::VPC::BgpPeer",
  "Properties": {
    "PeerIpAddress": String,
    "EnableBfd": Boolean,
    "BgpGroupId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PeerIpAddress|String|否|是|BGP邻居的IP地址。|无|
|EnableBfd|Boolean|否|是|是否开启BFD功能。|取值：-   true：开启。
-   false：不开启。 |
|BgpGroupId|String|是|否|BGP组的ID。|无|

## 返回值

Fn::GetAtt

BgpPeerId：BGP邻居的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeerIpAddress": {
      "Type": "String",
      "Description": "The IP address of the BGP peer."
    },
    "EnableBfd": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable the Bidirectional Forwarding Detection (BFD) feature.\nValid values:\ntrue: enables BFD.\nfalse: disables BFD.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "BgpGroupId": {
      "Type": "String",
      "Description": "The ID of the BGP group."
    }
  },
  "Resources": {
    "BgpPeer": {
      "Type": "ALIYUN::VPC::BgpPeer",
      "Properties": {
        "PeerIpAddress": {
          "Ref": "PeerIpAddress"
        },
        "EnableBfd": {
          "Ref": "EnableBfd"
        },
        "BgpGroupId": {
          "Ref": "BgpGroupId"
        }
      }
    }
  },
  "Outputs": {
    "BgpPeerId": {
      "Description": "The ID of the BGP peer.",
      "Value": {
        "Fn::GetAtt": [
          "BgpPeer",
          "BgpPeerId"
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
  BgpGroupId:
    Description: The ID of the BGP group.
    Type: String
  EnableBfd:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether to enable the Bidirectional Forwarding Detection
      (BFD) feature.

      Valid values:

      true: enables BFD.

      false: disables BFD.'
    Type: Boolean
  PeerIpAddress:
    Description: The IP address of the BGP peer.
    Type: String
Resources:
  BgpPeer:
    Properties:
      BgpGroupId:
        Ref: BgpGroupId
      EnableBfd:
        Ref: EnableBfd
      PeerIpAddress:
        Ref: PeerIpAddress
    Type: ALIYUN::VPC::BgpPeer
Outputs:
  BgpPeerId:
    Description: The ID of the BGP peer.
    Value:
      Fn::GetAtt:
      - BgpPeer
      - BgpPeerId
```


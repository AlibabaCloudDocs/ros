# ALIYUN::VPC::BgpPeer

ALIYUN::VPC::BgpPeer is used to add a Border Gateway Protocol \(BGP\) peer to a specific BGP group.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PeerIpAddress|String|No|Yes|The IP address of the BGP peer.|None|
|EnableBfd|Boolean|No|Yes|Specifies whether to enable the Bidirectional Forwarding Detection \(BFD\) feature.|Valid values:-   true: BFD is enabled.
-   false: BFD is disabled. |
|BgpGroupId|String|Yes|No|The ID of the BGP group.|None|

## Response parameters

Fn::GetAtt

BgpPeerId: the ID of the BGP peer.

## Examples

`JSON` format

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

`YAML` format

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


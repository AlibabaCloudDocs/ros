# ALIYUN::VPC::BgpGroup

ALIYUN::VPC::BgpGroup is used to create a Border Gateway Protocol \(BGP\) \(Multi-ISP\) group for a specified virtual border router \(VBR\).

BGP groups allow VBRs to communicate with data centers. Each BGP group is associated with a VBR. You can add a BGP peer that needs to communicate with a VBR to the corresponding BGP group and advertise the BGP network in the VBR. BGP groups are used to simplify BGP configurations. You can reduce the configuration complexity by adding BGP peers that use the same configurations to one BGP group. You must use an autonomous system \(AS\) number to create a BGP group.

**Note:**

-   Only BGP4 is supported by the BGP groups.
-   BGP groups support IPv4 BGP. IPv6 BGP is not supported.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the BGP group.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|LocalAsn|Integer|No|Yes|The AS number of the cloud device.|None|
|AuthKey|String|No|Yes|The authentication key of the BGP group.|None|
|RouterId|String|Yes|No|The ID of the VBR.|None|
|PeerAsn|Integer|No|Yes|The AS number of the on-premises device.|None|
|IsFakeAsn|Boolean|No|Yes|Specifies whether the AS number is fake.|Valid values:-   true
-   false |
|Name|String|No|Yes|The name of the BGP group.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   BgpGroupId: the ID of the BGP group.
-   Name: the name of the BGP group.

## Examples

`JSON` format

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

`YAML` format

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


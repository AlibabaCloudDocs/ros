# ALIYUN::ECS::VSwitch

ALIYUN::ECS::VSwitch is used to create a VSwitch.

## Syntax

```
{
  "Type": "ALIYUN::ECS::VSwitch",
  "Properties": {
    "VSwitchName": String,
    "VpcId": String,
    "Description": String,
    "Tags": List,
    "Ipv6CidrBlock": Integer,
    "ZoneId": String,
    "CidrBlock": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|Yes|No|The ID of the VPC where the VSwitch is created.|None|
|ZoneId|String|Yes|No|The ID of the zone.|None|
|VSwitchName|String|No|Yes|The name of the VSwitch.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|CidrBlock|String|Yes|No|The CIDR block of the VSwitch.|The VSwitch CIDR block must be a subset of the CIDR block assigned to the VPC where the VSwitch resides and cannot be in use by other VSwitches.|
|Description|String|No|Yes|The description of the VSwitch.|It must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Ipv6CidrBlock|Integer|No|No|The IPv6 CIDR block of the VSwitch.|Valid values: 0 to 255. The value is a decimal integer. By default, the prefix of the IPv6 CIDR block of the VSwitch is set to /64.

You can customize the last eight bits of the IPv6 CIDR block. |
|Tags|List|No|No|The tag of the VSwitch. Example: `[{"Key": "VswTag", "Value": ""}]`.|A maximum of 20 tags can be specified. Each tag is a key-value pair. The tag value can be left empty. For more information, see [Tags properties](#section_m42_j24_e31). |

## Tags syntax

```
"Tags": [
  {
    "Value": String,
    "Key": String
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

-   VSwitchId: the VSwitch ID allocated by the system.
-   CidrBlock: the IPv4 CIDR block of the VSwitch.
-   Ipv6CidrBlock: the IPv6 CIDR block of the VSwitch.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the VSwitch, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "VpcId": {
      "Type": "String",
      "Description": "VPC id to create vswtich."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The availability zone in which the VSwitch will be created."
    },
    "CidrBlock": {
      "Type": "String",
      "Description": "CIDR Block of created VSwitch, It must belong to itself VPC CIDR block."
    },
    "VSwitchName": {
      "Type": "String",
      "Description": "Display name of the vSwitch instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "Ipv6CidrBlock": {
      "Type": "Number",
      "Description": "The IPv6 network segment of the switch supports the last 8 bits of the VPC IPv6 network segment. Value: 0-255 (decimal).\nThe IPv6 segment mask of the switch defaults to 64 bits.",
      "MinValue": 0,
      "MaxValue": 255
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to vswitch. Max support 20 tags to add during create vswitch. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "VSwitch": {
      "Type": "ALIYUN::ECS::VSwitch",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "CidrBlock": {
          "Ref": "CidrBlock"
        },
        "VSwitchName": {
          "Ref": "VSwitchName"
        },
        "Ipv6CidrBlock": {
          "Ref": "Ipv6CidrBlock"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "VSwitchId": {
      "Description": "Id of created VSwitch.",
      "Value": {
        "Fn::GetAtt": [
          "VSwitch",
          "VSwitchId"
        ]
      }
    },
    "CidrBlock": {
      "Description": "CIDR Block of created VSwitch",
      "Value": {
        "Fn::GetAtt": [
          "VSwitch",
          "CidrBlock"
        ]
      }
    },
    "Ipv6CidrBlock": {
      "Description": "The IPv6 network segment of the VSwitch",
      "Value": {
        "Fn::GetAtt": [
          "VSwitch",
          "Ipv6CidrBlock"
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
  Description:
    Type: String
    Description: >-
      Description of the VSwitch, [2, 256] characters. Do not fill or empty, the
      default is empty.
  VpcId:
    Type: String
    Description: VPC id to create vswtich.
  ZoneId:
    Type: String
    Description: The availability zone in which the VSwitch will be created.
  CidrBlock:
    Type: String
    Description: 'CIDR Block of created VSwitch, It must belong to itself VPC CIDR block.'
  VSwitchName:
    Type: String
    Description: >-
      Display name of the vSwitch instance, [2, 128] English or Chinese
      characters, must start with a letter or Chinese in size, can contain
      numbers, '_' or '.', '-'
  Ipv6CidrBlock:
    Type: Number
    Description: >-
      The IPv6 network segment of the switch supports the last 8 bits of the VPC
      IPv6 network segment. Value: 0-255 (decimal).

      The IPv6 segment mask of the switch defaults to 64 bits.
    MinValue: 0
    MaxValue: 255
  Tags:
    Type: Json
    Description: >-
      Tags to attach to vswitch. Max support 20 tags to add during create
      vswitch. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
Resources:
  VSwitch:
    Type: 'ALIYUN::ECS::VSwitch'
    Properties:
      Description:
        Ref: Description
      VpcId:
        Ref: VpcId
      ZoneId:
        Ref: ZoneId
      CidrBlock:
        Ref: CidrBlock
      VSwitchName:
        Ref: VSwitchName
      Ipv6CidrBlock:
        Ref: Ipv6CidrBlock
      Tags:
        Ref: Tags
Outputs:
  VSwitchId:
    Description: Id of created VSwitch.
    Value:
      'Fn::GetAtt':
        - VSwitch
        - VSwitchId
  CidrBlock:
    Description: CIDR Block of created VSwitch
    Value:
      'Fn::GetAtt':
        - VSwitch
        - CidrBlock
  Ipv6CidrBlock:
    Description: The IPv6 network segment of the VSwitch
    Value:
      'Fn::GetAtt':
        - VSwitch
        - Ipv6CidrBlock
```


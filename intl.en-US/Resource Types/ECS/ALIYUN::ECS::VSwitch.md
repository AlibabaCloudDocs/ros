# ALIYUN::ECS::VSwitch

ALIYUN::ECS::VSwitch is used to create a vSwitch.

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
|VpcId|String|Yes|No|The ID of the virtual private cloud \(VPC\) where the vSwitch is to be created.|None|
|ZoneId|String|Yes|No|The ID of the zone.|None|
|VSwitchName|String|No|Yes|The name of the vSwitch.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|CidrBlock|String|Yes|No|The CIDR block of the vSwitch.|The vSwitch CIDR block must be a subset of the CIDR block assigned to the VPC where the vSwitch resides and cannot be used by other vSwitches.|
|Description|String|No|Yes|The description of the vSwitch.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|Ipv6CidrBlock|Integer|No|No|The IPv6 CIDR block of the vSwitch.|Valid values: 0 to 255. The value is a decimal integer. By default, the prefix of the IPv6 CIDR block of the vSwitch is set to /64.

You can customize the last eight bits of the IPv6 CIDR block. |
|Tags|List|No|Yes|The tags of the vSwitch.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_m42_j24_e31). |

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

-   VSwitchId: the vSwitch ID allocated by the system.
-   CidrBlock: the IPv4 CIDR block of the vSwitch.
-   Ipv6CidrBlock: the IPv6 CIDR block of the vSwitch.

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

For more examples, visit [SnatEntry.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json) and [SnatEntry.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml). In the examples, the ALIYUN::ECS::VPC, ALIYUN::ECS::VSwitch, ALIYUN::VPC::SnatEntry, ALIYUN::VPC::CommonBandwidthPackage, ALIYUN::VPC::CommonBandwidthPackageIp, ALIYUN::VPC::Ipv6Gateway, and ALIYUN::VPC::Ipv6InternetBandwidth resource types are involved.


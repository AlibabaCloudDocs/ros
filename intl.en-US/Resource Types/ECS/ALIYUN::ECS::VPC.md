# ALIYUN::ECS::VPC

ALIYUN::ECS::VPC is used to create a VPC.

## Syntax

```
{
  "Type": "ALIYUN::ECS::VPC",
  "Properties": {
    "Description": String,
    "Tags": List,
    "Ipv6CidrBlock": String,
    "EnableIpv6": Boolean,
    "ResourceGroupId": String,
    "VpcName": String,
    "CidrBlock": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the VPC belongs.|None|
|VpcName|String|No|Yes|The name of the VPC.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with`http://` or `https://`.|
|CidrBlock|String|No|Yes|The CIDR block of the VPC.|Valid values: -   10.0.0.0/8
-   172.16.0.0/12
-   192.168.0.0/16 and its subnets |
|Description|String|No|Yes|The description of the VPC.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Ipv6CidrBlock|String|No|No|The IPv6 CIDR block of the VPC.|None|
|EnableIpv6|Boolean|No|Yes|Specifies whether to enable IPv6 CIDR blocks.|Default value: false. Valid values: -   true
-   false |
|Tags|List|No|No|The tag of the VPC. Example: `[{"Key": "VpcTag", "Value": ""}]`.|A maximum of 20 tags can be specified. Each tag is a key-value pair. The tag value can be left empty. For more information, see [Tags properties](#section_52w_m69_z07). |

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

-   VpcId: the VPC ID allocated by the system.
-   VRouterId: the ID of the VRouter.
-   RouteTableId: the ID of the route table.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the vpc, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "CidrBlock": {
      "Type": "String",
      "Description": "The IP address range of the VPC in the CIDR block form. You can use the following IP address ranges and their subnets:\n10.0.0.0/8\n172.16.0.0/12 (Default)\n192.168.0.0/16"
    },
    "VpcName": {
      "Type": "String",
      "Description": "Display name of the vpc instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "Ipv6CidrBlock": {
      "Type": "String",
      "Description": "IPv6 network cidr of the VPC.",
      "MinLength": 1
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to vpc. Max support 20 tags to add during create vpc. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "EnableIpv6": {
      "Type": "Boolean",
      "Description": "Whether to enable an IPv6 network cidr, the value is:False (default): not turned on.True: On.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    }
  },
  "Resources": {
    "Vpc": {
      "Type": "ALIYUN::ECS::VPC",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "CidrBlock": {
          "Ref": "CidrBlock"
        },
        "VpcName": {
          "Ref": "VpcName"
        },
        "Ipv6CidrBlock": {
          "Ref": "Ipv6CidrBlock"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "EnableIpv6": {
          "Ref": "EnableIpv6"
        }
      }
    }
  },
  "Outputs": {
    "VRouterId": {
      "Description": "Router id of created VPC.",
      "Value": {
        "Fn::GetAtt": [
          "Vpc",
          "VRouterId"
        ]
      }
    },
    "RouteTableId": {
      "Description": "The router table id of created VPC.",
      "Value": {
        "Fn::GetAtt": [
          "Vpc",
          "RouteTableId"
        ]
      }
    },
    "VpcId": {
      "Description": "Id of created VPC.",
      "Value": {
        "Fn::GetAtt": [
          "Vpc",
          "VpcId"
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
      Description of the vpc, [2, 256] characters. Do not fill or empty, the
      default is empty.
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  CidrBlock:
    Type: String
    Description: >-
      The IP address range of the VPC in the CIDR block form. You can use the
      following IP address ranges and their subnets:

      10.0.0.0/8

      172.16.0.0/12 (Default)

      192.168.0.0/16
  VpcName:
    Type: String
    Description: >-
      Display name of the vpc instance, [2, 128] English or Chinese characters,
      must start with a letter or Chinese in size, can contain numbers, '_' or
      '.', '-'
  Ipv6CidrBlock:
    Type: String
    Description: IPv6 network cidr of the VPC.
    MinLength: 1
  Tags:
    Type: Json
    Description: >-
      Tags to attach to vpc. Max support 20 tags to add during create vpc. Each
      tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  EnableIpv6:
    Type: Boolean
    Description: >-
      Whether to enable an IPv6 network cidr, the value is:False (default): not
      turned on.True: On.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
Resources:
  Vpc:
    Type: 'ALIYUN::ECS::VPC'
    Properties:
      Description:
        Ref: Description
      ResourceGroupId:
        Ref: ResourceGroupId
      CidrBlock:
        Ref: CidrBlock
      VpcName:
        Ref: VpcName
      Ipv6CidrBlock:
        Ref: Ipv6CidrBlock
      Tags:
        Ref: Tags
      EnableIpv6:
        Ref: EnableIpv6
Outputs:
  VRouterId:
    Description: Router id of created VPC.
    Value:
      'Fn::GetAtt':
        - Vpc
        - VRouterId
  RouteTableId:
    Description: The router table id of created VPC.
    Value:
      'Fn::GetAtt':
        - Vpc
        - RouteTableId
  VpcId:
    Description: Id of created VPC.
    Value:
      'Fn::GetAtt':
        - Vpc
        - VpcId
```


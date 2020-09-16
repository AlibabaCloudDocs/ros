# ALIYUN::ECS::VPC

ALIYUN::ECS::VPC类型用于新建专有网络。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无|
|VpcName|String|否|是|专有网络名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|
|CidrBlock|String|否|是|专有网络网段。|取值： -   10.0.0.0/8
-   172.16.0.0/12
-   192.168.0.0/16及所包含的子网 |
|Description|String|否|是|专有网络描述。|长度为2~256个字符。不能以`http://`和`https://`开头。|
|Ipv6CidrBlock|String|否|否|专有网络的IPv6网段。|无|
|EnableIpv6|Boolean|否|是|是否开启IPv6网段。|取值： -   true
-   false（默认值） |
|Tags|List|否|否|标签，例如：`[{"Key": "VpcTag", "Value": ""}]`。|最多设置20个标签，每个标签由键值对组成。标签值可以为空。 详情请参见[Tags属性](#section_52w_m69_z07)。 |

## Tags语法

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   VpcId：系统分配的专有网络ID。
-   VRouterId：路由器ID。
-   RouteTableId：路由表ID。

## 示例

`JSON`格式

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

`YAML`格式

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


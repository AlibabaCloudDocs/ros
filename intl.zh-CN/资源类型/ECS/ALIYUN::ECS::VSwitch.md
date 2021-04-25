# ALIYUN::ECS::VSwitch

ALIYUN::ECS::VSwitch类型用于创建交换机。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|要创建交换机的专有网络ID。|无|
|ZoneId|String|是|否|可用区ID。|无|
|VSwitchName|String|否|是|交换机名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|
|CidrBlock|String|是|否|交换机网段。|必须是所属专有网络的子网段，并且没有被其他交换机占用。|
|Description|String|否|是|交换机描述。|长度为2~256个字符。不能以`http://`和`https://`开头。|
|Ipv6CidrBlock|Integer|否|否|交换机的IPv6网段。|取值范围：0~255（十进制）。 交换机的IPv6网段掩码默认为64位。

支持自定义VPC IPv6网段的最后8位。 |
|Tags|List|否|是|标签。|最多支持20个标签。 更多信息，请参见[Tags属性](#section_m42_j24_e31)。 |

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   VSwitchId：系统分配的交换机ID。
-   CidrBlock：交换机的IPv4网段。
-   Ipv6CidrBlock：交换机的IPv6网段。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建专有网络、创建专有网络中的交换机、在SNAT列表中添加SNAT条目、创建共享带宽实例、添加EIP到共享带宽中、创建IPv6网关和为IPv6地址购买公网带宽的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml)。


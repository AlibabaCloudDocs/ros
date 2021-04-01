# ALIYUN::ECS::NetworkInterface

ALIYUN::ECS::NetworkInterface类型用于创建一个弹性网卡（ENI）。

## 语法

```
{
  "Type": "ALIYUN::ECS::NetworkInterface",
  "Properties": {
    "Description": String,
    "SecurityGroupId": String,
    "PrimaryIpAddress": String,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "NetworkInterfaceName": String,
    "Tags": List,
    "SecurityGroupIds": List,
    "PrivateIpAddresses": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无|
|SecurityGroupId|String|否|是|安全组ID。|安全组和弹性网卡必须在同一个专有网络中。|
|VSwitchId|String|是|否|交换机ID。|无|
|Description|String|否|是|弹性网卡的描述信息。|长度为2~ 256个字符，不能以`http://`和`https://`开头。 |
|NetworkInterfaceName|String|否|是|弹性网卡名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。 |
|PrimaryIpAddress|String|否|否|弹性网卡的主私有IP地址。|指定IP必须是在所属交换机的地址段内的空闲地址，不指定则默认随机分配该交换机中的空闲地址。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_tpw_if9_xq8)。 |
|SecurityGroupIds|List|否|是|一个或多个安全组ID。|安全组和弹性网卡必须在同一个专有网络中。**说明：** 不支持同时指定SecurityGroupId和SecurityGroupIds。 |
|PrivateIpAddresses|List|否|否|从弹性网卡所属交换机的空闲IP地址中选择一个或多个辅助私有IP地址。|可以绑定的IP地址数量的取值范围：-   弹性网卡处于可用（Available）状态：1~10。
-   弹性网卡处于已绑定（InUse）状态：受到实例规格限制。更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。 |

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

-   NetworkInterfaceId：弹性网卡ID。
-   MacAddress：弹性网卡的MAC地址。
-   PrivateIpAddress：弹性网卡的私有IP地址。
-   SecondaryPrivateIpAddresses：弹性网卡的所有私有IP地址。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of your ENI. It is a string of [2, 256] English or Chinese characters."
    },
    "PrivateIpAddresses": {
      "Type": "Json",
      "Description": "Specifies secondary private IP addresses of the ENI. This IP address must be an available IP address in the CIDR block of the VSwitch to which the ENI belongs.",
      "MaxLength": 10
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the security group that the ENI joins. The security group and the ENI must be in a same VPC."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VSwitch ID of the specified VPC. Specifies the switch ID for the VPC."
    },
    "NetworkInterfaceName": {
      "Type": "String",
      "Description": "Name of your ENI. It is a string of [2, 128]  Chinese or English characters. It must begin with a letter and can contain numbers, underscores (_), colons (:), or hyphens (-)."
    },
    "PrimaryIpAddress": {
      "Type": "String",
      "Description": "The primary private IP address of the ENI.  The specified IP address must have the same Host ID as the VSwitch. If no IP addresses are specified, a random network ID is assigned for the ENI."
    },
    "SecurityGroupIds": {
      "Type": "Json",
      "Description": "The IDs of the security groups that the ENI joins. The security groups and the ENI must belong to the same VPC.",
      "MaxLength": 16
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "EniInstance": {
      "Type": "ALIYUN::ECS::NetworkInterface",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "PrivateIpAddresses": {
          "Ref": "PrivateIpAddresses"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "NetworkInterfaceName": {
          "Ref": "NetworkInterfaceName"
        },
        "PrimaryIpAddress": {
          "Ref": "PrimaryIpAddress"
        },
        "SecurityGroupIds": {
          "Ref": "SecurityGroupIds"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "PrivateIpAddress": {
      "Description": "The primary private ip address of your Network Interface.",
      "Value": {
        "Fn::GetAtt": [
          "EniInstance",
          "PrivateIpAddress"
        ]
      }
    },
    "SecondaryPrivateIpAddresses": {
      "Description": "The secondary private IP addresses of your Network Interface.",
      "Value": {
        "Fn::GetAtt": [
          "EniInstance",
          "SecondaryPrivateIpAddresses"
        ]
      }
    },
    "MacAddress": {
      "Description": "The MAC address of your Network Interface.",
      "Value": {
        "Fn::GetAtt": [
          "EniInstance",
          "MacAddress"
        ]
      }
    },
    "NetworkInterfaceId": {
      "Description": "ID of your Network Interface.",
      "Value": {
        "Fn::GetAtt": [
          "EniInstance",
          "NetworkInterfaceId"
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
    Description: Description of your ENI. It is a string of [2, 256] English or Chinese
      characters.
    Type: String
  NetworkInterfaceName:
    Description: Name of your ENI. It is a string of [2, 128]  Chinese or English
      characters. It must begin with a letter and can contain numbers, underscores
      (_), colons (:), or hyphens (-).
    Type: String
  PrimaryIpAddress:
    Description: The primary private IP address of the ENI.  The specified IP address
      must have the same Host ID as the VSwitch. If no IP addresses are specified,
      a random network ID is assigned for the ENI.
    Type: String
  PrivateIpAddresses:
    Description: Specifies secondary private IP addresses of the ENI. This IP address
      must be an available IP address in the CIDR block of the VSwitch to which the
      ENI belongs.
    MaxLength: 10
    Type: Json
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  SecurityGroupId:
    Description: The ID of the security group that the ENI joins. The security group
      and the ENI must be in a same VPC.
    Type: String
  SecurityGroupIds:
    Description: The IDs of the security groups that the ENI joins. The security groups
      and the ENI must belong to the same VPC.
    MaxLength: 16
    Type: Json
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  VSwitchId:
    Description: VSwitch ID of the specified VPC. Specifies the switch ID for the
      VPC.
    Type: String
Resources:
  EniInstance:
    Properties:
      Description:
        Ref: Description
      NetworkInterfaceName:
        Ref: NetworkInterfaceName
      PrimaryIpAddress:
        Ref: PrimaryIpAddress
      PrivateIpAddresses:
        Ref: PrivateIpAddresses
      ResourceGroupId:
        Ref: ResourceGroupId
      SecurityGroupId:
        Ref: SecurityGroupId
      SecurityGroupIds:
        Ref: SecurityGroupIds
      Tags:
        Ref: Tags
      VSwitchId:
        Ref: VSwitchId
    Type: ALIYUN::ECS::NetworkInterface
Outputs:
  MacAddress:
    Description: The MAC address of your Network Interface.
    Value:
      Fn::GetAtt:
      - EniInstance
      - MacAddress
  NetworkInterfaceId:
    Description: ID of your Network Interface.
    Value:
      Fn::GetAtt:
      - EniInstance
      - NetworkInterfaceId
  PrivateIpAddress:
    Description: The primary private ip address of your Network Interface.
    Value:
      Fn::GetAtt:
      - EniInstance
      - PrivateIpAddress
  SecondaryPrivateIpAddresses:
    Description: The secondary private IP addresses of your Network Interface.
    Value:
      Fn::GetAtt:
      - EniInstance
      - SecondaryPrivateIpAddresses
```

更多示例，请参见创建一个弹性网卡、绑定弹性网卡到专有网络类型实例和授权弹性网卡的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/NetworkInterfaceAttachment.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/NetworkInterfaceAttachment.yml)。


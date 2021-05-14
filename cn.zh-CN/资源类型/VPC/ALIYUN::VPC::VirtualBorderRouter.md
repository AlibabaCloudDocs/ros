# ALIYUN::VPC::VirtualBorderRouter

ALIYUN::VPC::VirtualBorderRouter类型用于创建边界路由器（VBR）。

## 语法

```
{
  "Type": "ALIYUN::VPC::VirtualBorderRouter",
  "Properties": {
    "PeerGatewayIp": String,
    "LocalGatewayIp": String,
    "Description": String,
    "CircuitCode": String,
    "PhysicalConnectionId": String,
    "PeeringSubnetMask": String,
    "VlanId": Integer,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PeerGatewayIp|String|是|是|VBR专线侧接口对端的IP地址。|该属性只允许VBR Owner指定或者修改。为专线所有者创建VBR时必须指定，为其他账号创建VBR时可以不指定。|
|LocalGatewayIp|String|是|是|VBR的阿里云侧互联IP。|无|
|Description|String|否|是|VBR的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|CircuitCode|String|否|是|运营商为物理专线提供的电路编码。|只有物理专线的所有者可以指定该参数。|
|PhysicalConnectionId|String|是|否|物理专线的ID。|无|
|PeeringSubnetMask|String|是|是|VBR的阿里云侧和客户侧互联IP的子网掩码。|两个IP地址必须位于同一个子网中。|
|VlanId|Integer|是|否|VBR的VLAN ID。|取值范围：1~2999。**说明：** 只有物理专线的所有者可以指定该参数，同一条物理专线下的两个VBR的VLAN ID不能相同。 |
|Name|String|否|是|VBR的名称。|长度为 2~128个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|

## 返回值

Fn::GetAtt

-   VbrId：VBR的ID。
-   Name：VBR的名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeerGatewayIp": {
      "Type": "String",
      "Description": "The IP address of the peer router interface of the VBR.\nOnly the owner of the VBR can set or modify the value.\nThis parameter is required when you create a VBR for the owner of the physical connection.\nYou can ignore this parameter when you create a VBR for another Alibaba Cloud account."
    },
    "LocalGatewayIp": {
      "Type": "String",
      "Description": "The IP address of the VBR on the Alibaba Cloud side."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the VBR.\nThe description must be 2 to 256 characters in length. It must start with a letter\nbut cannot start with http:// or https://."
    },
    "CircuitCode": {
      "Type": "String",
      "Description": "The circuit code provided by the Internet service provider (ISP) for the physical\nconnection.\nNote Only the owner of the physical connection can set this parameter."
    },
    "PhysicalConnectionId": {
      "Type": "String",
      "Description": "The ID of the physical connection."
    },
    "PeeringSubnetMask": {
      "Type": "String",
      "Description": "The subnet mask for the IP addresses of the VBR on the Alibaba Cloud side and on the\nuser side.\nThe two IP addresses must fall within the same subnet."
    },
    "VlanId": {
      "Type": "Number",
      "Description": "The VLAN ID of the VBR. Valid values: 1 to 2999.\nNote Only the owner of the physical connection can set this parameter. The VLAN IDs of\ntwo VBRs of the same physical connection must be different.",
      "MinValue": 1,
      "MaxValue": 2999
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the VBR.\nThe name must be 2 to 128 characters in length, and can contain, digits, periods (.),\nunderscores (_), and hyphens (-). The name cannot start with http:// or https://."
    }
  },
  "Resources": {
    "VirtualBorderRouter": {
      "Type": "ALIYUN::VPC::VirtualBorderRouter",
      "Properties": {
        "PeerGatewayIp": {
          "Ref": "PeerGatewayIp"
        },
        "LocalGatewayIp": {
          "Ref": "LocalGatewayIp"
        },
        "Description": {
          "Ref": "Description"
        },
        "CircuitCode": {
          "Ref": "CircuitCode"
        },
        "PhysicalConnectionId": {
          "Ref": "PhysicalConnectionId"
        },
        "PeeringSubnetMask": {
          "Ref": "PeeringSubnetMask"
        },
        "VlanId": {
          "Ref": "VlanId"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "VbrId": {
      "Description": "The ID of the VBR.",
      "Value": {
        "Fn::GetAtt": [
          "VirtualBorderRouter",
          "VbrId"
        ]
      }
    },
    "Name": {
      "Description": "The name of the VBR.",
      "Value": {
        "Fn::GetAtt": [
          "VirtualBorderRouter",
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
  CircuitCode:
    Description: 'The circuit code provided by the Internet service provider (ISP)
      for the physical

      connection.

      Note Only the owner of the physical connection can set this parameter.'
    Type: String
  Description:
    Description: 'The description of the VBR.

      The description must be 2 to 256 characters in length. It must start with a
      letter

      but cannot start with http:// or https://.'
    Type: String
  LocalGatewayIp:
    Description: The IP address of the VBR on the Alibaba Cloud side.
    Type: String
  Name:
    Description: 'The name of the VBR.

      The name must be 2 to 128 characters in length, and can contain, digits, periods
      (.),

      underscores (_), and hyphens (-). The name cannot start with http:// or https://.'
    Type: String
  PeerGatewayIp:
    Description: 'The IP address of the peer router interface of the VBR.

      Only the owner of the VBR can set or modify the value.

      This parameter is required when you create a VBR for the owner of the physical
      connection.

      You can ignore this parameter when you create a VBR for another Alibaba Cloud
      account.'
    Type: String
  PeeringSubnetMask:
    Description: 'The subnet mask for the IP addresses of the VBR on the Alibaba Cloud
      side and on the

      user side.

      The two IP addresses must fall within the same subnet.'
    Type: String
  PhysicalConnectionId:
    Description: The ID of the physical connection.
    Type: String
  VlanId:
    Description: 'The VLAN ID of the VBR. Valid values: 1 to 2999.

      Note Only the owner of the physical connection can set this parameter. The VLAN
      IDs of

      two VBRs of the same physical connection must be different.'
    MaxValue: 2999
    MinValue: 1
    Type: Number
Resources:
  VirtualBorderRouter:
    Properties:
      CircuitCode:
        Ref: CircuitCode
      Description:
        Ref: Description
      LocalGatewayIp:
        Ref: LocalGatewayIp
      Name:
        Ref: Name
      PeerGatewayIp:
        Ref: PeerGatewayIp
      PeeringSubnetMask:
        Ref: PeeringSubnetMask
      PhysicalConnectionId:
        Ref: PhysicalConnectionId
      VlanId:
        Ref: VlanId
    Type: ALIYUN::VPC::VirtualBorderRouter
Outputs:
  Name:
    Description: The name of the VBR.
    Value:
      Fn::GetAtt:
      - VirtualBorderRouter
      - Name
  VbrId:
    Description: The ID of the VBR.
    Value:
      Fn::GetAtt:
      - VirtualBorderRouter
      - VbrId
```


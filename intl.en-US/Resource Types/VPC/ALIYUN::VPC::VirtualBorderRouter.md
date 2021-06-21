# ALIYUN::VPC::VirtualBorderRouter

ALIYUN::VPC::VirtualBorderRouter is used to create a virtual border router \(VBR\).

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PeerGatewayIp|String|Yes|Yes|The IP address of the peer router interface of the VBR.|Only the owner of the VBR can set or modify the value. This parameter is required when you create a VBR for the owner of the physical connection. You can ignore this parameter when you create a VBR for another Alibaba Cloud account.|
|LocalGatewayIp|String|Yes|Yes|The IP address of the VBR on the Alibaba Cloud side.|None|
|Description|String|No|Yes|The description of the VBR.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|CircuitCode|String|No|Yes|The circuit code provided by the Internet service provider \(ISP\) of the physical connection.|Only the owner of the physical connection can set this parameter.|
|PhysicalConnectionId|String|Yes|No|The ID of the physical connection.|None|
|PeeringSubnetMask|String|Yes|Yes|The subnet mask for the IP addresses of the VBR on the Alibaba Cloud side and on the user side.|The two IP addresses must fall within the same subnet.|
|VlanId|Integer|Yes|No|The virtual LAN \(VLAN\) ID of the VBR.|Valid values: 1 to 2999. **Note:** Only the owner of the physical connection can set this parameter. The VLAN IDs of two VBRs of the same physical connection must be different. |
|Name|String|No|Yes|The name of the VBR.|The name must be 2 to 128 characters in length, and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   VbrId: the ID of the VBR.
-   Name: the name of the VBR.

## Examples

`JSON` format

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

`YAML` format

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


# ALIYUN::VPC::VpnRouteEntry

ALIYUN::VPC::VpnRouteEntry is used to create a destination-based route for a VPN gateway.

## Syntax

```
{
  "Type": "ALIYUN::VPC::VpnRouteEntry",
  "Properties": {
    "Description": String,
    "RouteDest": String,
    "OverlayMode": String,
    "VpnGatewayId": String,
    "NextHop": String,
    "PublishVpc": Boolean,
    "Weight": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the destination-based route.|None|
|RouteDest|String|Yes|No|The destination CIDR block of the destination-based route.|None|
|OverlayMode|String|No|No|The tunneling protocol.|Set the value to Ipsec. The value of Ipsec indicates the IPsec tunneling protocol.|
|VpnGatewayId|String|Yes|No|The ID of the VPN gateway.|None|
|NextHop|String|Yes|No|The next hop of the destination-based route.|None|
|PublishVpc|Boolean|Yes|Yes|Specifies whether to advertise the destination-based route to the route table of the associated virtual private cloud \(VPC\).|Valid values:-   true: advertises the destination-based route to the route table of the associated VPC.
-   false: does not advertise the destination-based route to the route table of the associated VPC. |
|Weight|Integer|Yes|Yes|The weight of the destination-based route.|Valid values: 0 to 100.|

## Response parameters

Fn::GetAtt

-   RouteDest: the destination CIDR block of the destination-based route.
-   VpnGatewayId: the ID of the VPN gateway.
-   NextHop: the next hop of the destination-based route.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the VPN destination route."
    },
    "RouteDest": {
      "Type": "String",
      "Description": "The destination CIDR block of the destination route."
    },
    "OverlayMode": {
      "Type": "String",
      "Description": "The overlay mode."
    },
    "VpnGatewayId": {
      "Type": "String",
      "Description": "The ID of the VPN Gateway."
    },
    "NextHop": {
      "Type": "String",
      "Description": "The next hop of the destination route entry."
    },
    "PublishVpc": {
      "Type": "Boolean",
      "Description": "Indicates whether to publish the destination route to the VPC. Valid values:\ntrue: Publish the destination route to the VPC.\nfalse: Do not publish the destination route to the VPC.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Weight": {
      "Type": "Number",
      "Description": "The weight of the destination route. Valid values: 0|100."
    }
  },
  "Resources": {
    "VpnRouteEntry": {
      "Type": "ALIYUN::VPC::VpnRouteEntry",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "RouteDest": {
          "Ref": "RouteDest"
        },
        "OverlayMode": {
          "Ref": "OverlayMode"
        },
        "VpnGatewayId": {
          "Ref": "VpnGatewayId"
        },
        "NextHop": {
          "Ref": "NextHop"
        },
        "PublishVpc": {
          "Ref": "PublishVpc"
        },
        "Weight": {
          "Ref": "Weight"
        }
      }
    }
  },
  "Outputs": {
    "RouteDest": {
      "Description": "The destination CIDR block of the destination route.",
      "Value": {
        "Fn::GetAtt": [
          "VpnRouteEntry",
          "RouteDest"
        ]
      }
    },
    "VpnGatewayId": {
      "Description": "The ID of the VPN Gateway.",
      "Value": {
        "Fn::GetAtt": [
          "VpnRouteEntry",
          "VpnGatewayId"
        ]
      }
    },
    "NextHop": {
      "Description": "The next hop of the destination route entry.",
      "Value": {
        "Fn::GetAtt": [
          "VpnRouteEntry",
          "NextHop"
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
    Description: The description of the VPN destination route.
    Type: String
  NextHop:
    Description: The next hop of the destination route entry.
    Type: String
  OverlayMode:
    Description: The overlay mode.
    Type: String
  PublishVpc:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Indicates whether to publish the destination route to the VPC. Valid
      values:

      true: Publish the destination route to the VPC.

      false: Do not publish the destination route to the VPC.'
    Type: Boolean
  RouteDest:
    Description: The destination CIDR block of the destination route.
    Type: String
  VpnGatewayId:
    Description: The ID of the VPN Gateway.
    Type: String
  Weight:
    Description: 'The weight of the destination route. Valid values: 0|100.'
    Type: Number
Resources:
  VpnRouteEntry:
    Properties:
      Description:
        Ref: Description
      NextHop:
        Ref: NextHop
      OverlayMode:
        Ref: OverlayMode
      PublishVpc:
        Ref: PublishVpc
      RouteDest:
        Ref: RouteDest
      VpnGatewayId:
        Ref: VpnGatewayId
      Weight:
        Ref: Weight
    Type: ALIYUN::VPC::VpnRouteEntry
Outputs:
  NextHop:
    Description: The next hop of the destination route entry.
    Value:
      Fn::GetAtt:
      - VpnRouteEntry
      - NextHop
  RouteDest:
    Description: The destination CIDR block of the destination route.
    Value:
      Fn::GetAtt:
      - VpnRouteEntry
      - RouteDest
  VpnGatewayId:
    Description: The ID of the VPN Gateway.
    Value:
      Fn::GetAtt:
      - VpnRouteEntry
      - VpnGatewayId
```


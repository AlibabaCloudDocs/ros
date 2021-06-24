# ALIYUN::VPC::VpnPbrRouteEntry

ALIYUN::VPC::VpnPbrRouteEntry is used to create a policy-based route for a VPN gateway.

## Syntax

```
{
  "Type": "ALIYUN::VPC::VpnPbrRouteEntry",
  "Properties": {
    "Description": String,
    "RouteDest": String,
    "OverlayMode": String,
    "VpnGatewayId": String,
    "NextHop": String,
    "RouteSource": String,
    "PublishVpc": Boolean,
    "Weight": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the policy-based route.|None|
|RouteDest|String|Yes|No|The destination CIDR block of the policy-based route.|None|
|OverlayMode|String|No|No|The tunneling protocol.|Set the value to Ipsec. The value of Ipsec indicates the IPsec tunneling protocol.|
|VpnGatewayId|String|Yes|No|The ID of the VPN gateway.|None|
|NextHop|String|Yes|No|The next hop of the policy-based route.|None|
|RouteSource|String|Yes|No|The source CIDR block of the policy-based route.|None|
|PublishVpc|Boolean|Yes|Yes|Specifies whether to advertise the policy-based route to the route table of the associated virtual private cloud \(VPC\).|Valid values:-   true: advertises the policy-based route to the route table of the associated VPC.
-   false: does not advertise the policy-based route to the route table of the associated VPC. |
|Weight|Integer|Yes|Yes|The weight of the policy-based route.|Valid values: 0 to 100.|

## Response parameters

Fn::GetAtt

-   RouteDest: the destination CIDR block of the policy-based route.
-   VpnGatewayId: the ID of the VPN gateway.
-   NextHop: the next hop of the policy-based route.
-   RouteSource: the source CIDR block of the policy-based route.

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
    "RouteSource": {
      "Type": "String",
      "Description": "The source CIDR block of the policy-based route."
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
    "VpnPbrRouteEntry": {
      "Type": "ALIYUN::VPC::VpnPbrRouteEntry",
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
        "RouteSource": {
          "Ref": "RouteSource"
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
          "VpnPbrRouteEntry",
          "RouteDest"
        ]
      }
    },
    "VpnGatewayId": {
      "Description": "The ID of the VPN Gateway.",
      "Value": {
        "Fn::GetAtt": [
          "VpnPbrRouteEntry",
          "VpnGatewayId"
        ]
      }
    },
    "NextHop": {
      "Description": "The next hop of the destination route entry.",
      "Value": {
        "Fn::GetAtt": [
          "VpnPbrRouteEntry",
          "NextHop"
        ]
      }
    },
    "RouteSource": {
      "Description": "The destination CIDR block of the policy-based route.",
      "Value": {
        "Fn::GetAtt": [
          "VpnPbrRouteEntry",
          "RouteSource"
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
  RouteSource:
    Description: The source CIDR block of the policy-based route.
    Type: String
  VpnGatewayId:
    Description: The ID of the VPN Gateway.
    Type: String
  Weight:
    Description: 'The weight of the destination route. Valid values: 0|100.'
    Type: Number
Resources:
  VpnPbrRouteEntry:
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
      RouteSource:
        Ref: RouteSource
      VpnGatewayId:
        Ref: VpnGatewayId
      Weight:
        Ref: Weight
    Type: ALIYUN::VPC::VpnPbrRouteEntry
Outputs:
  NextHop:
    Description: The next hop of the destination route entry.
    Value:
      Fn::GetAtt:
      - VpnPbrRouteEntry
      - NextHop
  RouteDest:
    Description: The destination CIDR block of the destination route.
    Value:
      Fn::GetAtt:
      - VpnPbrRouteEntry
      - RouteDest
  RouteSource:
    Description: The destination CIDR block of the policy-based route.
    Value:
      Fn::GetAtt:
      - VpnPbrRouteEntry
      - RouteSource
  VpnGatewayId:
    Description: The ID of the VPN Gateway.
    Value:
      Fn::GetAtt:
      - VpnPbrRouteEntry
      - VpnGatewayId
```


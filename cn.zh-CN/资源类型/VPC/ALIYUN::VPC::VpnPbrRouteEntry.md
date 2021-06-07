# ALIYUN::VPC::VpnPbrRouteEntry

ALIYUN::VPC::VpnPbrRouteEntry类型用于创建VPN策略路由。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|策略路由的描述信息。|无|
|RouteDest|String|是|否|策略路由的目标网段。|无|
|OverlayMode|String|否|否|覆盖模式。|取值：Ipsec，表示IPsec隧道协议。|
|VpnGatewayId|String|是|否|VPN网关的ID。|无|
|NextHop|String|是|否|策略路由的下一跳。|无|
|RouteSource|String|是|否|策略路由的源网段。|无|
|PublishVpc|Boolean|是|是|是否发布策略路由到VPC。|取值：-   true：发布策略路由到VPC。
-   false：不发布策略路由到VPC。 |
|Weight|Integer|是|是|策略路由的权重值。|取值：0~100。|

## 返回值

Fn::GetAtt

-   RouteDest：策略路由的目标网段。
-   VpnGatewayId：VPN网关的ID。
-   NextHop：策略路由的下一跳。
-   RouteSource：策略路由的源网段。

## 示例

`JSON`格式

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

`YAML`格式

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


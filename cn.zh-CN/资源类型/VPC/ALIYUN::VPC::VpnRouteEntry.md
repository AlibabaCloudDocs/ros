# ALIYUN::VPC::VpnRouteEntry

ALIYUN::VPC::VpnRouteEntry类型用于创建VPN目的路由。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|VPN目的路由的描述信息。|无|
|RouteDest|String|是|否|目的路由的目标网段。|无|
|OverlayMode|String|否|否|覆盖模式。|取值：Ipsec，表示IPsec隧道协议。|
|VpnGatewayId|String|是|否|VPN网关的ID。|无|
|NextHop|String|是|否|目的路由的下一跳。|无|
|PublishVpc|Boolean|是|是|是否发布目的路由到VPC。|取值：-   true：发布目的路由到VPC。
-   false：不发布目的路由到VPC。 |
|Weight|Integer|是|是|目的路由的权重值。|取值：0~100。|

## 返回值

Fn::GetAtt

-   RouteDest：目的路由的目标网段。
-   VpnGatewayId：VPN网关的ID。
-   NextHop：目的路由的下一跳。

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


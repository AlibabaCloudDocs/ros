# ALIYUN::ECS::Route {#concept_51197_zh .concept}

ALIYUN::ECS::Route is used to create a custom route.

## Syntax {#section_j2t_tw2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::Route",
  "Properties": {
    "DestinationCidrBlock": String,
    "RouteTableId": String,
    "NextHopId": String,
    "NextHopType": String,
    "RouteId": String,
    "NextHopList": List
  }
}
```

## Properties {#section_nny_ww2_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DestinationCidrBlock|String|Yes|No|The destination CIDR block of a routing entry.|None|
|RouteTableId|String|Yes|No|The ID of the routing table to which the routing entry belongs.|None|
|NextHopId|String|Yes|No|The ID of the next-hop instance of the routing entry.|This parameter is applicable to non-ECMP routes.|
|RouteId|String|Yes|No|The route ID of the created routing entry.|None|
|NextHopType|String|No|No|The type of the next hop.| Valid values: Instance, Tunnel, HaVip, and RouterInterface.

 Default value: Instance. Instance indicates that the next hop is an ECS instance.

 |
|NextHopList|List|No|No|The list of next hops of the routing entry.|You must set the NextHopType and NextHopId parameters to specify the next hops. If you set the NextHopList parameter, the routing entry is added for the ECMP destination. The list contains multiple next hops of the ECMP routing entry. The list can contain two to four next hops. The NextHopList parameter can be set only when the routing entry belongs to a VRouter. The next hops must be the router interfaces pointing to the connected VBRs. If you do not set the NextHopList parameter, ECMP is not configured for the routing entry.|

## NextHopList syntax {#section_xbk_fx2_lfb .section}

```language-json
"NextHopList": [
  "NextHopId": String,
  "NextHopType": String
]
```

## NextHopList properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|NextHopId|String|Yes|No|The ID of the next-hop instance of a routing entry.|None|
|NextHopType|String|No|No|The type of the next hop.| Valid values: Instance, Tunnel, HaVip, and RouterInterface.

 Default value: RouterInterface. RouterInterface indicates that the next hop is a router interface instance.

 |

## Response parameters { .section}

**Fn::GetAtt**

None

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ECSRoute": {
      "Type": "ALIYUN::ECS::Route",
      "Properties": {
        "RouteId": "vrt-25mz0uxk4",
        "RouteTableId": "vtb-25oudgpsu",
        "DestinationCidrBlock": "172.16.107.0/24",
        "NextHopId": "i-25xzyhxtp"
      }
    }
  }
}
```


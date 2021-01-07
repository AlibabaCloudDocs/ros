# ALIYUN::ECS::Route

ALIYUN::ECS::Route is used to create a custom route.

## Syntax

```
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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DestinationCidrBlock|String|Yes|No|The destination Classless Inter-Domain Routing \(CIDR\) block of the route entry.|None|
|RouteTableId|String|Yes|No|The ID of the route table.|None|
|NextHopId|String|No|No|The ID of the next-hop instance of the route entry.|The route is a non-ECMP route.|
|RouteId|String|Yes|No|The ID of the route.|None|
|NextHopType|String|No|No|The type of the next hop.|Default value: Instance. Valid values: -   Instance
-   Tunnel
-   HaVip
-   RouterInterface |
|NextHopList|List|No|No|The list of next hops of the route entry.|You must specify the NextHopType and NextHopId parameters to specify the next hops. -   If you specify the NextHopList parameter, the route is an ECMP route. The list contains two to four next hops of the ECMP route entry.

**Note:** The NextHopList parameter can be specified only when the route entry belongs to a VRouter. In addition, the next hops must be the router interfaces pointing to the connected VBRs.

-   If you do not specify the NextHopList parameter, the route is a non-ECMP route. |

## NextHopList syntax

```
"NextHopList": [
  {
    "NextHopId": String,
    "NextHopType": String
  }
]
```

## NextHopList properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NextHopId|String|Yes|No|The ID of the next-hop instance of the route entry.|None|
|NextHopType|String|No|No|The type of the next hop.|Default value: RouterInterface. Valid values: -   Instance
-   Tunnel
-   HaVip
-   RouterInterface |

## Response parameters

Fn::GetAtt

None

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ECSRoute": {
      "Type": "ALIYUN::ECS::Route",
      "Properties": {
 "RouteId": "vrt-25mz0****",
        "RouteTableId": "vtb-25oud****",
        "DestinationCidrBlock": "172.16.XX.XX/24",
        "NextHopId": "i-25xzy****"
      }
    }
  }
}
```


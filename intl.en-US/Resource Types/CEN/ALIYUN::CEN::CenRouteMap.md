# ALIYUN::CEN::CenRouteMap

ALIYUN::CEN::CenRouteMap is used to create a route map.

## Syntax

```
{
  "Type": "ALIYUN::CEN::CenRouteMap",
  "Properties": {
    "Description": String,
    "SourceInstanceIdsReverseMatch": Boolean,
    "TransmitDirection": String,
    "MatchCommunitySet": List,
    "CenRegionId": String,
    "SourceRouteTableIds": List,
    "DestinationInstanceIds": List,
    "DestinationInstanceIdsReverseMatch": Boolean,
    "SourceInstanceIds": List,
    "DestinationRouteTableIds": List,
    "DestinationCidrBlocks": List,
    "OperateCommunitySet": List,
    "DestinationChildInstanceTypes": List,
    "Priority": Integer,
    "SourceChildInstanceTypes": List,
    "AsPathMatchMode": String,
    "CidrMatchMode": String,
    "MapResult": String,
    "RouteTypes": List,
    "Preference": Integer,
    "CommunityOperateMode": String,
    "CenId": String,
    "NextPriority": Integer,
    "PrependAsPath": List,
    "CommunityMatchMode": String,
    "MatchAsns": List,
    "SourceRegionIds": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the route map.|None|
|SourceInstanceIdsReverseMatch|Boolean|No|Yes|Specifies whether the match is successful if the source instance ID is not in the list specified by SourceInstanceIds.|Default value: false. Valid values:-   false: If the source instance ID is in the list specified by SourceInstanceIds, the match is successful.
-   true: If the source instance ID is not in the list specified by SourceInstanceIds, the match is successful. |
|TransmitDirection|String|Yes|No|The direction in which the route map is to be applied.|Valid values:-   RegionIn: Routes are advertised to Cloud Enterprise Network \(CEN\) regional gateways. For example, routes are advertised from network instances deployed in the current region or routes deployed in other regions to the gateways deployed in the current region.
-   RegionOut: Routes are advertised from CEN regional gateways. For example, routes are advertised from gateways deployed in the current region to network instances deployed in the same region, or to gateways deployed in other regions. |
|MatchCommunitySet|List|No|Yes|The community set to be matched by using a match statement.|Specify each community in the nn:nn format. Valid values of nn: 1 to 65535.

A maximum of 32 communities can be specified.

Each community must comply with RFC 1997. RFC 8092 that defines Border Gateway Protocol \(BGP\) large communities is not supported. **Note:** If the configurations of the communities are incorrect, routes may not be advertised to your data center. |
|CenRegionId|String|Yes|No|The region ID of the CEN instance.|None|
|SourceRouteTableIds|List|No|Yes|The IDs of the source route tables to be matched by using a match statement.|A maximum of 32 route table IDs can be specified. |
|DestinationInstanceIds|List|No|Yes|The destination instance IDs to be matched by using a match statement.|You can enter the IDs of virtual private clouds \(VPCs\), virtual border routers \(VBRs\), and smart access gateway \(SAG\) instances.

A maximum of 32 instance IDs can be specified. **Note:** The destination instance IDs are valid only when the route map is applied to scenarios where routes are advertised from gateways in the current region to instances in the current region. |
|DestinationInstanceIdsReverseMatch|Boolean|No|Yes|Specifies whether the match is successful if the destination instance ID is not in the list specified by DestinationInstanceIds.|Default value: false. Valid values:-   false: The match is successful if the destination instance ID is in the list specified by DestinationInstanceIds.
-   true: The match is successful if the destination instance ID is not in the list specified by DestinationInstanceIds. |
|SourceInstanceIds|List|No|Yes|The source instance IDs to be matched by using a match statement.|You can enter the IDs of VPCs, VBRs, and SAG instances.

A maximum of 32 instance IDs can be specified.|
|DestinationRouteTableIds|List|No|Yes|The IDs of the destination route tables to be matched by using a match statement.|A maximum of 32 route table IDs can be specified. |
|DestinationCidrBlocks|List|No|Yes|The prefixes to be matched by using a match statement.|The CIDR format is used. A maximum of 32 CIDR blocks can be specified. |
|OperateCommunitySet|List|No|Yes|The community set to be managed by using an action statement.|Specify each community in the nn:nn format. Valid values of nn: 1 to 65535.

A maximum of 32 communities can be specified.

Each community must comply with RFC 1997. RFC 8092 that defines BGP large communities is not supported. **Note:** If the configurations of the communities are incorrect, routes may not be advertised to your data center. |
|DestinationChildInstanceTypes|List|No|Yes|The destination instance types to be matched by using a match statement.|Valid values:-   VPC
-   VBR

**Note:** The destination instance types are valid only when the route map is applied to scenarios where routes are advertised from gateways in the current region to instances in the current region. |
|Priority|Integer|Yes|Yes|The priority of the route map.|Valid values: 1 to 100. A smaller value indicates a higher priority. **Note:** After you specify a priority value for a route map, you cannot set the same priority value for another route map that is applied in the same region and direction. The system filters routes based on route maps that start from the route map with the lowest priority value. Therefore, set appropriate priority values to sort the route maps in the desired order. |
|SourceChildInstanceTypes|List|No|Yes|Source instance types to be matched by using a match statement.|Valid values:-   VPC
-   VBR |
|AsPathMatchMode|String|No|Yes|The mode in which the autonomous system \(AS\) paths are matched by using a match statement.|Valid values:-   Include: fuzzy match. A route meets the match condition if the AS path of the route overlaps with that specified in the match condition.
-   Complete: exact match. A route meets the match condition only if the AS path of the route is the same as that specified in the match condition. |
|CidrMatchMode|String|No|Yes|The mode in which the prefixes are matched by using a match statement.|Valid values:-   Include: fuzzy match. A route meets the match condition if the route prefix specified in the match condition contains the prefix of the route. For example, if you set the match condition to 1.1.0.0/16 and fuzzy match is applied, the route whose prefix is 1.1.1.0/24 meets the match condition.
-   Complete: exact match. A route meets the match condition only when the prefix of the route is the same as that specified in the match condition. For example, if you set the match condition to 1.1.0.0/16 and exact match is applied, only the route whose route prefix is 1.1.0.0/16 meets the match condition. |
|MapResult|String|Yes|Yes|The action to be performed on a route if the route matches all the match conditions.|Valid values:-   Permit: allows the routes that are matched.
-   Deny: rejects the routes that are matched. |
|RouteTypes|List|No|Yes|The types of routes to be matched by using a match statement.|Valid values:-   System: system routes that are generated by the system
-   Custom: custom routes that are created by users
-   BGP: BGP routes that are advertised to BGP

You can enter multiple types.|
|Preference|Integer|No|Yes|The route priority to be modified by using an action statement.|Valid values: 1 to 100.

Default value: 50.

A smaller value indicates a higher priority.|
|CommunityOperateMode|String|No|Yes|The mode in which communities are managed by using an action statement.|Valid values:-   Additive: adds communities.
-   Replace: replaces communities. |
|CenId|String|Yes|No|The ID of the CEN instance.|None|
|NextPriority|Integer|No|Yes|The priority of the next associated route map.|Valid values: 1 to 100. -   If the priority is not set, no next route map is associated with the current route map.
-   If the priority is set to 1, the next route map is associated with the current route map.
-   If the priority is set and the value is not 1, the priority of the associated route map must be higher than that of the current route map.

Only when the MapResult parameter is set to Permit, the matched routes continue to match the next associated route maps.|
|PrependAsPath|List|No|Yes|The AS paths that are prepended by using an action statement when regional gateways receive or advertise routes.|For route maps that are applied in different directions, the requirements for AS paths to be prepended are different:-   When AS paths are prepended in the inbound direction, you must specify the source instance IDs and the source region in the match condition. In addition, the source region must be the same as the region where the route map is applied.
-   When AS paths are prepended in the outbound direction, you must specify the destination instance IDs in the match condition. |
|CommunityMatchMode|String|No|Yes|The mode in which communities are matched by using a match statement.|Valid values:-   Include: fuzzy match. A route meets the match condition if the community of the route overlaps with that specified in the match condition.
-   Complete: exact match. A route meets the match condition only if the community of the route is the same as that specified in the match condition. |
|MatchAsns|List|No|Yes|The AS paths to be matched by using a match statement.|An AS path is a mandatory attribute, which describes the AS number through which a BGP route passes when the BGP route is advertised.

Only the AS-SEQUENCE parameter is supported. The AS-SET, AS-CONFED-SEQUENCE, and AS-CONFED-SET parameters are not supported. In other words, only the AS number list is supported. Sets and sub-lists are not supported.|
|SourceRegionIds|List|No|Yes|The source region IDs to be matched by using a match statement.|A maximum of 32 region IDs can be specified. |

## Response parameters

Fn::GetAtt

-   Description: the description of the route map.
-   SourceInstanceIdsReverseMatch: indicates whether the match is successful if the source instance ID is not in the list specified by SourceInstanceIds.
-   TransmitDirection: the direction in which the route map is applied.
-   MatchCommunitySet: the matched community set.
-   CenRegionId: the region ID of the CEN instance.
-   SourceRouteTableIds: the IDs of the source route tables that are matched.
-   DestinationInstanceIds: the destination instance IDs that are matched.
-   DestinationInstanceIdsReverseMatch: indicates whether the match is successful if the destination instance ID is not in the list specified by DestinationInstanceIds.
-   SourceInstanceIds: the source instance IDs that are matched.
-   DestinationRouteTableIds: the IDs of the destination route tables that are matched.
-   DestinationCidrBlocks: the matched prefixes.
-   RouteMapId: the ID of the route map.
-   OperateCommunitySet: the managed community set.
-   DestinationChildInstanceTypes: the destination instance types that are matched.
-   Priority: the priority of the route map.
-   SourceChildInstanceTypes: the source instance types that are matched.
-   AsPathMatchMode: the mode in which the AS paths are matched.
-   CidrMatchMode: the mode in which the prefixes are matched.
-   MapResult: the action that is performed on a route if the route matches all the match conditions.
-   RouteTypes: the matched route types.
-   Preference: the modified route priority.
-   CommunityOperateMode: the mode in which communities are managed.
-   CenId: the ID of the CEN instance.
-   NextPriority: the priority of the next associated route map.
-   PrependAsPath: The AS paths that are prepended when regional gateways receive or advertise routes.
-   CommunityMatchMode: the mode in which communities are matched.
-   MatchAsns: the matched AS paths.
-   SourceRegionIds: the source region IDs that are matched.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the route map."
    },
    "SourceInstanceIdsReverseMatch": {
      "Type": "Boolean",
      "Description": "Indicates whether to enable the reverse match method of the SourceInstanceIds match condition. Valid values:  false (default): If the ID of a route's source instance is included in SourceInstanceIds, the route is permitted. true: If the ID of a route's source instance is not included in SourceInstanceIds, the route is permitted.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "TransmitDirection": {
      "Type": "String",
      "Description": "The direction in which the route map is applied. Valid values:  RegionIn: The direction in which routes are imported to the regional gateway of the CEN.  For example, routes are imported to the regional gateway from an instance in the current region or another region.  RegionOut: The direction in which routes are exported from the regional gateway of the CEN.  For example, routes are exported from the regional gateway of the current region to an instance in the same region, or to the regional gateway in another region."
    },
    "MatchCommunitySet": {
      "Type": "Json",
      "Description": "A match statement that indicates the community set."
    },
    "CenRegionId": {
      "Type": "String",
      "Description": "The ID of the region to which the CEN instance belongs."
    },
    "SourceRouteTableIds": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the source route tables."
    },
    "DestinationInstanceIds": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the destination instances.  This parameter is valid only when the TransmitDirection parameter is set to RegionOut, and the destination instance and the route map belongs to the same region."
    },
    "DestinationInstanceIdsReverseMatch": {
      "Type": "Boolean",
      "Description": "Indicates whether to enable the reverse match method of the DestinationInstanceIds match condition. Valid values:  false (default): If the ID of a route's destination instance is included in DestinationInstanceIds, the route is permitted. true: If the ID of a route's destination instance is not included in DestinationInstanceIds, the route is permitted.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "SourceInstanceIds": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the source instances."
    },
    "DestinationRouteTableIds": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the destination route tables.  This parameter is valid only when the TransmitDirection parameter is set to RegionOut, and the destination route table and the route map belongs to the same region."
    },
    "DestinationCidrBlocks": {
      "Type": "Json",
      "Description": "A match statement that indicates the prefix list."
    },
    "OperateCommunitySet": {
      "Type": "Json",
      "Description": "An action statement that operates the community attribute."
    },
    "DestinationChildInstanceTypes": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the destination instances.  VPC: VPC VBR: VBR CCN: Mainland China CCN This parameter is valid only when the TransmitDirection parameter is set to RegionOut, and the destination instance and the route map belong to the same region."
    },
    "Priority": {
      "Type": "Number",
      "Description": "The priority of the route map."
    },
    "SourceChildInstanceTypes": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the source instances.  VPC: Virtual Private Cloud (VPC) VBR: Virtual Border Router (VBR) CCN: Mainland China Cloud Connect Network (CCN)"
    },
    "AsPathMatchMode": {
      "Type": "String",
      "Description": "A match statement. It indicates the mode in which the as-path attribute is matched. Valid values:  Include: Fuzzy match. A route matches the condition if the AS path in the route overlaps the AS path in the match condition. Complete: Exact match. A route matches the condition only when the AS path of the route is the same as the AS path in the match condition."
    },
    "CidrMatchMode": {
      "Type": "String",
      "Description": "A match statement. It indicates the mode in which the prefix attribute is matched. Valid values:  Include: Fuzzy match. If the prefix of a route is contained in the prefix in the match condition, the route matches the condition.  For example, if the prefix in the match condition is set to 1.1.0.0/16 and the match method is set to Fuzzy Match, the route with the prefix of 1.1.1.0/24 matches the condition.  Complete: Exact match. A route matches the condition only when the prefix of the route is the same as the prefix in the match condition.  For example, if the prefix in the match condition is set to 1.1.0.0/16 and the match method is set to Exact Match, only the route with the prefix of 1.1.1.0/16 matches the condition."
    },
    "MapResult": {
      "Type": "String",
      "Description": "The action that is performed to a route if the route meets all the match conditions.  Permit: The route is permitted. Deny: The route is denied."
    },
    "RouteTypes": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of route types.  System: System routes generated by the system. Custom: Custom routes added by users. BGP: Routes advertised to BGP."
    },
    "Preference": {
      "Type": "Number",
      "Description": "An action statement that modifies the preference of the route."
    },
    "CommunityOperateMode": {
      "Type": "String",
      "Description": "An action statement. It indicates the mode in which the community attribute is operated. Valid values:  Additive: Sets a value for the community attribute. Replace: Replaces the value of the community attribute."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "NextPriority": {
      "Type": "Number",
      "Description": "The priority of the next route map that is associated with the current route map. Value range: 1 to 100.  If this parameter is not set, the current route map is not associated with any route map that is ordered next to the current route map. If this parameter is set to 1, the current route map is associated with the next route map. If this parameter is set to a value other than 1, the priority of the associated route map must be lower than the priority of the current route map, that is, the value of NextPriority must be greater than the value set for Priority. Only when MapResult is set to Permit, the routes which match all the matching conditions will be evaluated by the associated route map that is configured with a specific preference value."
    },
    "PrependAsPath": {
      "Type": "Json",
      "Description": "Indicates AS Path prepending when a regional gateway receives or publishes a route."
    },
    "CommunityMatchMode": {
      "Type": "String",
      "Description": "A match statement. It indicates the mode in which the community attribute is matched. Valid values:  Include: Fuzzy match. A route matches the condition if the community of the route overlaps the community in the match condition. Complete: Exact match. A route matches the condition only when the community of the route is the same as the community in the match condition."
    },
    "MatchAsns": {
      "Type": "Json",
      "Description": "A match statement that indicates the As path list."
    },
    "SourceRegionIds": {
      "Type": "Json",
      "Description": "A match statement that indicates the list of IDs of the source regions."
    }
  },
  "Resources": {
    "CENCenRouteMap": {
      "Type": "ALIYUN::CEN::CenRouteMap",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "SourceInstanceIdsReverseMatch": {
          "Ref": "SourceInstanceIdsReverseMatch"
        },
        "TransmitDirection": {
          "Ref": "TransmitDirection"
        },
        "MatchCommunitySet": {
          "Ref": "MatchCommunitySet"
        },
        "CenRegionId": {
          "Ref": "CenRegionId"
        },
        "SourceRouteTableIds": {
          "Ref": "SourceRouteTableIds"
        },
        "DestinationInstanceIds": {
          "Ref": "DestinationInstanceIds"
        },
        "DestinationInstanceIdsReverseMatch": {
          "Ref": "DestinationInstanceIdsReverseMatch"
        },
        "SourceInstanceIds": {
          "Ref": "SourceInstanceIds"
        },
        "DestinationRouteTableIds": {
          "Ref": "DestinationRouteTableIds"
        },
        "DestinationCidrBlocks": {
          "Ref": "DestinationCidrBlocks"
        },
        "OperateCommunitySet": {
          "Ref": "OperateCommunitySet"
        },
        "DestinationChildInstanceTypes": {
          "Ref": "DestinationChildInstanceTypes"
        },
        "Priority": {
          "Ref": "Priority"
        },
        "SourceChildInstanceTypes": {
          "Ref": "SourceChildInstanceTypes"
        },
        "AsPathMatchMode": {
          "Ref": "AsPathMatchMode"
        },
        "CidrMatchMode": {
          "Ref": "CidrMatchMode"
        },
        "MapResult": {
          "Ref": "MapResult"
        },
        "RouteTypes": {
          "Ref": "RouteTypes"
        },
        "Preference": {
          "Ref": "Preference"
        },
        "CommunityOperateMode": {
          "Ref": "CommunityOperateMode"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "NextPriority": {
          "Ref": "NextPriority"
        },
        "PrependAsPath": {
          "Ref": "PrependAsPath"
        },
        "CommunityMatchMode": {
          "Ref": "CommunityMatchMode"
        },
        "MatchAsns": {
          "Ref": "MatchAsns"
        },
        "SourceRegionIds": {
          "Ref": "SourceRegionIds"
        }
      }
    }
  },
  "Outputs": {
    "Description": {
      "Description": "The description of the route map.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "Description"
        ]
      }
    },
    "SourceInstanceIdsReverseMatch": {
      "Description": "Indicates whether to enable the reverse match method of the SourceInstanceIds match condition. Valid values:  false (default): If the ID of a route's source instance is included in SourceInstanceIds, the route is permitted. true: If the ID of a route's source instance is not included in SourceInstanceIds, the route is permitted.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "SourceInstanceIdsReverseMatch"
        ]
      }
    },
    "TransmitDirection": {
      "Description": "The direction in which the route map is applied. Valid values:  RegionIn: The direction in which routes are imported to the regional gateway of the CEN.  For example, routes are imported to the regional gateway from an instance in the current region or another region.  RegionOut: The direction in which routes are exported from the regional gateway of the CEN.  For example, routes are exported from the regional gateway of the current region to an instance in the same region, or to the regional gateway in another region.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "TransmitDirection"
        ]
      }
    },
    "MatchCommunitySet": {
      "Description": "A match statement that indicates the community set.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "MatchCommunitySet"
        ]
      }
    },
    "CenRegionId": {
      "Description": "The ID of the region to which the CEN instance belongs.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "CenRegionId"
        ]
      }
    },
    "SourceRouteTableIds": {
      "Description": "A match statement that indicates the list of IDs of the source route tables.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "SourceRouteTableIds"
        ]
      }
    },
    "DestinationInstanceIds": {
      "Description": "A match statement that indicates the list of IDs of the destination instances.  This parameter is valid only when the TransmitDirection parameter is set to RegionOut, and the destination instance and the route map belongs to the same region.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "DestinationInstanceIds"
        ]
      }
    },
    "DestinationInstanceIdsReverseMatch": {
      "Description": "Indicates whether to enable the reverse match method of the DestinationInstanceIds match condition. Valid values:  false (default): If the ID of a route's destination instance is included in DestinationInstanceIds, the route is permitted. true: If the ID of a route's destination instance is not included in DestinationInstanceIds, the route is permitted.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "DestinationInstanceIdsReverseMatch"
        ]
      }
    },
    "SourceInstanceIds": {
      "Description": "A match statement that indicates the list of IDs of the source instances.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "SourceInstanceIds"
        ]
      }
    },
    "DestinationRouteTableIds": {
      "Description": "A match statement that indicates the list of IDs of the destination route tables.  This parameter is valid only when the TransmitDirection parameter is set to RegionOut, and the destination route table and the route map belongs to the same region.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "DestinationRouteTableIds"
        ]
      }
    },
    "DestinationCidrBlocks": {
      "Description": "A match statement that indicates the prefix list.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "DestinationCidrBlocks"
        ]
      }
    },
    "RouteMapId": {
      "Description": "The ID of the route map.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "RouteMapId"
        ]
      }
    },
    "OperateCommunitySet": {
      "Description": "An action statement that operates the community attribute.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "OperateCommunitySet"
        ]
      }
    },
    "DestinationChildInstanceTypes": {
      "Description": "A match statement that indicates the list of IDs of the destination instances.  VPC: VPC VBR: VBR CCN: Mainland China CCN This parameter is valid only when the TransmitDirection parameter is set to RegionOut, and the destination instance and the route map belong to the same region.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "DestinationChildInstanceTypes"
        ]
      }
    },
    "Priority": {
      "Description": "The priority of the route map.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "Priority"
        ]
      }
    },
    "SourceChildInstanceTypes": {
      "Description": "A match statement that indicates the list of IDs of the source instances.  VPC: Virtual Private Cloud (VPC) VBR: Virtual Border Router (VBR) CCN: Mainland China Cloud Connect Network (CCN)",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "SourceChildInstanceTypes"
        ]
      }
    },
    "AsPathMatchMode": {
      "Description": "A match statement. It indicates the mode in which the as-path attribute is matched. Valid values:  Include: Fuzzy match. A route matches the condition if the AS path in the route overlaps the AS path in the match condition. Complete: Exact match. A route matches the condition only when the AS path of the route is the same as the AS path in the match condition.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "AsPathMatchMode"
        ]
      }
    },
    "CidrMatchMode": {
      "Description": "A match statement. It indicates the mode in which the prefix attribute is matched. Valid values:  Include: Fuzzy match. If the prefix of a route is contained in the prefix in the match condition, the route matches the condition.  For example, if the prefix in the match condition is set to 1.1.0.0/16 and the match method is set to Fuzzy Match, the route with the prefix of 1.1.1.0/24 matches the condition.  Complete: Exact match. A route matches the condition only when the prefix of the route is the same as the prefix in the match condition.  For example, if the prefix in the match condition is set to 1.1.0.0/16 and the match method is set to Exact Match, only the route with the prefix of 1.1.1.0/16 matches the condition.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "CidrMatchMode"
        ]
      }
    },
    "MapResult": {
      "Description": "The action that is performed to a route if the route meets all the match conditions.  Permit: The route is permitted. Deny: The route is denied.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "MapResult"
        ]
      }
    },
    "RouteTypes": {
      "Description": "A match statement that indicates the list of route types.  System: System routes generated by the system. Custom: Custom routes added by users. BGP: Routes advertised to BGP.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "RouteTypes"
        ]
      }
    },
    "Preference": {
      "Description": "An action statement that modifies the preference of the route.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "Preference"
        ]
      }
    },
    "CommunityOperateMode": {
      "Description": "An action statement. It indicates the mode in which the community attribute is operated. Valid values:  Additive: Sets a value for the community attribute. Replace: Replaces the value of the community attribute.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "CommunityOperateMode"
        ]
      }
    },
    "CenId": {
      "Description": "The ID of the CEN instance.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "CenId"
        ]
      }
    },
    "NextPriority": {
      "Description": "The priority of the next route map that is associated with the current route map. Value range: 1 to 100.  If this parameter is not set, the current route map is not associated with any route map that is ordered next to the current route map. If this parameter is set to 1, the current route map is associated with the next route map. If this parameter is set to a value other than 1, the priority of the associated route map must be lower than the priority of the current route map, that is, the value of NextPriority must be greater than the value set for Priority. Only when MapResult is set to Permit, the routes which match all the matching conditions will be evaluated by the associated route map that is configured with a specific preference value.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "NextPriority"
        ]
      }
    },
    "PrependAsPath": {
      "Description": "Indicates AS Path prepending when a regional gateway receives or publishes a route.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "PrependAsPath"
        ]
      }
    },
    "CommunityMatchMode": {
      "Description": "A match statement. It indicates the mode in which the community attribute is matched. Valid values:  Include: Fuzzy match. A route matches the condition if the community of the route overlaps the community in the match condition. Complete: Exact match. A route matches the condition only when the community of the route is the same as the community in the match condition.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "CommunityMatchMode"
        ]
      }
    },
    "MatchAsns": {
      "Description": "A match statement that indicates the As path list.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "MatchAsns"
        ]
      }
    },
    "SourceRegionIds": {
      "Description": "A match statement that indicates the list of IDs of the source regions.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "SourceRegionIds"
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
  AsPathMatchMode:
    Description: 'A match statement. It indicates the mode in which the as-path attribute
      is matched. Valid values:  Include: Fuzzy match. A route matches the condition
      if the AS path in the route overlaps the AS path in the match condition. Complete:
      Exact match. A route matches the condition only when the AS path of the route
      is the same as the AS path in the match condition.'
    Type: String
  CenId:
    Description: The ID of the CEN instance.
    Type: String
  CenRegionId:
    Description: The ID of the region to which the CEN instance belongs.
    Type: String
  CidrMatchMode:
    Description: 'A match statement. It indicates the mode in which the prefix attribute
      is matched. Valid values:  Include: Fuzzy match. If the prefix of a route is
      contained in the prefix in the match condition, the route matches the condition.  For
      example, if the prefix in the match condition is set to 1.1.0.0/16 and the match
      method is set to Fuzzy Match, the route with the prefix of 1.1.1.0/24 matches
      the condition.  Complete: Exact match. A route matches the condition only when
      the prefix of the route is the same as the prefix in the match condition.  For
      example, if the prefix in the match condition is set to 1.1.0.0/16 and the match
      method is set to Exact Match, only the route with the prefix of 1.1.1.0/16 matches
      the condition.'
    Type: String
  CommunityMatchMode:
    Description: 'A match statement. It indicates the mode in which the community
      attribute is matched. Valid values:  Include: Fuzzy match. A route matches the
      condition if the community of the route overlaps the community in the match
      condition. Complete: Exact match. A route matches the condition only when the
      community of the route is the same as the community in the match condition.'
    Type: String
  CommunityOperateMode:
    Description: 'An action statement. It indicates the mode in which the community
      attribute is operated. Valid values:  Additive: Sets a value for the community
      attribute. Replace: Replaces the value of the community attribute.'
    Type: String
  Description:
    Description: The description of the route map.
    Type: String
  DestinationChildInstanceTypes:
    Description: 'A match statement that indicates the list of IDs of the destination
      instances.  VPC: VPC VBR: VBR CCN: Mainland China CCN This parameter is valid
      only when the TransmitDirection parameter is set to RegionOut, and the destination
      instance and the route map belong to the same region.'
    Type: Json
  DestinationCidrBlocks:
    Description: A match statement that indicates the prefix list.
    Type: Json
  DestinationInstanceIds:
    Description: A match statement that indicates the list of IDs of the destination
      instances.  This parameter is valid only when the TransmitDirection parameter
      is set to RegionOut, and the destination instance and the route map belongs
      to the same region.
    Type: Json
  DestinationInstanceIdsReverseMatch:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Indicates whether to enable the reverse match method of the DestinationInstanceIds
      match condition. Valid values:  false (default): If the ID of a route''s destination
      instance is included in DestinationInstanceIds, the route is permitted. true:
      If the ID of a route''s destination instance is not included in DestinationInstanceIds,
      the route is permitted.'
    Type: Boolean
  DestinationRouteTableIds:
    Description: A match statement that indicates the list of IDs of the destination
      route tables.  This parameter is valid only when the TransmitDirection parameter
      is set to RegionOut, and the destination route table and the route map belongs
      to the same region.
    Type: Json
  MapResult:
    Description: 'The action that is performed to a route if the route meets all the
      match conditions.  Permit: The route is permitted. Deny: The route is denied.'
    Type: String
  MatchAsns:
    Description: A match statement that indicates the As path list.
    Type: Json
  MatchCommunitySet:
    Description: A match statement that indicates the community set.
    Type: Json
  NextPriority:
    Description: 'The priority of the next route map that is associated with the current
      route map. Value range: 1 to 100.  If this parameter is not set, the current
      route map is not associated with any route map that is ordered next to the current
      route map. If this parameter is set to 1, the current route map is associated
      with the next route map. If this parameter is set to a value other than 1, the
      priority of the associated route map must be lower than the priority of the
      current route map, that is, the value of NextPriority must be greater than the
      value set for Priority. Only when MapResult is set to Permit, the routes which
      match all the matching conditions will be evaluated by the associated route
      map that is configured with a specific preference value.'
    Type: Number
  OperateCommunitySet:
    Description: An action statement that operates the community attribute.
    Type: Json
  Preference:
    Description: An action statement that modifies the preference of the route.
    Type: Number
  PrependAsPath:
    Description: Indicates AS Path prepending when a regional gateway receives or
      publishes a route.
    Type: Json
  Priority:
    Description: The priority of the route map.
    Type: Number
  RouteTypes:
    Description: 'A match statement that indicates the list of route types.  System:
      System routes generated by the system. Custom: Custom routes added by users.
      BGP: Routes advertised to BGP.'
    Type: Json
  SourceChildInstanceTypes:
    Description: 'A match statement that indicates the list of IDs of the source instances.  VPC:
      Virtual Private Cloud (VPC) VBR: Virtual Border Router (VBR) CCN: Mainland China
      Cloud Connect Network (CCN)'
    Type: Json
  SourceInstanceIds:
    Description: A match statement that indicates the list of IDs of the source instances.
    Type: Json
  SourceInstanceIdsReverseMatch:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Indicates whether to enable the reverse match method of the SourceInstanceIds
      match condition. Valid values:  false (default): If the ID of a route''s source
      instance is included in SourceInstanceIds, the route is permitted. true: If
      the ID of a route''s source instance is not included in SourceInstanceIds, the
      route is permitted.'
    Type: Boolean
  SourceRegionIds:
    Description: A match statement that indicates the list of IDs of the source regions.
    Type: Json
  SourceRouteTableIds:
    Description: A match statement that indicates the list of IDs of the source route
      tables.
    Type: Json
  TransmitDirection:
    Description: 'The direction in which the route map is applied. Valid values:  RegionIn:
      The direction in which routes are imported to the regional gateway of the CEN.  For
      example, routes are imported to the regional gateway from an instance in the
      current region or another region.  RegionOut: The direction in which routes
      are exported from the regional gateway of the CEN.  For example, routes are
      exported from the regional gateway of the current region to an instance in the
      same region, or to the regional gateway in another region.'
    Type: String
Resources:
  CENCenRouteMap:
    Properties:
      AsPathMatchMode:
        Ref: AsPathMatchMode
      CenId:
        Ref: CenId
      CenRegionId:
        Ref: CenRegionId
      CidrMatchMode:
        Ref: CidrMatchMode
      CommunityMatchMode:
        Ref: CommunityMatchMode
      CommunityOperateMode:
        Ref: CommunityOperateMode
      Description:
        Ref: Description
      DestinationChildInstanceTypes:
        Ref: DestinationChildInstanceTypes
      DestinationCidrBlocks:
        Ref: DestinationCidrBlocks
      DestinationInstanceIds:
        Ref: DestinationInstanceIds
      DestinationInstanceIdsReverseMatch:
        Ref: DestinationInstanceIdsReverseMatch
      DestinationRouteTableIds:
        Ref: DestinationRouteTableIds
      MapResult:
        Ref: MapResult
      MatchAsns:
        Ref: MatchAsns
      MatchCommunitySet:
        Ref: MatchCommunitySet
      NextPriority:
        Ref: NextPriority
      OperateCommunitySet:
        Ref: OperateCommunitySet
      Preference:
        Ref: Preference
      PrependAsPath:
        Ref: PrependAsPath
      Priority:
        Ref: Priority
      RouteTypes:
        Ref: RouteTypes
      SourceChildInstanceTypes:
        Ref: SourceChildInstanceTypes
      SourceInstanceIds:
        Ref: SourceInstanceIds
      SourceInstanceIdsReverseMatch:
        Ref: SourceInstanceIdsReverseMatch
      SourceRegionIds:
        Ref: SourceRegionIds
      SourceRouteTableIds:
        Ref: SourceRouteTableIds
      TransmitDirection:
        Ref: TransmitDirection
    Type: ALIYUN::CEN::CenRouteMap
Outputs:
  AsPathMatchMode:
    Description: 'A match statement. It indicates the mode in which the as-path attribute
      is matched. Valid values:  Include: Fuzzy match. A route matches the condition
      if the AS path in the route overlaps the AS path in the match condition. Complete:
      Exact match. A route matches the condition only when the AS path of the route
      is the same as the AS path in the match condition.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - AsPathMatchMode
  CenId:
    Description: The ID of the CEN instance.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - CenId
  CenRegionId:
    Description: The ID of the region to which the CEN instance belongs.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - CenRegionId
  CidrMatchMode:
    Description: 'A match statement. It indicates the mode in which the prefix attribute
      is matched. Valid values:  Include: Fuzzy match. If the prefix of a route is
      contained in the prefix in the match condition, the route matches the condition.  For
      example, if the prefix in the match condition is set to 1.1.0.0/16 and the match
      method is set to Fuzzy Match, the route with the prefix of 1.1.1.0/24 matches
      the condition.  Complete: Exact match. A route matches the condition only when
      the prefix of the route is the same as the prefix in the match condition.  For
      example, if the prefix in the match condition is set to 1.1.0.0/16 and the match
      method is set to Exact Match, only the route with the prefix of 1.1.1.0/16 matches
      the condition.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - CidrMatchMode
  CommunityMatchMode:
    Description: 'A match statement. It indicates the mode in which the community
      attribute is matched. Valid values:  Include: Fuzzy match. A route matches the
      condition if the community of the route overlaps the community in the match
      condition. Complete: Exact match. A route matches the condition only when the
      community of the route is the same as the community in the match condition.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - CommunityMatchMode
  CommunityOperateMode:
    Description: 'An action statement. It indicates the mode in which the community
      attribute is operated. Valid values:  Additive: Sets a value for the community
      attribute. Replace: Replaces the value of the community attribute.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - CommunityOperateMode
  Description:
    Description: The description of the route map.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - Description
  DestinationChildInstanceTypes:
    Description: 'A match statement that indicates the list of IDs of the destination
      instances.  VPC: VPC VBR: VBR CCN: Mainland China CCN This parameter is valid
      only when the TransmitDirection parameter is set to RegionOut, and the destination
      instance and the route map belong to the same region.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - DestinationChildInstanceTypes
  DestinationCidrBlocks:
    Description: A match statement that indicates the prefix list.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - DestinationCidrBlocks
  DestinationInstanceIds:
    Description: A match statement that indicates the list of IDs of the destination
      instances.  This parameter is valid only when the TransmitDirection parameter
      is set to RegionOut, and the destination instance and the route map belongs
      to the same region.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - DestinationInstanceIds
  DestinationInstanceIdsReverseMatch:
    Description: 'Indicates whether to enable the reverse match method of the DestinationInstanceIds
      match condition. Valid values:  false (default): If the ID of a route''s destination
      instance is included in DestinationInstanceIds, the route is permitted. true:
      If the ID of a route''s destination instance is not included in DestinationInstanceIds,
      the route is permitted.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - DestinationInstanceIdsReverseMatch
  DestinationRouteTableIds:
    Description: A match statement that indicates the list of IDs of the destination
      route tables.  This parameter is valid only when the TransmitDirection parameter
      is set to RegionOut, and the destination route table and the route map belongs
      to the same region.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - DestinationRouteTableIds
  MapResult:
    Description: 'The action that is performed to a route if the route meets all the
      match conditions.  Permit: The route is permitted. Deny: The route is denied.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - MapResult
  MatchAsns:
    Description: A match statement that indicates the As path list.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - MatchAsns
  MatchCommunitySet:
    Description: A match statement that indicates the community set.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - MatchCommunitySet
  NextPriority:
    Description: 'The priority of the next route map that is associated with the current
      route map. Value range: 1 to 100.  If this parameter is not set, the current
      route map is not associated with any route map that is ordered next to the current
      route map. If this parameter is set to 1, the current route map is associated
      with the next route map. If this parameter is set to a value other than 1, the
      priority of the associated route map must be lower than the priority of the
      current route map, that is, the value of NextPriority must be greater than the
      value set for Priority. Only when MapResult is set to Permit, the routes which
      match all the matching conditions will be evaluated by the associated route
      map that is configured with a specific preference value.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - NextPriority
  OperateCommunitySet:
    Description: An action statement that operates the community attribute.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - OperateCommunitySet
  Preference:
    Description: An action statement that modifies the preference of the route.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - Preference
  PrependAsPath:
    Description: Indicates AS Path prepending when a regional gateway receives or
      publishes a route.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - PrependAsPath
  Priority:
    Description: The priority of the route map.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - Priority
  RouteMapId:
    Description: The ID of the route map.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - RouteMapId
  RouteTypes:
    Description: 'A match statement that indicates the list of route types.  System:
      System routes generated by the system. Custom: Custom routes added by users.
      BGP: Routes advertised to BGP.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - RouteTypes
  SourceChildInstanceTypes:
    Description: 'A match statement that indicates the list of IDs of the source instances.  VPC:
      Virtual Private Cloud (VPC) VBR: Virtual Border Router (VBR) CCN: Mainland China
      Cloud Connect Network (CCN)'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - SourceChildInstanceTypes
  SourceInstanceIds:
    Description: A match statement that indicates the list of IDs of the source instances.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - SourceInstanceIds
  SourceInstanceIdsReverseMatch:
    Description: 'Indicates whether to enable the reverse match method of the SourceInstanceIds
      match condition. Valid values:  false (default): If the ID of a route''s source
      instance is included in SourceInstanceIds, the route is permitted. true: If
      the ID of a route''s source instance is not included in SourceInstanceIds, the
      route is permitted.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - SourceInstanceIdsReverseMatch
  SourceRegionIds:
    Description: A match statement that indicates the list of IDs of the source regions.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - SourceRegionIds
  SourceRouteTableIds:
    Description: A match statement that indicates the list of IDs of the source route
      tables.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - SourceRouteTableIds
  TransmitDirection:
    Description: 'The direction in which the route map is applied. Valid values:  RegionIn:
      The direction in which routes are imported to the regional gateway of the CEN.  For
      example, routes are imported to the regional gateway from an instance in the
      current region or another region.  RegionOut: The direction in which routes
      are exported from the regional gateway of the CEN.  For example, routes are
      exported from the regional gateway of the current region to an instance in the
      same region, or to the regional gateway in another region.'
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - TransmitDirection
```


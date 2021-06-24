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
|SourceInstanceIdsReverseMatch|Boolean|No|Yes|Specifies whether the match is successful if the source instance ID is not in the list specified by SourceInstanceIds.|Default value: false. Valid values:-   false: The match is successful if the source instance ID is in the list specified by SourceInstanceIds.
-   true: The match is successful if the source instance ID is not in the list specified by SourceInstanceIds. |
|TransmitDirection|String|Yes|No|The direction in which the route map is to be applied.|Valid values:-   RegionIn: Routes are advertised to Cloud Enterprise Network \(CEN\) regional gateways. For example, routes are advertised from network instances deployed in the current region or routes deployed in other regions to gateways deployed in the current region.
-   RegionOut: Routes are advertised from CEN regional gateways. For example, routes are advertised from gateways deployed in the current region to network instances deployed in the same region, or to gateways deployed in other regions. |
|MatchCommunitySet|List|No|Yes|The community set to be matched by using a match statement.|Specify each community in the nn:nn format. Valid values of nn: 1 to 65535.

A maximum of 32 communities are supported.

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
|DestinationCidrBlocks|List|No|Yes|The prefixes to be matched by using a match statement.|Specify the prefixes in the CIDR format. A maximum of 32 CIDR blocks can be specified. |
|OperateCommunitySet|List|No|Yes|The community set to be managed by using an action statement.|Specify each community in the nn:nn format. Valid values of nn: 1 to 65535.

A maximum of 32 communities can be specified.

Each community must comply with RFC 1997. RFC 8092 that defines BGP large communities is not supported. **Note:** If the configurations of the communities are incorrect, routes may not be advertised to your data center. |
|DestinationChildInstanceTypes|List|No|Yes|The destination instance types to be matched by using a match statement.|Valid values:-   VPC
-   VBR

**Note:** The destination instance types are valid only when the route map is applied to scenarios where routes are advertised from gateways in the current region to instances in the current region. |
|Priority|Integer|Yes|Yes|The priority of the route map.|Valid values: 1 to 100. A small value indicates a high priority. **Note:** After you specify a priority value for a route map, you cannot set the same priority value for another route map that is applied in the same region and direction. The system filters routes based on route maps that start from the route map with the lowest priority value. Therefore, set appropriate priority values to sort the route maps in the desired order. |
|SourceChildInstanceTypes|List|No|Yes|The source instance types to be matched by using a match statement.|Valid values:-   VPC
-   VBR |
|AsPathMatchMode|String|No|Yes|The mode in which the autonomous system \(AS\) paths are matched by using a match statement.|Valid values:-   Include: fuzzy match. A route meets the match condition if the AS path of the route overlaps with that specified in the match condition.
-   Complete: exact match. A route meets the match condition only if the AS path of the route is the same as that specified in the match condition. |
|CidrMatchMode|String|No|Yes|The mode in which the prefixes are matched by using a match statement.|Valid values:-   Include: fuzzy match. A route meets the match condition if the route prefix specified in the match condition contains the prefix of the route. For example, if you set the match condition to 1.1.0.0/16 and fuzzy match is applied, the route whose prefix is 1.1.1.0/24 meets the match condition.
-   Complete: exact match. A route meets the match condition only if the prefix of the route is the same as that specified in the match condition. For example, if you set the match condition to 1.1.0.0/16 and exact match is applied, only the route whose prefix is 1.1.0.0/16 meets the match condition. |
|MapResult|String|Yes|Yes|The action to be performed on a route if the route matches all the match conditions.|Valid values:-   Permit: allows the routes that are matched.
-   Deny: rejects the routes that are matched. |
|RouteTypes|List|No|Yes|The types of routes to be matched by using a match statement.|Valid values:-   System: system routes that are generated by the system
-   Custom: custom routes that are created by users
-   BGP: BGP routes that are advertised to BGP

You can enter multiple types.|
|Preference|Integer|No|Yes|The route priority to be modified by using an action statement.|Valid values: 1 to 100.

Default value: 50.

A small value indicates a high priority.|
|CommunityOperateMode|String|No|Yes|The mode in which communities are managed by using an action statement.|Valid values:-   Additive: Communities are added.
-   Replace: Communities are replaced. |
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
-   PrependAsPath: the AS paths that are prepended by using an action statement when regional gateways receive or advertise routes.
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
      "Description": "The IDs of source instances to be advertised do not support match statements. Valid values: \n false (default value): If the source instance ID is in the SourceInstanceIds field, the match is successful. \n true: If the source instance ID is not in the SourceInstanceIds field, the match is successful.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "TransmitDirection": {
      "Type": "String",
      "Description": "The direction in which the route map is applied. Valid values: \n RegionIn: Routes are advertised to CEN gateways. \n For example, routes are advertised from network instances deployed in the current region or other regions to the gateways deployed in the current region. \n RegionOut: Routes are advertised from CEN gateways. \n For example, routes are advertised from gateways deployed in the current region to network instances or gateways deployed in other regions."
    },
    "MatchCommunitySet": {
      "Type": "Json",
      "Description": "Match statements are used to match the Communities. Enter each Community in the format of nn:nn. Valid values of nn: 1 to 65535. You can enter at most 32 Communities. Each Community must comply with RFC 1997. RFC 8092 is not supported. \n Note If the configurations of the Communities are incorrect, routes may not be advertised to the on-premises data center."
    },
    "CenRegionId": {
      "Type": "String",
      "Description": "The region where the CEN instance is deployed. You can call the DescribeRegions operation to query region IDs."
    },
    "SourceRouteTableIds": {
      "Type": "Json",
      "Description": "Match statements are used to match source route table IDs of the routes. You can enter at most 32 route table IDs."
    },
    "DestinationInstanceIds": {
      "Type": "Json",
      "Description": "Match statements are used to match the destination instance IDs. \n You can enter instance IDs of the following types: VPC, VBR, CCN in mainland China, and SAG. You can enter at most 32 instance IDs. \n Note The destination instance IDs are valid only when the route map is applied to scenarios where routes are advertised from gateways in the current region to instances in the current region."
    },
    "DestinationInstanceIdsReverseMatch": {
      "Type": "Boolean",
      "Description": "The IDs of destination instances to be advertised do not support match statements. Valid values: \n false(default value): If the ID of the destination instance to be advertised is in the DestinationInstanceIds field, the match is successful. \n true: If the ID of the destination instance to be advertised is not in the DestinationInstanceIds filed, the match is successful.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "SourceInstanceIds": {
      "Type": "Json",
      "Description": "Match statements are used to match source instance IDs of the routes. \n You can enter instance IDs of the following types: virtual private cloud (VPC), virtual border router (VBR), Cloud Connect Network (CCN) in mainland China, Smart Access Gateway (SAG). You can enter at most 32 instance IDs."
    },
    "DestinationRouteTableIds": {
      "Type": "Json",
      "Description": "Match statements are used to match the IDs of the destination route tables. You can enter at most 32 route table IDs. \n Note The destination route table IDs are valid only when the route map is applied to scenarios where routes are advertised from gateways in the current region to route tables in the current region."
    },
    "DestinationCidrBlocks": {
      "Type": "Json",
      "Description": "Match statements are used to match the routing prefixes. The CIDR format is used. You can enter at most 32 CIDR blocks."
    },
    "OperateCommunitySet": {
      "Type": "Json",
      "Description": "Action statements are used to operate the Communities. Valid values: Enter each Community in the format of nn:nn. Valid values of nn: 1 to 65535. You can enter at most 32 Communities. Each Community must comply with RFC 1997. RFC 8092 is not supported. \n Note If the configurations of the Communities are incorrect, routes may not be advertised to the on-premises data center."
    },
    "DestinationChildInstanceTypes": {
      "Type": "Json",
      "Description": "Match statements are used to match the destination instance types. Valid values: \n VPC: VPCs. \n VBR: VBRs. \n CCN: CCN instances in mainland China. \n Note The destination instance types are valid only when the route map is applied to scenarios where routes are advertised from gateways in the current region to instances in the current region."
    },
    "Priority": {
      "Type": "Number",
      "Description": "The priority of the route map. Valid values: 1 to 100 . A lower value indicates a higher priority. \n Note In the same region, for route maps that are applied in the same direction, the priority is unique. When a route map is implemented, the system matches conditions with a route map whose priority number is the smallest. Therefore, make sure that you set priorities for route maps to meet your requirements."
    },
    "SourceChildInstanceTypes": {
      "Type": "Json",
      "Description": "Match statements are used to match source instance types of the routes. Valid values: \n VPC: VPCs. \n VBR: VBRs. \n CCN: CCN instances in mainland China."
    },
    "AsPathMatchMode": {
      "Type": "String",
      "Description": "Match statements are used to match the AS paths. Valid values:\n Include: uses fuzzy match. If the AS path in the condition overlaps with the AS path in the route, the match is successful.\n Complete: uses exact match. Only when the AS path in the condition is the same as the AS path in the route, the match is successful."
    },
    "CidrMatchMode": {
      "Type": "String",
      "Description": "Match statements are used to match the prefixes. Valid values: \n Include: uses fuzzy match. If the routing prefix in the condition contains the routing prefix of the route, the match is successful. \n For example, the 1.1.0.0/16 policy can match the 1.1.1.0/24 route. \n Complete: uses exact match. Only when the routing prefix in the condition is the same as the routing prefix of the route, the match is successful. \n For example, the 1.1.0.0/16 policy can match the 1.1.0.0/16 route."
    },
    "MapResult": {
      "Type": "String",
      "Description": "The route map behavior after all conditions are matched. Valid values: \n Permit: allows the routes that are matched. \n Deny: rejects the routes that are matched."
    },
    "RouteTypes": {
      "Type": "Json",
      "Description": "Match statements are used to match the route types. Valid values: \n System: system routes that are generated by the system. \n Custom: custom routes that are created by users. \n BGP: Border Gateway Protocol (BGP) routes that are advertised to BGP. \n You can enter multiple types."
    },
    "Preference": {
      "Type": "Number",
      "Description": "Action statements are used to modify route priorities. Valid values: 1 to 100. Default value: 50. A smaller number indicates a higher priority."
    },
    "CommunityOperateMode": {
      "Type": "String",
      "Description": "Action statements are used to operate the Communities. Valid values: \n Additive: adds. \n Replace: replaces."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the Cloud Enterprise Network (CEN) instance."
    },
    "NextPriority": {
      "Type": "Number",
      "Description": "The priority of the next associated route map. Valid values: 1 to 100. \n If the priority is not set, no next route map is associated with the current route map. \n If the priority is set to 1, the next route map is associated with the current route map. \n If the priority is set and the value is not 1, the priority of the associated route map must be higher than that of the current route map. \n Only when the MapResult parameter is set to Permit, the matched routes continue to match the next associated route maps."
    },
    "PrependAsPath": {
      "Type": "Json",
      "Description": "AS paths are attached when regional gateways receive or advertise routes. \n For route maps that are applied in different directions, the requirements for AS paths to be attached are different: \n For the inbound direction: You must specify the list of source instance IDs and the source region in the condition to be matched. The source region must be the same as the region where the route map is applied. \n For the outbound direction: You must specify the list of destination instance IDs in the condition to be matched."
    },
    "CommunityMatchMode": {
      "Type": "String",
      "Description": "Match statements are used to match the Communities. Valid values: \n Include: uses fuzzy match. If the Community in the condition overlaps with the Community of the route, the match is successful. \n Complete: uses exact match. Only when the Community in the condition is the same as the Community of the route, the match is successful."
    },
    "MatchAsns": {
      "Type": "Json",
      "Description": "Match statements are used to match AS paths of the routes. An AS path is a mandatory attribute, which describes the AS number through which a BGP route passes when the BGP route is advertised. \n Only the AS-SEQUENCE parameter is supported. The AS-SET, AS-CONFED-SEQUENCE, and AS-CONFED-SET parameters are not supported. Specifically, only the AS number list is supported. Sets and sub-lists are not supported."
    },
    "SourceRegionIds": {
      "Type": "Json",
      "Description": "Match statements are used to match source region IDs of the routes. You can enter at most 32 region IDs."
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
    "RouteMapId": {
      "Description": "The ID of the route map.",
      "Value": {
        "Fn::GetAtt": [
          "CENCenRouteMap",
          "RouteMapId"
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
    Description: "Match statements are used to match the AS paths. Valid values:\n\
      \ Include: uses fuzzy match. If the AS path in the condition overlaps with the\
      \ AS path in the route, the match is successful.\n Complete: uses exact match.\
      \ Only when the AS path in the condition is the same as the AS path in the route,\
      \ the match is successful."
    Type: String
  CenId:
    Description: The ID of the Cloud Enterprise Network (CEN) instance.
    Type: String
  CenRegionId:
    Description: The region where the CEN instance is deployed. You can call the DescribeRegions
      operation to query region IDs.
    Type: String
  CidrMatchMode:
    Description: "Match statements are used to match the prefixes. Valid values: \n\
      \ Include: uses fuzzy match. If the routing prefix in the condition contains\
      \ the routing prefix of the route, the match is successful. \n For example,\
      \ the 1.1.0.0/16 policy can match the 1.1.1.0/24 route. \n Complete: uses exact\
      \ match. Only when the routing prefix in the condition is the same as the routing\
      \ prefix of the route, the match is successful. \n For example, the 1.1.0.0/16\
      \ policy can match the 1.1.0.0/16 route."
    Type: String
  CommunityMatchMode:
    Description: "Match statements are used to match the Communities. Valid values:\
      \ \n Include: uses fuzzy match. If the Community in the condition overlaps with\
      \ the Community of the route, the match is successful. \n Complete: uses exact\
      \ match. Only when the Community in the condition is the same as the Community\
      \ of the route, the match is successful."
    Type: String
  CommunityOperateMode:
    Description: "Action statements are used to operate the Communities. Valid values:\
      \ \n Additive: adds. \n Replace: replaces."
    Type: String
  Description:
    Description: The description of the route map.
    Type: String
  DestinationChildInstanceTypes:
    Description: "Match statements are used to match the destination instance types.\
      \ Valid values: \n VPC: VPCs. \n VBR: VBRs. \n CCN: CCN instances in mainland\
      \ China. \n Note The destination instance types are valid only when the route\
      \ map is applied to scenarios where routes are advertised from gateways in the\
      \ current region to instances in the current region."
    Type: Json
  DestinationCidrBlocks:
    Description: Match statements are used to match the routing prefixes. The CIDR
      format is used. You can enter at most 32 CIDR blocks.
    Type: Json
  DestinationInstanceIds:
    Description: "Match statements are used to match the destination instance IDs.\
      \ \n You can enter instance IDs of the following types: VPC, VBR, CCN in mainland\
      \ China, and SAG. You can enter at most 32 instance IDs. \n Note The destination\
      \ instance IDs are valid only when the route map is applied to scenarios where\
      \ routes are advertised from gateways in the current region to instances in\
      \ the current region."
    Type: Json
  DestinationInstanceIdsReverseMatch:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "The IDs of destination instances to be advertised do not support\
      \ match statements. Valid values: \n false(default value): If the ID of the\
      \ destination instance to be advertised is in the DestinationInstanceIds field,\
      \ the match is successful. \n true: If the ID of the destination instance to\
      \ be advertised is not in the DestinationInstanceIds filed, the match is successful."
    Type: Boolean
  DestinationRouteTableIds:
    Description: "Match statements are used to match the IDs of the destination route\
      \ tables. You can enter at most 32 route table IDs. \n Note The destination\
      \ route table IDs are valid only when the route map is applied to scenarios\
      \ where routes are advertised from gateways in the current region to route tables\
      \ in the current region."
    Type: Json
  MapResult:
    Description: "The route map behavior after all conditions are matched. Valid values:\
      \ \n Permit: allows the routes that are matched. \n Deny: rejects the routes\
      \ that are matched."
    Type: String
  MatchAsns:
    Description: "Match statements are used to match AS paths of the routes. An AS\
      \ path is a mandatory attribute, which describes the AS number through which\
      \ a BGP route passes when the BGP route is advertised. \n Only the AS-SEQUENCE\
      \ parameter is supported. The AS-SET, AS-CONFED-SEQUENCE, and AS-CONFED-SET\
      \ parameters are not supported. Specifically, only the AS number list is supported.\
      \ Sets and sub-lists are not supported."
    Type: Json
  MatchCommunitySet:
    Description: "Match statements are used to match the Communities. Enter each Community\
      \ in the format of nn:nn. Valid values of nn: 1 to 65535. You can enter at most\
      \ 32 Communities. Each Community must comply with RFC 1997. RFC 8092 is not\
      \ supported. \n Note If the configurations of the Communities are incorrect,\
      \ routes may not be advertised to the on-premises data center."
    Type: Json
  NextPriority:
    Description: "The priority of the next associated route map. Valid values: 1 to\
      \ 100. \n If the priority is not set, no next route map is associated with the\
      \ current route map. \n If the priority is set to 1, the next route map is associated\
      \ with the current route map. \n If the priority is set and the value is not\
      \ 1, the priority of the associated route map must be higher than that of the\
      \ current route map. \n Only when the MapResult parameter is set to Permit,\
      \ the matched routes continue to match the next associated route maps."
    Type: Number
  OperateCommunitySet:
    Description: "Action statements are used to operate the Communities. Valid values:\
      \ Enter each Community in the format of nn:nn. Valid values of nn: 1 to 65535.\
      \ You can enter at most 32 Communities. Each Community must comply with RFC\
      \ 1997. RFC 8092 is not supported. \n Note If the configurations of the Communities\
      \ are incorrect, routes may not be advertised to the on-premises data center."
    Type: Json
  Preference:
    Description: 'Action statements are used to modify route priorities. Valid values:
      1 to 100. Default value: 50. A smaller number indicates a higher priority.'
    Type: Number
  PrependAsPath:
    Description: "AS paths are attached when regional gateways receive or advertise\
      \ routes. \n For route maps that are applied in different directions, the requirements\
      \ for AS paths to be attached are different: \n For the inbound direction: You\
      \ must specify the list of source instance IDs and the source region in the\
      \ condition to be matched. The source region must be the same as the region\
      \ where the route map is applied. \n For the outbound direction: You must specify\
      \ the list of destination instance IDs in the condition to be matched."
    Type: Json
  Priority:
    Description: "The priority of the route map. Valid values: 1 to 100 . A lower\
      \ value indicates a higher priority. \n Note In the same region, for route maps\
      \ that are applied in the same direction, the priority is unique. When a route\
      \ map is implemented, the system matches conditions with a route map whose priority\
      \ number is the smallest. Therefore, make sure that you set priorities for route\
      \ maps to meet your requirements."
    Type: Number
  RouteTypes:
    Description: "Match statements are used to match the route types. Valid values:\
      \ \n System: system routes that are generated by the system. \n Custom: custom\
      \ routes that are created by users. \n BGP: Border Gateway Protocol (BGP) routes\
      \ that are advertised to BGP. \n You can enter multiple types."
    Type: Json
  SourceChildInstanceTypes:
    Description: "Match statements are used to match source instance types of the\
      \ routes. Valid values: \n VPC: VPCs. \n VBR: VBRs. \n CCN: CCN instances in\
      \ mainland China."
    Type: Json
  SourceInstanceIds:
    Description: "Match statements are used to match source instance IDs of the routes.\
      \ \n You can enter instance IDs of the following types: virtual private cloud\
      \ (VPC), virtual border router (VBR), Cloud Connect Network (CCN) in mainland\
      \ China, Smart Access Gateway (SAG). You can enter at most 32 instance IDs."
    Type: Json
  SourceInstanceIdsReverseMatch:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "The IDs of source instances to be advertised do not support match\
      \ statements. Valid values: \n false (default value): If the source instance\
      \ ID is in the SourceInstanceIds field, the match is successful. \n true: If\
      \ the source instance ID is not in the SourceInstanceIds field, the match is\
      \ successful."
    Type: Boolean
  SourceRegionIds:
    Description: Match statements are used to match source region IDs of the routes.
      You can enter at most 32 region IDs.
    Type: Json
  SourceRouteTableIds:
    Description: Match statements are used to match source route table IDs of the
      routes. You can enter at most 32 route table IDs.
    Type: Json
  TransmitDirection:
    Description: "The direction in which the route map is applied. Valid values: \n\
      \ RegionIn: Routes are advertised to CEN gateways. \n For example, routes are\
      \ advertised from network instances deployed in the current region or other\
      \ regions to the gateways deployed in the current region. \n RegionOut: Routes\
      \ are advertised from CEN gateways. \n For example, routes are advertised from\
      \ gateways deployed in the current region to network instances or gateways deployed\
      \ in other regions."
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
  RouteMapId:
    Description: The ID of the route map.
    Value:
      Fn::GetAtt:
      - CENCenRouteMap
      - RouteMapId
```


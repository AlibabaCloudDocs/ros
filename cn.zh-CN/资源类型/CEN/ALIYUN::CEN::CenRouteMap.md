# ALIYUN::CEN::CenRouteMap

ALIYUN::CEN::CenRouteMap类型用于创建路由策略。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|路由策略的描述。|无|
|SourceInstanceIdsReverseMatch|Boolean|否|是|路由传递源实例ID列表不在SourceInstanceIds中时，是否匹配通过。|取值： -   false（默认值）：路由传递源实例ID在SourceInstanceIds中时，匹配通过。
-   true：路由传递源实例ID不在SourceInstanceIds中时，匹配通过。 |
|TransmitDirection|String|是|否|路由策略应用的方向。|取值： -   RegionIn：路由传入云企业网地域网关的方向。例如：路由从本地域网络实例发布到本地域网关，或其他地域的路由发布到本地域网关。
-   RegionOut：路由传出云企业网地域网关的方向。例如：路由从本地域网关发布到本地域下其他网络实例，或发布到其他地域网关。 |
|MatchCommunitySet|List|否|是|匹配Community集合。|match语句。 Community格式为nn:nn，nn取值范围：1~65,535。

 最多支持32个Community。

 Community需要符合RFC 1997，不支持Large Community（RFC 8092）。 **说明：** Community配置错误可能导致路由不能发布到IDC侧。 |
|CenRegionId|String|是|否|云企业网所在的地域。|无|
|SourceRouteTableIds|List|否|是|匹配路由的源路由表ID列表。|match语句。 最多支持32个路由表ID。 |
|DestinationInstanceIds|List|否|是|匹配路由的目的实例ID列表。|match语句。 支持输入专有网络实例ID、边界路由器实例ID、云连接网实例ID、智能接入网关实例ID。

 最多支持32个实例ID。 **说明：** 目的实例ID列表仅在路由策略应用方向（TransmitDirection）为出地域网关方向（RegionOut）且目的实例ID为本地域下实例时有效。 |
|DestinationInstanceIdsReverseMatch|Boolean|否|是|路由传递目的实例ID列表不在DestinationInstanceIds中时，是否匹配通过。|取值： -   false（默认值）：路由传递目的实例ID在DestinationInstanceIds中时，匹配通过。
-   true：路由传递目的实例ID不在DestinationInstanceIds中时，匹配通过。 |
|SourceInstanceIds|List|否|是|匹配路由的源实例ID列表。|match语句。 支持输入专有网络实例ID、边界路由器实例ID、云连接网实例ID、智能接入网关实例ID。

 最多支持32个实例ID。|
|DestinationRouteTableIds|List|否|是|匹配路由的目的路由表ID列表。|match语句。 最多支持32个路由表ID。 |
|DestinationCidrBlocks|List|否|是|匹配路由的前缀列表。|match语句。 使用CIDR格式，最多支持32个CIDR。 |
|OperateCommunitySet|List|否|是|操作Community的集合。|action语句。 Community格式为nn:nn，nn取值范围为1~65535。

 最多支持32个Community。

 Community需要符合RFC 1997，不支持Large community（RFC 8092）。 **说明：** Community配置错误可能导致路由不能发布到IDC侧。 |
|DestinationChildInstanceTypes|List|否|是|匹配路由的目的实例类型列表。|match语句。取值： -   VPC：专有网络。
-   VBR：边界路由器。
-   CCN：云连接网。

 **说明：** 目的实例类型仅路由策略应用方向（TransmitDirection）为出地域网关方向（RegionOut）且目的实例类型为本地域下实例类型时有效。 |
|Priority|Integer|是|是|路由策略的优先级。|取值：1~100。数字越小，优先级越高。 **说明：** 同地域同路由策略应用方向的路由策略优先级唯一。执行路由策略时，系统从优先级数字最小的路由策略开始匹配条件语句，因此在指定路由策略优先级时，要注意符合期望的匹配顺序。 |
|SourceChildInstanceTypes|List|否|是|匹配路由的源实例类型列表。|match语句。取值： -   VPC：专有网络。
-   VBR：边界路由器。
-   CCN：云连接网。 |
|AsPathMatchMode|String|否|是|匹配as-path模式。|match语句。取值： -   Include：模糊匹配，匹配条件中的AS Path与被匹配路由的AS Path有重叠即判定为匹配成功。
-   Complete：精确匹配，匹配条件中的AS Path必须与被匹配路由的AS Path一致，才判定为匹配成功。 |
|CidrMatchMode|String|否|是|匹配前缀模式。|match语句。取值： -   Include：模糊匹配。匹配条件中的路由前缀包含被匹配路由的路由前缀即判定为匹配成功。例如：定义1.1.0.0/16的策略可以模糊匹配到1.1.1.0/24的路由。
-   Complete：精确匹配。匹配条件中的路由前缀必须与被匹配路由的路由前缀一致，才判定为匹配成功。例如：定义1.1.0.0/16的策略仅可以精确匹配到1.1.0.0/16的路由。 |
|MapResult|String|是|是|所有匹配条件通过后的策略行为。|取值： -   Permit：允许通过被匹配的路由。
-   Deny：拒绝通过被匹配的路由。 |
|RouteTypes|List|否|是|匹配路由的类型列表。|match语句。取值： -   System：系统路由，由系统自动生成的路由。
-   Custom：用户路由，由用户手动添加的自定义路由。
-   BGP：BGP路由，通告至BGP中的路由。

 支持输入多种类型。|
|Preference|Integer|否|是|修改路由的优先级。|action语句。 取值范围：1~100。

 默认值：50。

 数字越小，优先级越高。|
|CommunityOperateMode|String|否|是|操作Community的模式。|action语句。取值： -   Additive：添加。
-   Replace：替换。 |
|CenId|String|是|否|云企业网的ID。|无|
|NextPriority|Integer|否|是|关联的下一条路由策略的优先级。|取值范围：1~100。 -   当未配置关联优先级时，路由策略无关联的下一条路由策略。
-   当关联优先级取值为1时，路由策略关联当前路由策略的下一条路由策略。
-   当关联优先级取值非1时，路由策略关联优先级必须大于当前路由策略的优先级。

 仅当MapResult取值为Permit时，匹配通过的路由才会继续匹配关联的下一条路由策略。|
|PrependAsPath|List|否|是|地域网关接收或发布路由时追加AS Path。|action语句。路由策略应用方向不同，配置追加AS Path的要求也不同，具体如下： -   入地域网关方向配置追加AS Path时，匹配条件中必须配置源实例ID列表和源地域，且源地域必须与路由策略应用的地域一致。
-   出地域网关方向配置追加AS Path时，匹配条件中必须配置目的实例ID列表。 |
|CommunityMatchMode|String|否|是|匹配Community模式。|match语句。取值： -   Include：模糊匹配，匹配条件中的Community与被匹配路由的Community有重叠即判定为匹配成功。
-   Complete：精确匹配，匹配条件中的Community必须与被匹配路由的Community一致，才判定为匹配成功。 |
|MatchAsns|List|否|是|匹配路由的as-path列表。|match语句。 as-path是公认强制属性，描述了一条BGP路由在传递过程中所经过的AS的号码。

 仅支持AS SEQUENCE，不支持AS SET、AS CONFED SEQUENCE和AS CONFED SET，即只能是AS号列表，不支持集合和子列表。|
|SourceRegionIds|List|否|是|匹配路由的源地域ID列表。|match语句。 最多支持32个地域ID。 |

## 返回值

Fn::GetAtt

-   Description：路由策略的描述。
-   SourceInstanceIdsReverseMatch：路由传递源实例ID列表不在SourceInstanceIds中时，是否匹配通过。
-   TransmitDirection：路由策略应用的方向。
-   MatchCommunitySet：匹配Community集合。
-   CenRegionId：云企业网所在的地域。
-   SourceRouteTableIds：匹配路由的源路由表ID列表。
-   DestinationInstanceIds：匹配路由的目的实例ID列表。
-   DestinationInstanceIdsReverseMatch：路由传递目的实例ID列表不在DestinationInstanceIds中时，是否匹配通过。
-   SourceInstanceIds：匹配路由的源实例ID列表。
-   DestinationRouteTableIds：匹配路由的目的路由表ID列表。
-   DestinationCidrBlocks：匹配路由的前缀列表。
-   RouteMapId：路由策略的ID。
-   OperateCommunitySet：操作Community的集合。
-   DestinationChildInstanceTypes：匹配路由的目的实例类型列表。
-   Priority：路由策略的优先级。
-   SourceChildInstanceTypes：匹配路由的源实例类型列表。
-   AsPathMatchMode：匹配as-path模式。
-   CidrMatchMode：匹配前缀模式。
-   MapResult：所有匹配条件通过后的策略行为。
-   RouteTypes：匹配路由的类型列表。
-   Preference：修改路由的优先级。
-   CommunityOperateMode：操作Community的模式。
-   CenId：云企业网的ID。
-   NextPriority：关联的下一条路由策略的优先级。
-   PrependAsPath：地域网关接收或发布路由时追加AS Path。
-   CommunityMatchMode：匹配Community模式。
-   MatchAsns：匹配路由的as-path列表。
-   SourceRegionIds：匹配路由的源地域ID列表。

## 示例

`JSON`格式

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

`YAML`格式

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


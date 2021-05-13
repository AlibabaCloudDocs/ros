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
|SourceInstanceIdsReverseMatch|Boolean|否|是|路由传递源实例ID列表不在SourceInstanceIds中时，是否匹配通过。|取值：-   false（默认值）：路由传递源实例ID在SourceInstanceIds中时，匹配通过。
-   true：路由传递源实例ID不在SourceInstanceIds中时，匹配通过。 |
|TransmitDirection|String|是|否|路由策略应用的方向。|取值：-   RegionIn：路由传入云企业网地域网关的方向。例如：路由从本地域网络实例发布到本地域网关，或其他地域的路由发布到本地域网关。
-   RegionOut：路由传出云企业网地域网关的方向。例如：路由从本地域网关发布到本地域下其他网络实例，或发布到其他地域网关。 |
|MatchCommunitySet|List|否|是|匹配Community集合。|match语句。Community格式为nn:nn，nn取值范围：1~65,535。

最多支持32个Community。

Community需要符合RFC 1997，不支持Large Community（RFC 8092）。**说明：** Community配置错误可能导致路由不能发布到IDC侧。 |
|CenRegionId|String|是|否|云企业网所在的地域。|无|
|SourceRouteTableIds|List|否|是|匹配路由的源路由表ID列表。|match语句。最多支持32个路由表ID。 |
|DestinationInstanceIds|List|否|是|匹配路由的目的实例ID列表。|match语句。支持输入专有网络实例ID、边界路由器实例ID、智能接入网关实例ID。

最多支持32个实例ID。**说明：** 目的实例ID列表仅在路由策略应用方向（TransmitDirection）为出地域网关方向（RegionOut）且目的实例ID为本地域下实例时有效。 |
|DestinationInstanceIdsReverseMatch|Boolean|否|是|路由传递目的实例ID列表不在DestinationInstanceIds中时，是否匹配通过。|取值：-   false（默认值）：路由传递目的实例ID在DestinationInstanceIds中时，匹配通过。
-   true：路由传递目的实例ID不在DestinationInstanceIds中时，匹配通过。 |
|SourceInstanceIds|List|否|是|匹配路由的源实例ID列表。|match语句。支持输入专有网络实例ID、边界路由器实例ID、智能接入网关实例ID。

最多支持32个实例ID。|
|DestinationRouteTableIds|List|否|是|匹配路由的目的路由表ID列表。|match语句。最多支持32个路由表ID。 |
|DestinationCidrBlocks|List|否|是|匹配路由的前缀列表。|match语句。使用CIDR格式，最多支持32个CIDR。 |
|OperateCommunitySet|List|否|是|操作Community的集合。|action语句。Community格式为nn:nn，nn取值范围为1~65535。

最多支持32个Community。

Community需要符合RFC 1997，不支持Large community（RFC 8092）。**说明：** Community配置错误可能导致路由不能发布到IDC侧。 |
|DestinationChildInstanceTypes|List|否|是|匹配路由的目的实例类型列表。|match语句。取值：-   VPC：专有网络。
-   VBR：边界路由器。

**说明：** 目的实例类型仅路由策略应用方向（TransmitDirection）为出地域网关方向（RegionOut）且目的实例类型为本地域下实例类型时有效。 |
|Priority|Integer|是|是|路由策略的优先级。|取值：1~100。数字越小，优先级越高。**说明：** 同地域同路由策略应用方向的路由策略优先级唯一。执行路由策略时，系统从优先级数字最小的路由策略开始匹配条件语句，因此在指定路由策略优先级时，要注意符合期望的匹配顺序。 |
|SourceChildInstanceTypes|List|否|是|匹配路由的源实例类型列表。|match语句。取值：-   VPC：专有网络。
-   VBR：边界路由器。 |
|AsPathMatchMode|String|否|是|匹配as-path模式。|match语句。取值：-   Include：模糊匹配，匹配条件中的AS Path与被匹配路由的AS Path有重叠即判定为匹配成功。
-   Complete：精确匹配，匹配条件中的AS Path必须与被匹配路由的AS Path一致，才判定为匹配成功。 |
|CidrMatchMode|String|否|是|匹配前缀模式。|match语句。取值：-   Include：模糊匹配。匹配条件中的路由前缀包含被匹配路由的路由前缀即判定为匹配成功。例如：定义1.1.0.0/16的策略可以模糊匹配到1.1.1.0/24的路由。
-   Complete：精确匹配。匹配条件中的路由前缀必须与被匹配路由的路由前缀一致，才判定为匹配成功。例如：定义1.1.0.0/16的策略仅可以精确匹配到1.1.0.0/16的路由。 |
|MapResult|String|是|是|所有匹配条件通过后的策略行为。|取值：-   Permit：允许通过被匹配的路由。
-   Deny：拒绝通过被匹配的路由。 |
|RouteTypes|List|否|是|匹配路由的类型列表。|match语句。取值：-   System：系统路由，由系统自动生成的路由。
-   Custom：用户路由，由用户手动添加的自定义路由。
-   BGP：BGP路由，通告至BGP中的路由。

支持输入多种类型。|
|Preference|Integer|否|是|修改路由的优先级。|action语句。取值范围：1~100。

默认值：50。

数字越小，优先级越高。|
|CommunityOperateMode|String|否|是|操作Community的模式。|action语句。取值：-   Additive：添加。
-   Replace：替换。 |
|CenId|String|是|否|云企业网的ID。|无|
|NextPriority|Integer|否|是|关联的下一条路由策略的优先级。|取值范围：1~100。-   当未配置关联优先级时，路由策略无关联的下一条路由策略。
-   当关联优先级取值为1时，路由策略关联当前路由策略的下一条路由策略。
-   当关联优先级取值非1时，路由策略关联优先级必须大于当前路由策略的优先级。

仅当MapResult取值为Permit时，匹配通过的路由才会继续匹配关联的下一条路由策略。|
|PrependAsPath|List|否|是|地域网关接收或发布路由时追加AS Path。|action语句。路由策略应用方向不同，配置追加AS Path的要求也不同，具体如下：-   入地域网关方向配置追加AS Path时，匹配条件中必须配置源实例ID列表和源地域，且源地域必须与路由策略应用的地域一致。
-   出地域网关方向配置追加AS Path时，匹配条件中必须配置目的实例ID列表。 |
|CommunityMatchMode|String|否|是|匹配Community模式。|match语句。取值：-   Include：模糊匹配，匹配条件中的Community与被匹配路由的Community有重叠即判定为匹配成功。
-   Complete：精确匹配，匹配条件中的Community必须与被匹配路由的Community一致，才判定为匹配成功。 |
|MatchAsns|List|否|是|匹配路由的as-path列表。|match语句。as-path是公认强制属性，描述了一条BGP路由在传递过程中所经过的AS的号码。

仅支持AS SEQUENCE，不支持AS SET、AS CONFED SEQUENCE和AS CONFED SET，即只能是AS号列表，不支持集合和子列表。|
|SourceRegionIds|List|否|是|匹配路由的源地域ID列表。|match语句。最多支持32个地域ID。 |

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

`YAML`格式

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


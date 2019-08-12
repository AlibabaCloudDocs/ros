# ALIYUN::ECS::Route {#concept_51197_zh .concept}

ALIYUN::ECS::Route 类型用于新建自定义路由。

## 语法 {#section_j2t_tw2_lfb .section}

``` {#codeblock_rx5_ajy_b0b .language-json}
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

## 属性 {#section_nny_ww2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DestinationCidrBlock|String|是|否|RouteEntry 的目标网段。|无|
|RouteTableId|String|是|否|路由表 ID|无|
|NextHopId|String|否|否|路由条目的下一跳实例 ID|非 ECMP 路由。|
|RouteId|String|是|否|路由 ID|无|
|NextHopType|String|否|否|下一跳的类型| 可选值： Instance、Tunnel、HaVip、和 RouterInterface。

 默认值： Instance，即 ECS 实例。

 |
|NextHopList|List|否|否|路由条目的下一跳列表。|由 NextHopType 和 NextHopId 指定下一跳。如果指定了 NextHopList，则该路由为 ECMP 类路由。NextHopList 包含了 ECMP 方式的多个下一跳。NextHopList 支持包含有 2 至 4 个下一跳。只支持 VRouter上的路由指定 NextHopList，而且下一跳只能是从 VRouter 连往 VBR 方向的路由器接口。如果没有指定 NextHopList，则该路由为非 ECMP 类路由。|

## NextHopList 语法 {#section_xbk_fx2_lfb .section}

``` {#codeblock_kdd_grv_v8l .language-json}
"NextHopList": [
  {
    "NextHopId": String,
    "NextHopType": String
  }
]
```

## NextHopList 属性 {#section_wf6_6k9_bg3 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NextHopId|String|是|否|路由条目的下一跳实例 ID|无|
|NextHopType|String|否|否|下一跳的类型| 可选值：Instance、Tunnel、HaVip、和RouterInterface。

 默认值： RouterInterface，即路由器接口实例。

 |

## 返回值 {#section_wie_ewd_wg8 .section}

**Fn::GetAtt**

无

## 示例 {#section_eze_jb3_cow .section}

``` {#codeblock_h1a_vaw_kdt .language-json}
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


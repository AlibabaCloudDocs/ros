# ALIYUN::SLB::LoadBalancerClone {#concept_48918_zh .concept}

ALIYUN::SLB::LoadBalancerClone 类型用于克隆负载均衡实例。

## 语法 {#section_zw2_rvy_lfb .section}

``` {#codeblock_ehj_uz3_m98 .language-json}
{
  "Type": "ALIYUN::SLB::LoadBalancerClone",
  "Properties": {
    "SourceLoadBalancerId": String,
    "BackendServersPolicy": String
  }
}
```

## 属性 {#section_kj8_e7e_l49 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SourceLoadBalancerId|String|是|否|将要克隆的负载均衡实例 ID。|无|
|BackendServersPolicy|String|否|否|克隆策略，指定配置新负载均衡实例需要监听的 ECS 实例以及各 ECS 实例的权重。| 可选值：clone、empty、append和 replace。

 默认值：clone。

 -   clone：把源负载均衡实例中监听的 ECS 实例和权重配置全部克隆到新的负载均衡实例中。
-   empty：不给新的负载均衡实例添加任何 ECS 实例。
-   append：既克隆源负载均衡实例中监听的 ECS 实例和权重配置，也添加新的 ECS 实例和权重配置到新的负载均衡实例。
-   replace：只添加新的 ECS 实例列表和权重配置而不克隆源负载均衡实例所监听的 ECS 实例列表和权重配置。

 |
|BackendServers|List|否|是|指定新添加的需要监听的 ECS 实例列表。|无|
|LoadBalancerName|String|否|否|负载均衡实例名称。|取值：用户自定义字符串。长度限制为 1-80 个字符，允许包含字母、数字、连字符（-）、正斜杠（/）、点号（.）和下划线（\_）。|

## BackendServers 语法 {#section_xyd_o2m_5rw .section}

``` {#codeblock_l9k_k9i_wdr .language-json}
"BackendServers": [
  {
    "ServerId": String,
    "Weight": Integer
  }
]
```

## BackendServers 属性 {#section_3xt_cew_nfq .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerId|String|是|是|ECS 实例 ID。|ECS 实例必须是 Running 状态。|
|Weight|Integer|是|是|ECS 实例在负载均衡实例中的权重。|取值：0-100。默认值：100。|

## 返回值 {#section_vbb_zp7_yna .section}

**Fn::GetAtt**

LoadBalancerId：新负载均衡实例的 ID。

## 示例 {#section_yaa_nr9_hed .section}

``` {#codeblock_14c_z40_z74 .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "CloneLoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancerClone",
      "Properties": {
        "SourceLoadBalancerId": "150ebed5f06-cn-beijing-btc-***",
        "LoadBalancerName": "rosnew",
        "BackendServersPolicy": "replace",
        "BackendServers": [
            {
                "ServerId": "i-25zsk****",
                "Weight": 20
            }
        ]
      }
    }
  },
  "Outputs": {
    "LoadBalanceDetails": {
         "Value" : {"Fn::GetAtt": ["CloneLoadBalance", "LoadBalancerId"]}
    }
  }
}            
```


# ALIYUN::SLB::BackendServerAttachment {#concept_ivk_kwy_lfb .concept}

ALIYUN::SLB::BackendServerAttachment 类型用于添加后端服务器。

## 语法 {#section_sh5_tyy_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::SLB::BackendServerAttachment",
  "Properties": {
    "LoadBalancerId": String,
    "BackendServers": List,
    "BackendServerList": List,
    "BackendServerWeightList": List
  }
}
```

## 属性 {#section_qk4_lzy_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|LoadBalancerId|String|是|否|负载均衡实例的唯一标识 ID|无|
|BackendServerList|List|否|是|需要添加的后端服务器列表|和 BackendServerWeightList 联合使用。ECS 的实例 ID 用逗号分隔。当指定 BackendServers 时，将忽略该值。|
|BackendServerWeightList|List|否|是|按顺序指定 BackendServerList 中各 ECS 实例的权重|不指定该值，则 BackendServerList 中所有 ECS 实例权重都是 100；当 BackendServerWeightList 长度小于 BackendServerList 时， 则使用 BackendServerWeightList 中的最后一个值配置 BackendServerList 中剩余 ECS 实例的权重。|
|BackendServers|List|否|是|需要添加的后端服务器列表|必须是运行中的后端服务器才可以加入负载均衡。|

## BackendServers 语法 {#section_oyb_4zy_lfb .section}

``` {#codeblock_uoz_vdu_2d5 .language-json}
"BackendServers": [
  {
    "ServerId" : String,
    "Weight" : Integer
  }
]
```

## BackendServers 属性 {#section_q3w_zzy_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|ServerId|String|是|是|ECS 实例 ID|必须是 Running 状态的 ECS 实例。|
|Weight|Integer|是|是|ECS 实例在 SLB 实例中的权重|取值：0-100。默认值：100。|

## 返回值 {#section_esx_zzy_lfb .section}

**Fn::GetAtt**

-   BackendServers： 所有加入负载均衡中的服务器列表。
-   LoadBalancerId：负载均衡实例 ID。

## **示例** {#section_tcz_zzy_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Attachment2": {
      "Type": "ALIYUN::SLB::BackendServerAttachment",
      "Properties": {
        "LoadBalancerId": "15187200816-cn-beijing-btc-****",
        "BackendServerList": [
          "i-25o0m****",
          "i-25zsk****"
        ],
        "BackendServerWeightList": [
          "20",
          "100"
        ]
      }
    }
  }
}
```


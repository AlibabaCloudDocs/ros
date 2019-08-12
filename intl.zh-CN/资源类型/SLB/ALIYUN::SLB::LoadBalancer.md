# ALIYUN::SLB::LoadBalancer {#concept_51191_zh .concept}

ALIYUN::SLB::LoadBalancer类型用于创建LoadBalancer。

## 语法 {#section_ey2_ycz_lfb .section}

``` {#codeblock_csa_5va_4w1 .language-json}
{
  "Type": "ALIYUN::SLB::LoadBalancer",
  "Properties": {
    "DeletionProtection": Boolean,
    "VpcId": String ,
    "SlaveZoneId": String ,
    "Bandwidth": Integer,
    "AddressType": String ,
    "VSwitchId": String ,
    "LoadBalancerName": String ,
    "InternetChargeType": String ,
    "MasterZoneId": String ,
    "Tags": List,
    "AutoPay": Boolean,
    "PayType": String ,
    "PricingCycle": String ,
    "Duration": Number,
    "LoadBalancerSpec": String
  }
}
```

## 属性 {#section_n13_22z_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DeletionProtection|Boolean|否|否|删除保护。|可用值:"True","true","False","false"|
|VpcId|String|否|否|专有网络 ID。|无 。|
|SlaveZoneId|String|否|否|该创建实例的备可用区 ID。|无 。|
|Bandwidth|Integer|否|否|按固定带宽计费方式的公网类型实例的带宽峰值。| 针对按固定带宽计费方式的公网类型实例，需要将当前设定值通过 Listener 中的 Bandwidth 参数进行分配后才能生效；针对按使用流量计费方式的公网类型实例的带宽峰值，请直接通过 Listener 上 Bandwidth 参数进行设定，此时本参数会被忽略。

 取值：1-1000（单位为 Mbps）。

 默认值：1。

 专有网络实例系统会统一按流量计费设置。

 |
|AddressType|String|否|否|Address 类型。| 可选值：internet、intranet。

 默认值：internet。

 |
|VSwitchId|String|否|否|专有网络下的虚拟交换机 ID。|无 。|
|LoadBalancerName|String|否|否|负载均衡实例的名称。|取值：用户自定义字符串。长度限制为 1-80 个字节，允许包含字母、数字、连字符（-\)、正斜线（/）、点号（.）、和下划线（\_）。不指定该参数时，默认由系统分配一个实例名称。|
|InternetChargeType|String|否|否|公网类型实例付费方式。| 可选值：paybybandwidth、paybytraffic。

 默认值：paybytraffic。

 |
|MasterZoneId|String|否|否|实例的主可用区 ID。|无 。|
|Tags|List|否|否|负载均衡实例绑定的Tag列表，其结构是一个Json List，包含TagKey和TagValue。|最多5个。|
|LoadBalancerSpec|String|否|否|负载均衡实例的规格。| 取值：

 -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large

 每个地域支持的规格不同。关于每种规格的说明，参见[性能保障型实例](https://www.alibabacloud.com/help/doc-detail/85939.htm)。

 |
|AutoPay|Boolean|否|否|是否是自动支付预付费公网实例的账单。|取值：true|false（默认） **说明：** 仅适用于中国站。

 |
|PayType|String|否|否|实例的计费类型。|取值： -   PayOnDemand：按量付费
-   PrePay：预付费

 |
|PricingCycle|String|否|否|预付费公网实例的计费周期。|取值：month|year **说明：** 仅适用于中国站。

 |
|Duration|Number|否|否|预付费公网实例的购买时长。|取值： -   如果PricingCycle为month，取值为1~9。
-   如果PricingCycle为year，取值为1~3。

 **说明：** 仅适用于中国站。

 |

## Tags 语法 {#section_v5m_kk5_cgb .section}

``` {#codeblock_kc0_5rn_9jr .language-json}
"Tags": [
  {
    "Value": String ,
    "Key": String 
  }
]
```

## Tags 属性 {#section_h3q_kk5_cgb .section}

|名称|类型|是否必需|允许更新|描述|约束|
|--|--|----|----|--|--|
|Key|String|是|否|无|无|
|Value|String|否|否|无|无|

## 返回值 {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   LoadBalancerId：负载均衡实例的唯一标识。
-   NetworkType：负载均衡实例的网络类型，即vpc或classic。
-   AddressType：Address类型， 即intranet或internet。
-   IpAddress：负载均衡实例的IP。
-   OrderId：订单ID。

## 示例 {#section_lcd_s2z_lfb .section}

``` {#codeblock_h0c_eea_ia9 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CreateLoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "createdByHeat",
        "AddressType": "internet",
        "InternetChargeType": "paybybandwidth",
      }
    }
  },
  "Outputs": {
    "LoadBalanceDetails": {
      "Value": {
        "Fn::GetAtt": ["CreateLoadBalance", "LoadBalancerId"]}
    }
  }
}
```


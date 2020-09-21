# ALIYUN::SLB::LoadBalancer

ALIYUN::SLB::LoadBalancer类型用于创建LoadBalancer。

## 语法

```
{
  "Type": "ALIYUN::SLB::LoadBalancer",
  "Properties": {
    "DeletionProtection": Boolean,
    "AddressType": String,
    "Tags": List,
    "InternetChargeType": String,
    "Bandwidth": Integer,
    "SlaveZoneId": String,
    "ResourceGroupId": String,
    "AutoPay": Boolean,
    "VpcId": String,
    "PricingCycle": String,
    "LoadBalancerName": String,
    "Duration": Number,
    "VSwitchId": String,
    "LoadBalancerSpec": String,
    "MasterZoneId": String,
    "PayType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无|
|DeletionProtection|Boolean|否|否|删除保护。|取值： -   true
-   false |
|VpcId|String|否|否|专有网络ID。|无|
|SlaveZoneId|String|否|否|该创建实例的可用区ID。|无|
|Bandwidth|Integer|否|否|按固定带宽计费方式的公网类型实例的带宽峰值。|-   针对按固定带宽计费方式的公网类型实例，需要将当前设定值通过Listener中的Bandwidth参数进行分配后才能生效。
-   针对按使用流量计费方式的公网类型实例的带宽峰值，请直接通过Listener上Bandwidth参数进行设定，此时本参数会被忽略。

 取值范围：1~1000。

 单位：Mbps。

 默认值：1。

 专有网络实例系统会统一按流量计费设置。 |
|AddressType|String|否|否|Address类型。|取值：

-   internet（默认值）
-   intranet |
|VSwitchId|String|否|否|专有网络下的虚拟交换机ID。|无|
|LoadBalancerName|String|否|否|负载均衡实例的名称。|长度为1~80个字符。可包含英文字母、数字、短划线（-）、正斜线（/）、英文句点（.）和下划线（\_）。 不指定该参数时，默认由系统分配一个实例名称。 |
|InternetChargeType|String|否|否|公网类型实例付费方式。|取值：

-   paybybandwidth
-   paybytraffic（默认值） |
|MasterZoneId|String|否|否|实例的主可用区ID。|无|
|Tags|List|否|是|负载均衡实例的标签。|最多支持5个标签。 详情请参见[Tags属性](/intl.zh-CN/资源类型/SLB/ALIYUN::SLB::LoadBalancerClone.md)。 |
|LoadBalancerSpec|String|否|否|负载均衡实例的规格。|取值： -   slb.s1.small
-   slb.s2.small
-   slb.s2.medium
-   slb.s3.small
-   slb.s3.medium
-   slb.s3.large

 每个地域支持的规格不同。关于每种规格的说明，参见[性能保障型实例](https://www.alibabacloud.com/help/doc-detail/85939.htm)。 |
|PayType|String|否|否|实例的计费类型。|取值： -   PayOnDemand：按量付费。
-   PrePay：预付费。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String 
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~64个字符，不能以`aliyun`和acs:开头，不能包含`http://`或`https://`。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和acs:开头，不能包含`http://`或`https://`。|

## 返回值

Fn::GetAtt

-   LoadBalancerId：负载均衡实例的唯一标识。
-   NetworkType：负载均衡实例的网络类型，vpc或classic。
-   AddressType：Address类型，intranet或internet。
-   IpAddress：负载均衡实例的IP。
-   OrderId：订单ID。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CreateLoadBalance": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "createdBy****",
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


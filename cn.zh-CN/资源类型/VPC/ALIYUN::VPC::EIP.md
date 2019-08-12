# ALIYUN::VPC::EIP {#concept_cxc_v5n_jgb .concept}

ALIYUN::VPC::EIP类型用于申请弹性公网IP。

## 语法 {#section_hr1_kzd_lfb .section}

``` {#codeblock_zaw_0oi_rtm .language-json}
{
  "Type": "ALIYUN::VPC::EIP",
  "Properties": {
    "Isp": String,
    "Period": Number,
    "ResourceGroupId": String,
    "AutoPay": Boolean,
    "InstanceChargeType": String,
    "PricingCycle": String,
    "InternetChargeType": String,
    "Bandwidth": Number
  }
}
```

## 属性 {#section_vq2_3vn_jgb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无。|
|Bandwidth|Number|否|否|带宽值。|如果不指定，则取默认值 5 Mbps。|
|InternetChargeType|String|否|否|EIP的计费方式。| 取值：

 -   PayByBandwidth（默认值）：按带宽计费。
-   PayByTraffic：按流量计费。

 |
|InstanceChargeType|String|否|否|EIP的付费方式。| 取值：

 -   Prepaid：预付费。
-   Postpaid（默认值）：后付费。

 |
|PricingCycle|String|否|否|预付费的计费周期。| 取值：

 -   Month（默认值）：按月付费。
-   Year：按年付费。

 **说明：** InstanceChargeType参数的值为 Prepaid时，该参数必选。

 |
|Period|Number|否|否|购买时长。| 取值：

 -   当选择按月付费时，取值范围为 \[1, 9\]。
-   当选择按年付费时，取值范围为 \[1, 3\]。

 默认值为 1。

 **说明：** InstanceChargeType参数的值为Prepaid时，该参数必选。

 |
|AutoPay|Boolean|否|否|是否自动付费。| 取值：

 -   false：不开启自动付费，生成订单后需要到[订单中心](https://expense.console.aliyun.com/?#/order/list/)完成支付。
-   true：开启自动付费，自动支付订单。

 **说明：** InstanceChargeType参数的值为Prepaid时，该参数必选。

 |
|Isp|String|否|否|用于金融云的ISP标签，仅对cn-hangzhou 地域有效。| 如果您不是金融云用户，该参数会被忽略。

 |

## 返回值 {#section_ejn_dwn_jgb .section}

 **Fn::GetAtt** 

-   EipAddress：分配的弹性公网IP。
-   AllocationId：弹性公网IP的实例ID。
-   OrderId：选择预付费时返回的订单号。

## 示例 {#section_plh_gwn_jgb .section}

``` {#codeblock_shg_jc8_s7j .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Eip": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "InternetChargeType": "PayByTraffic",
          "Bandwidth": 200
      }
    }
  },
  "Outputs": {
    "EipAddress": {
      "Value" : {"Fn::GetAtt": ["Eip", "EipAddress"]}
    },
    "AllocationId": {
      "Value" : {"Fn::GetAtt": ["Eip", "AllocationId"]}
    },
    "OrderId": {
      "Value" : {"Fn::GetAtt": ["Eip", "OrderId"]}
    }
  }
}
```


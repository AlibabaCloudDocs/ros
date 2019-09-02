# ALIYUN::MarketPlace::Image {#concept_48964_zh .concept}

ALIYUN::MarketPlace::Image 类型用于购买云市场镜像。

## 语法 {#section_ugr_ck1_mfb .section}

``` {#codeblock_26o_jlf_5aw .language-json}
{
  "Type": "ALIYUN::MarketPlace::Image",
  "Properties": {
    "Duration": Number,
    "Quantity": Number,
    "PricingCycle": String,
    "ChargeType": String,
    "ImageId": String
  }
}
```

## 属性 {#section_hfb_ukq_8f2 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ImageId|String|是|否|云市场镜像 ID。|无|
|PricingCycle|String|否|否|付费周期单位。|如果 ChargeType 指定为 Postpaid（按量付费），这个参数将被忽略；如果 ChargeType 是 Prepaid（包年包月），则可选值：Month 和 Year。|
|ChargeType|String|否|否|付费类型。| 可选值：Prepaid 和 Postpaid。

 默认值是 Prepaid。

 |
|Duration|Number|否|否|付费时长。| 可选值：1、 2、3、6、12、24。

 默认值：1。

 该属性和 PricingCycle 联合使用。云市场资源支持如下付费周期：一个月，一个季度，半年，一年，两年。如果不指定 PricingCycle，则表示只购买该资源一次。

 |
|Quantity|Number|否|否|购买该资源的数量。|默认值：1。|

## 返回值 {#section_98p_ted_0mu .section}

**Fn::GetAtt**

OrderId：购买云市场镜像订单 ID。

## 示例 {#section_8e4_5e2_wdk .section}

``` {#codeblock_ayl_b8q_g7g .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ImageOrder": {
      "Type": "ALIYUN::MarketPlace::Image",
      "Properties": {
        "ImageId":"m-25xov****",
        "Duration":"1",
        "PricingCycle": "Month",
        "Quantity": 2,
        "ChargeType": "Prepaid"
      }
    }
  }
}            
```


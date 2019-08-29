# ALIYUN::MarketPlace::Order {#concept_48483_zh .concept}

ALIYUN::MarketPlace::Order 类型用于购买云市场的资源。

## 语法 {#section_nhl_zl1_mfb .section}

```language-json
{
  "Type": "ALIYUN::MarketPlace::Order",
  "Properties": {
    "ProductCode": String,
    "SkuCode": String,
    "PricingCycle": String,
    "Preference": Map,
    "ChargeType": String,
    "Duration": Number,
    "Quantity": Number
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProductCode|String|是|否|云市场资源的 Product Code。|无|
|SkuCode|String|是|否|云市场资源的 sku code。|无|
|PricingCycle|String|否|否|付费周期单位。|如果 ChargeType 指定为 Postpaid，此参数将被忽略；如果 ChargeType 为 Prepaid，则允许选值：Month 或 Year。|
|Preference|Map|否|否|用户自定义参数。|无|
|ChargeType|String|否|否|付费类型。|可选值：Prepaid 和 Postpaid。 默认值： Prepaid。|
|Duration|Number|否|否|付费时长。| 可选值： 1、2、3、6、12、和 24，单位：月。

 默认值： 1。

 该属性和 PricingCycle 联合使用。云市场资源支持如下付费周期：一个月，一个季度，半年，一年，两年。如果不指定 PricingCycle，则表示只购买该资源一次。

 |
|Quantity|Number|否|否|购买该资源的数量。|默认值： 1 。|

## 返回值 { .section}

**Fn::GetAtt**

OrderId：购买云市场资源的订单 ID。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MarketOrder": {
      "Type": "ALIYUN::MarketPlace::Order",
      "Properties": {
        "ProductCode":"cmapi011900",
        "SkuCode":"postpay",
        "Duration":"1",
        "PricingCycle": "Year",
        "Quantity": 1,
        "ChargeType": "Prepaid",
        "Preference": {"my_email": "1111@aliyun.com"}
      }
    }
  },
  "Outputs" : {
    "OderId": {
      "Value": {
        "Fn::GetAtt": [
          "MarketOrder",
          "OrderId"
        ]
      }
    }
  }
}			
```


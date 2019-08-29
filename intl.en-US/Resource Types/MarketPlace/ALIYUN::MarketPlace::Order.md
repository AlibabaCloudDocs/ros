# ALIYUN::MarketPlace::Order {#concept_48483_zh .concept}

ALIYUN::MarketPlace::Order is used to purchase resources from Alibaba Cloud Marketplace.

## Syntax {#section_nhl_zl1_mfb .section}

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

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ProductCode|String|Yes|No|The code of a Alibaba Cloud Marketplace product.|None|
|SkuCode|String|Yes|No|The SKU code of the product.|None|
|PricingCycle|String|No|No|The billing cycle of the product.|This parameter is ignored if the ChargeType parameter is set to Postpaid. This parameter can be set to Month or Year if the ChargeType parameter is set to Prepaid.|
|Preference|Map|No|No|The user-defined parameters of the product.|None|
|ChargeType|String|No|No|The billing method of the product.|Valid values: Prepaid and Postpaid. Default value: Prepaid.|
|Duration|Number|No|No|The subscription period of the product.| Valid values: 1, 2, 3, 6, 12, and 24. Unit: month.

 Default value: 1.

 This parameter is used in combination with the PricingCycle parameter. The billing cycle for Alibaba Cloud Marketplace resources can be one month, one quarter, half a year, one year, or two years. If the PricingCycle parameter is not set, the resource is bought only once.

 |
|Quantity|Number|No|No|The number of products to be purchased.|Default value: 1.|

## Response parameters { .section}

**Fn::GetAtt**

OrderId: the order ID of the purchased Alibaba Cloud Marketplace product.

## Examples { .section}

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


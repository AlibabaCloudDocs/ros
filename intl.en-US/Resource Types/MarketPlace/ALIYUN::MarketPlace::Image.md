# ALIYUN::MarketPlace::Image {#concept_48964_zh .concept}

ALIYUN::MarketPlace::Image is used to purchase images from Alibaba Cloud Marketplace.

## Syntax {#section_ugr_ck1_mfb .section}

```language-json
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

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ImageId|String|Yes|No|The ID of an image in Alibaba Cloud Marketplace.|None|
|PricingCycle|String|No|No|The billing cycle of the image.|This parameter is ignored if the ChargeType parameter is set to Postpaid. This parameter can be set to Month or Year if the ChargeType parameter is set to Prepaid.|
|ChargeType|String|No|No|The billing method of the image.| Valid values: Prepaid and Postpaid.

 Default value: Prepaid.

 |
|Duration|Number|No|No|The subscription period of the image.| Valid values: 1, 2, 3, 6, 12, and 24.

 Default value: 1.

 This parameter is used in combination with the PricingCycle parameter. The billing cycle for Alibaba Cloud Marketplace resources can be one month, one quarter, half a year, one year, or two years. If the PricingCycle parameter is not set, the image is bought only once.

 |
|Quantity|Number|No|No|The number of images to be purchased.|Default value: 1.|

## Response parameters { .section}

**Fn::GetAtt**

OrderId: the order ID of the purchased Alibaba Cloud Marketplace image.

## Examples { .section}

```language-json
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


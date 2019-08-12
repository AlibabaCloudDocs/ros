# ALIYUN::MarketPlace::ImageSubscription {#concept_48965_zh .concept}

ALIYUN::MarketPlace::ImageSubscription is used to subscribe to images available in Alibaba Cloud Marketplace.

## Syntax {#section_uwp_rk1_mfb .section}

```language-json
{
  "Type": "ALIYUN::MarketPlace::ImageSubscription",
  "Properties": {
    "ImageId": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ImageId|String|Yes|No|The ID of an image in Alibaba Cloud Marketplace.|Before you can use an image from Alibaba Cloud Marketplace to create a Pay-As-You-Go ECS instance, you must subscribe to the image.|

## Response parameters { .section}

**Fn::GetAtt**

ImageId: the ID of the image in Alibaba Cloud Marketplace.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ImageSubscription": {
      "Type": "ALIYUN::MarketPlace::ImageSubscription",
      "Properties": {
        "ImageId":"m-25xov****"
      }
    }
  }
}            
```


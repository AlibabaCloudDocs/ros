# ALIYUN::MarketPlace::ImageSubscription {#concept_48965_zh .concept}

ALIYUN::MarketPlace::ImageSubscription 类型用于订阅云市场镜像。

## 语法 {#section_uwp_rk1_mfb .section}

```language-json
{
  "Type": "ALIYUN::MarketPlace::ImageSubscription",
  "Properties": {
    "ImageId": String
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ImageId|String|是|否|云市场镜像 ID。|使用云市场镜像创建按量付费的 ECS 实例时，需先订阅云市场镜像。|

## 返回值 { .section}

**Fn::GetAtt**

ImageId：云市场镜像 ID。

## 示例 { .section}

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


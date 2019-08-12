# ALIYUN::CEN::CenBandwidthPackage {#concept_dmj_hvy_3hb .concept}

ALIYUN::CEN::CenBandwidthPackage类型用于在使用云企业网连接不同地域的网络实例前，您需要根据网络实例所属的区域购买带宽包。

## 语法 {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenBandwidthPackage",
  "Properties": {
    "GeographicRegionAId": String,
    "Description": String,
    "AutoPay": Boolean,
    "Period": Integer,
    "GeographicRegionBId": String,
    "Bandwidth": Integer,
    "PricingCycle": String,
    "BandwidthPackageChargeType": String,
    "Name": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GeographicRegionAId|String|是|否|网络实例所属的区域。|取值：China | North-America | Asia-Pacific | Europe | Australia|
|Description|String|否|是|带宽包的描述。可以包含\[2,256\]个字符、数字、下划线和连字符，必须以英文字母开头，但不能以http://或https://开头。|无。|
|AutoPay|Boolean|否|否|是否自动支付账单。| 取值：

 -   true
-   false （默认值）

 |
|Period|Integer|否|否|带宽包的购买时长，默认值为1。|无。|
|GeographicRegionBId|String|是|否|网络实例所属的区域。|取值：China | North-America | Asia-Pacific | Europe | Australiat|
|Bandwidth|Integer|是|是|带宽包的带宽峰值，单位为Mbps，最小值为2。|无。|
|PricingCycle|String|否|否|带宽包的计费周期。取值：Month | Year，默认值为Month。|无。|
|BandwidthPackageChargeType|String|否|否|带宽包的付费类型。| 取值：

 -   POSTPAY
-   PREPAY

 |
|Name|String|否|是| 带宽包的名称。

 长度为 2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以`http://`或`https://`开头。

 |无。|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

CenBandwidthPackageId：新建带宽包的ID。

## 示例 {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenBandwidthPackage": {
      "Type": "ALIYUN::CEN::CenBandwidthPackage",
      "Properties": {
        "GeographicRegionAId": {
          "Ref": "GeographicRegionAId"
        },
        "Description": {
          "Ref": "Description"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "Period": {
          "Ref": "Period"
        },
        "GeographicRegionBId": {
          "Ref": "GeographicRegionBId"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "BandwidthPackageChargeType": {
          "Ref": "BandwidthPackageChargeType"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "GeographicRegionAId": {
      "Type": "String",
      "Description": "The other area A to connect.\nValid value: China | North-America | Asia-Pacific | Europe | Australia",
      "AllowedValues": [
        "China",
        "North-America",
        "Asia-Pacific",
        "Europe",
        "Australia"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the bandwidth package.\nThe description can contain [2,256] characters, numbers, underscores, and hyphens, and the name must start with English letters, but cannot start with http:// or https://."
    },
    "AutoPay": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to automatically pay the bill. Valid value:\ntrue\nfalse (Default)",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Period": {
      "Default": 1,
      "Type": "Number",
      "Description": "The purchase period. The default value is 1."
    },
    "GeographicRegionBId": {
      "Type": "String",
      "Description": "The other area B to connect.\nValid value: China | North-America | Asia-Pacific | Europe | Australia",
      "AllowedValues": [
        "China",
        "North-America",
        "Asia-Pacific",
        "Europe",
        "Australia"
      ]
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The bandwidth in Mbps of the bandwidth package. The bandwidth cannot be less than 2 Mbps.",
      "MinValue": 2
    },
    "PricingCycle": {
      "Type": "String",
      "Description": "The pricing cycle.",
      "AllowedValues": [
            "Month",
            "Year"
          ]
    },
    "BandwidthPackageChargeType": {
      "Type": "String",
      "Description": "The billing method. Valid value: PREPAY, POSTPAY (Default)",
      "AllowedValues": [
        "PREPAY",
        "POSTPAY"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the bandwidth package.\nThe name can contain 2-128 characters including a-z, A-Z, 0-9, periods, underlines, and hyphens. It must start with English letters, but cannot start with http:// or https://."
    }
  },
  "Outputs": {
    "CenBandwidthPackageId": {
      "Description": "The ID of the bandwidth package.",
      "Value": {
        "Fn::GetAtt": [
          "CenBandwidthPackage",
          "CenBandwidthPackageId"
        ]
      }
    }
  }
}
```


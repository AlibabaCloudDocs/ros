# ALIYUN::CEN::CenBandwidthPackage {#concept_dmj_hvy_3hb .concept}

ALIYUN::CEN::CenBandwidthPackage is used to purchase a bandwidth package before you use CEN to connect network instances in different regions.

## Syntax {#section_xyg_tn2_lfb .section}

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

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|GeographicRegionAId|String|Yes|No|The geographic region where a network instance resides.|Valid values: China, North-America, Asia-Pacific, Europe, and Australia.|
|Description|String|No|Yes|The description of the bandwidth package. The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.|None|
|AutoPay|Boolean|No|No|Indicates whether to enable automatic payment. Default value: false.| Valid values:

 -   true
-   false

 |
|Period|Integer|No|No|The subscription period of the bandwidth package. Default value: 1.|None|
|GeographicRegionBId|String|Yes|No|The geographic region where the other network instance resides.|Valid values: China, North-America, Asia-Pacific, Europe, and Australia.|
|Bandwidth|Integer|Yes|Yes|The peak bandwidth of the bandwidth package. Unit: Mbit/s. Minimum value: 2.|None|
|PricingCycle|String|No|No|The pricing cycle of the bandwidth package. Valid values: Month and Year. Default value: Month.|None|
|BandwidthPackageChargeType|String|No|No|The billing method of the bandwidth package.| Valid values:

 -   POSTPAY
-   PREPAY

 |
|Name|String|No|Yes| The name of the bandwidth package.

 The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with `http://` or `https://`.

 |None|

## Response parameters {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

CenBandwidthPackageId: the ID of the created bandwidth package.

## Examples {#section_klp_54n_4fb .section}

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
      "Description": "The description of the bandwidth package. \n The description must be 2 to 256 characters in length and can contain letters, digits, underscores (_), and hyphens (-). It must start with a letter but cannot start with http:// or https://. "
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
      "Description": "The name of the bandwidth package.\n The name must be 2 to 128 characters in length, including a-z, A-Z, 0-9, periods (.), underscores (_), and hyphens (-). It must start with a letter but cannot start with http:// or https://."
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


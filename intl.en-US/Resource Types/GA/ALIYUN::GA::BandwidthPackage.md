# ALIYUN::GA::BandwidthPackage

ALIYUN::GA::BandwidthPackage is used to create a bandwidth plan.

## Syntax

```
{
  "Type": "ALIYUN::GA::BandwidthPackage",
  "Properties": {
    "BandwidthType": String,
    "CbnGeographicRegionIdB": String,
    "Type": String,
    "CbnGeographicRegionIdA": String,
    "AutoUseCoupon": String,
    "PricingCycle": String,
    "ChargeType": String,
    "Bandwidth": Integer,
    "Ratio": String,
    "Duration": String,
    "AutoPay": String,
    "BillingType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|BandwidthType|String|No|Yes|The bandwidth type.|Valid values:-   Basic: basic acceleration bandwidth
-   Enhanced: enhanced acceleration bandwidth
-   Advanced: premium acceleration bandwidth |
|CbnGeographicRegionIdB|String|No|No|Area B defined in the cross-border bandwidth plan.|None|
|Type|String|Yes|No|The type of the bandwidth plan.|Valid values:-   Basic: basic bandwidth plan
-   CrossDomain: cross-border bandwidth plan |
|CbnGeographicRegionIdA|String|No|No|Area A defined in the cross-border bandwidth plan.|None|
|AutoUseCoupon|String|No|Yes|Specifies whether to use coupons.|Valid values:-   True
-   False |
|PricingCycle|String|No|No|The unit of the subscription period.|Valid values:-   Month
-   Year |
|ChargeType|String|No|No|The billing method of the bandwidth plan.|Set the value to PREPAY. |
|Bandwidth|Integer|Yes|Yes|The bandwidth provided by the bandwidth plan.|Valid values: 2 to 2000Unit: MB |
|Ratio|String|No|No|The minimum bandwidth guaranteed in percentile.|None|
|Duration|String|No|No|The subscription period.|-   Valid values when the PricingCycle parameter is set to Month: 1 to 9
-   Valid values when the PricingCycle parameter is set to Year: 1 to 3 |
|AutoPay|String|No|Yes|Specifies whether to enable automatic payment.|Valid values:-   True
-   False |
|BillingType|String|No|No|The billing method for network usage.|None|

## Response parameters

Fn::GetAtt

-   BandwidthPackageName: the name of the bandwidth plan.
-   CbnGeographicRegionIdA: Area A defined in the cross-border bandwidth plan.
-   CbnGeographicRegionIdB: Area B defined in the cross-border bandwidth plan.
-   AutoPay: indicates whether automatic payment is enabled.
-   BandwidthType: the bandwidth type.
-   Type: the type of the bandwidth plan.
-   AutoUseCoupon: indicates whether coupons are used.
-   ChargeType: the billing method of the bandwidth plan.
-   Bandwidth: the bandwidth provided by the bandwidth plan.
-   BandwidthPackageId: the ID of the bandwidth plan.
-   Ratio: the minimum bandwidth guaranteed in percentile.
-   BillingType: the billing method for network usage.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "BandwidthType": {
      "Type": "String",
      "Description": "the bandwidth BandwidthType of the bandwidth"
    },
    "CbnGeographicRegionIdB": {
      "Type": "String",
      "Description": "The CbnGeographicRegionIdB of the bandwidth"
    },
    "Type": {
      "Type": "String",
      "Description": "The type of the bandwidth plan"
    },
    "CbnGeographicRegionIdA": {
      "Type": "String",
      "Description": "The CbnGeographicRegionIdA  of the bandwidth"
    },
    "AutoUseCoupon": {
      "Type": "String",
      "Description": "The AutoUseCoupon  of the bandwidth"
    },
    "PricingCycle": {
      "Type": "String",
      "Description": ""
    },
    "ChargeType": {
      "Type": "String",
      "Description": "The ChargeType of the bandwidth"
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The bandwidth provided by the bandwidth plan."
    },
    "Ratio": {
      "Type": "String",
      "Description": "The Ratio of the bandwidth"
    },
    "Duration": {
      "Type": "String",
      "Description": ""
    },
    "AutoPay": {
      "Type": "String",
      "Description": "The AutoPay of the bandwidth"
    },
    "BillingType": {
      "Type": "String",
      "Description": "The BillingType of the bandwidth"
    }
  },
  "Resources": {
    "GaBandwidthPackage": {
      "Type": "ALIYUN::GA::BandwidthPackage",
      "Properties": {
        "BandwidthType": {
          "Ref": "BandwidthType"
        },
        "CbnGeographicRegionIdB": {
          "Ref": "CbnGeographicRegionIdB"
        },
        "Type": {
          "Ref": "Type"
        },
        "CbnGeographicRegionIdA": {
          "Ref": "CbnGeographicRegionIdA"
        },
        "AutoUseCoupon": {
          "Ref": "AutoUseCoupon"
        },
        "PricingCycle": {
          "Ref": "PricingCycle"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "Ratio": {
          "Ref": "Ratio"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "AutoPay": {
          "Ref": "AutoPay"
        },
        "BillingType": {
          "Ref": "BillingType"
        }
      }
    }
  },
  "Outputs": {
    "BandwidthPackageName": {
      "Description": "The Resource name of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "BandwidthPackageName"
        ]
      }
    },
    "CbnGeographicRegionIdB": {
      "Description": "The CbnGeographicRegionIdB of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "CbnGeographicRegionIdB"
        ]
      }
    },
    "CbnGeographicRegionIdA": {
      "Description": "The CbnGeographicRegionIdA  of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "CbnGeographicRegionIdA"
        ]
      }
    },
    "AutoPay": {
      "Description": "The AutoPay of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "AutoPay"
        ]
      }
    },
    "BandwidthType": {
      "Description": "the bandwidth BandwidthType of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "BandwidthType"
        ]
      }
    },
    "Type": {
      "Description": "The type of the bandwidth plan",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "Type"
        ]
      }
    },
    "AutoUseCoupon": {
      "Description": "The AutoUseCoupon  of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "AutoUseCoupon"
        ]
      }
    },
    "ChargeType": {
      "Description": "The ChargeType of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "ChargeType"
        ]
      }
    },
    "Bandwidth": {
      "Description": "The bandwidth provided by the bandwidth plan.",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "Bandwidth"
        ]
      }
    },
    "PaymentType": {
      "Description": "The Payment Type of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "PaymentType"
        ]
      }
    },
    "BandwidthPackageId": {
      "Description": "The Resource ID of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "BandwidthPackageId"
        ]
      }
    },
    "Ratio": {
      "Description": "The Ratio of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "Ratio"
        ]
      }
    },
    "BillingType": {
      "Description": "The BillingType of the bandwidth",
      "Value": {
        "Fn::GetAtt": [
          "GaBandwidthPackage",
          "BillingType"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  BandwidthType:
    Type: String
    Description: the bandwidth BandwidthType of the bandwidth
  CbnGeographicRegionIdB:
    Type: String
    Description: The CbnGeographicRegionIdB of the bandwidth
  Type:
    Type: String
    Description: The type of the bandwidth plan
  CbnGeographicRegionIdA:
    Type: String
    Description: The CbnGeographicRegionIdA  of the bandwidth
  AutoUseCoupon:
    Type: String
    Description: The AutoUseCoupon  of the bandwidth
  PricingCycle:
    Type: String
    Description: ''
  ChargeType:
    Type: String
    Description: The ChargeType of the bandwidth
  Bandwidth:
    Type: Number
    Description: The bandwidth provided by the bandwidth plan.
  Ratio:
    Type: String
    Description: The Ratio of the bandwidth
  Duration:
    Type: String
    Description: ''
  AutoPay:
    Type: String
    Description: The AutoPay of the bandwidth
  BillingType:
    Type: String
    Description: The BillingType of the bandwidth
Resources:
  GaBandwidthPackage:
    Type: 'ALIYUN::GA::BandwidthPackage'
    Properties:
      BandwidthType:
        Ref: BandwidthType
      CbnGeographicRegionIdB:
        Ref: CbnGeographicRegionIdB
      Type:
        Ref: Type
      CbnGeographicRegionIdA:
        Ref: CbnGeographicRegionIdA
      AutoUseCoupon:
        Ref: AutoUseCoupon
      PricingCycle:
        Ref: PricingCycle
      ChargeType:
        Ref: ChargeType
      Bandwidth:
        Ref: Bandwidth
      Ratio:
        Ref: Ratio
      Duration:
        Ref: Duration
      AutoPay:
        Ref: AutoPay
      BillingType:
        Ref: BillingType
Outputs:
  BandwidthPackageName:
    Description: The Resource name of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - BandwidthPackageName
  CbnGeographicRegionIdB:
    Description: The CbnGeographicRegionIdB of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - CbnGeographicRegionIdB
  CbnGeographicRegionIdA:
    Description: The CbnGeographicRegionIdA  of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - CbnGeographicRegionIdA
  AutoPay:
    Description: The AutoPay of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - AutoPay
  BandwidthType:
    Description: the bandwidth BandwidthType of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - BandwidthType
  Type:
    Description: The type of the bandwidth plan
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - Type
  AutoUseCoupon:
    Description: The AutoUseCoupon  of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - AutoUseCoupon
  ChargeType:
    Description: The ChargeType of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - ChargeType
  Bandwidth:
    Description: The bandwidth provided by the bandwidth plan.
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - Bandwidth
  PaymentType:
    Description: The Payment Type of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - PaymentType
  BandwidthPackageId:
    Description: The Resource ID of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - BandwidthPackageId
  Ratio:
    Description: The Ratio of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - Ratio
  BillingType:
    Description: The BillingType of the bandwidth
    Value:
      'Fn::GetAtt':
        - GaBandwidthPackage
        - BillingType
```


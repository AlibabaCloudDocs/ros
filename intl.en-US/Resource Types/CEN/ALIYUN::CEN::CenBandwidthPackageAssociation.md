# ALIYUN::CEN::CenBandwidthPackageAssociation {#concept_ecb_ygz_3hb .concept}

ALIYUN::CEN::CenBandwidthPackageAssociation is used to bind a bandwidth package to the specified Cloud Enterprise Network \(CEN\) instance.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenBandwidthPackageAssociation",
  "Properties": {
    "CenId": String,
    "CenBandwidthPackageId": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CenId|String|Yes|No|The ID of the CEN instance.|None|
|CenBandwidthPackageId|String|Yes|No|The ID of the bandwidth package.|None|

## Response parameters {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

None

## Examples {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenBandwidthPackageAssociation": {
      "Type": "ALIYUN::CEN::CenBandwidthPackageAssociation",
      "Properties": {
        "CenId": {
          "Ref": "CenId"
        },
        "CenBandwidthPackageId": {
          "Ref": "CenBandwidthPackageId"
        }
      }
    }
  },
  "Parameters": {
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "CenBandwidthPackageId": {
      "Type": "String",
      "Description": "The ID of the bandwidth package."
    }
  },
  "Outputs": {}
}
```


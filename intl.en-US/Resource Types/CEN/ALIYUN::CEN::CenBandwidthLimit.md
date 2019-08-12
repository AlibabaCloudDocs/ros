# ALIYUN::CEN::CenBandwidthLimit {#concept_185695 .concept}

ALIYUN::CEN::CenBandwidthLimit is used to configure the cross-region interconnection bandwidth between two specified regions after you attach a bandwidth package to the specified CEN instance.

**Note:** After a resource is deleted, the bandwidth will not be restored to its original value before the resource was created.

## Syntax {#section_dhx_v86_qbn .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenBandwidthLimit",
  "Properties": {
    "OppositeRegionId": String,
    "CenId": String,
    "BandwidthLimit": Integer,
    "LocalRegionId": String
  }
}
```

## Properties {#section_n9c_cpv_tzh .section}

|Name|Type|Required|Editable|Description |Validity|
|----|----|--------|--------|------------|--------|
|OppositeRegionId|String |Yes|No|The ID of the peer region.|None|
|CenId|String|Yes|No|The ID of the CEN instance.|None|
|BandwidthLimit|Integer|Yes|No|The bandwidth limit configured for the communication between interconnected regions.|Minimum value: 1.|
|LocalRegionId|String|Yes|No|The ID of the local region.|None|

## Response parameters {#section_tgw_aej_j8f .section}

**Fn::GetAtt**

None

## Examples {#section_r4y_edv_raz .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenBandwidthLimit": {
      "Type": "ALIYUN::CEN::CenBandwidthLimit",
      "Properties": {
        "OppositeRegionId": {
          "Ref": "OppositeRegionId"
        },
        "CenId": {
          "Ref": "CenId"
        },
        "BandwidthLimit": {
          "Ref": "BandwidthLimit"
        },
        "LocalRegionId": {
          "Ref": "LocalRegionId"
        }
      }
    }
  },
  "Parameters": {
    "OppositeRegionId": {
      "Type": "String",
      "Description": "The ID of the other interconnected region."
    },
    "CenId": {
      "Type": "String",
      "Description": "The ID of the CEN instance."
    },
    "BandwidthLimit": {
      "Type": "Number",
      "Description": "The bandwidth configured for the interconnected regions communication. Minimal value: 1",
      "MinValue": 1
    },
    "LocalRegionId": {
      "Type": "String",
      "Description": "The ID of the local region."
    }
  },
  "Outputs": {}
}
```


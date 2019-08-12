# ALIYUN::ESS::AlarmTaskEnable {#concept_bw3_xyz_qgb .concept}

ALIYUN::ESS::AlarmTaskEnable is used to enable an alarm task. You can use this API to enable alarm tasks that are disabled.

## Syntax {#section_xxx_ff1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::AlarmTaskEnable",
  "Properties": {
    "AlarmTaskId": String,
    "Enable": Boolean
  }
}
```

## Properties {#section_gmr_gf1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AlarmTaskId|String|Yes|No|The ID of the alarm task.|None|
|Enable|Boolean|Yes|Yes|Indicates whether to enable the alarm task.|None|

## Response parameters {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

None

## Examples {#section_mmh_mf1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Enable": {
      "Type": "Boolean",
      "Description": "Enable an alarm task or not",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "AlarmTaskId": {
      "Type": "String",
      "Description": "The ID of the alarm task."
    }
  },
  "Resources": {
    "AlarmTaskEnable": {
      "Type": "ALIYUN::ESS::AlarmTaskEnable",
      "Properties": {
        "Enable": {
          "Ref": "Enable"
        },
        "AlarmTaskId": {
          "Ref": "AlarmTaskId"
        }
      }
    }
  },
  "Outputs": {}
}
```


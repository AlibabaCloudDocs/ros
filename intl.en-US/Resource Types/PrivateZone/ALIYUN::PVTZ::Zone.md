# ALIYUN::PVTZ::Zone {#concept_omw_1cy_dhb .concept}

ALIYUN::PVTZ::Zone is used to create a private zone.

## Syntax {#section_hrg_dcy_dhb .section}

```
{
  "Type": "ALIYUN::PVTZ::Zone",
  "Properties": {
    "ProxyPattern": String,
    "Remark": String,
    "ZoneName": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ProxyPattern|String|No|Yes| ZONE: DNS records for the entire zone are hijacked.

 RECORD: Recursive resolution of public DNS records is enabled.

 |Valid values: ZONE and RECORD.|
|Remark|String|No|Yes|The remarks.|The remarks must be 1 to 50 characters in length.|
|ZoneName|String|Yes|No|The name of the zone.|None|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

ZoneId: the ID of the zone.

## Examples {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Zone": {
      "Type": "ALIYUN::PVTZ::Zone",
      "Properties": {
        "ProxyPattern": {
          "Ref": "ProxyPattern"
        },
        "Remark": {
          "Ref": "Remark"
        },
        "ZoneName": {
          "Ref": "ZoneName"
        }
      }
    }
  },
  "Parameters": {
    "ProxyPattern": {
      "Default": "ZONE",
      "Type": "String",
      "Description": "ZONE: DNS records for the entire zone are hijacked.\n RECORD: Recursive resolution of public DNS records is enabled.\nDefault to ZONE.",
      "AllowedValues": ["RECORD", "ZONE"]
    },
    "Remark": {
      "AllowedPattern": "^[-_,.\\uff0c\\u3002a-zA-Z0-9\\u4e00-\\u9fa5]{0,50}$",
      "Type": "String",
      "Description": "50 characters at most. It can only contain digits, letters, and special characters: \"_-,.\uff0c\u3002\".",
      "MaxLength": 50
    },
    "ZoneName": {
      "Type": "String",
      "Description": "Zone name"
    }
  },
  "Outputs": {
    "ZoneId": {
      "Description": "Zone ID",
      "value": {
        "Fn::GetAtt": ["Zone", "ZoneId"]
      }
    }
  }
}
```


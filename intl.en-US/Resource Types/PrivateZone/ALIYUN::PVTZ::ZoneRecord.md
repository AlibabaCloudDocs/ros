# ALIYUN::PVTZ::ZoneRecord {#concept_rsp_kcy_dhb .concept}

ALIYUN::PVTZ::ZoneRecord is used to add DNS records to a private zone.

## Syntax {#section_hrg_dcy_dhb .section}

```
{
  "Type": "ALIYUN::PVTZ::ZoneRecord",
  "Properties": {
    "Status": String,
    "Rr": String,
    "Value": String,
    "ZoneId": String,
    "Priority": Integer,
    "Ttl": Integer,
    "Type": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Status|String|Yes|Yes|The DNS resolution status.-   ENABLE: DNS resolution is enabled.
-   DISABLE: DNS resolution is disabled.

|Valid values: ENABLE and DISABLE.|
|Rr|String|Yes|Yes|The host record. For example, to resolve @.example.com, you must set the host record to an at sign \(@\). The record cannot be blank.|None|
|Value|String|Yes|Yes|The record value.|None|
|ZoneId|String|Yes|No|The ID of the zone.|None|
|Priority|Integer|No|Yes|The MX record priority.|Valid values: 1 to 10.|
|Ttl|Integer|No|Yes|The Time-to-Live \(TTL\) of a record. Default value: 60.|None|
|Type|String|Yes|Yes|The record type. You can add A, CNAME, TXT, MX, and PTR records to your private zone.|Valid values: A, CNAME, TXT, MX, and PTR.|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

RecordId: The ID of a DNS record.

## Examples {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ZoneRecord": {
      "Type": "ALIYUN::PVTZ::ZoneRecord",
      "Properties": {
        "Status": {
          "Ref": "Status"
        },
        "Rr": {
          "Ref": "Rr"
        },
        "Value": {
          "Ref": "Value"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "Priority": {
          "Ref": "Priority"
        },
        "Ttl": {
          "Ref": "Ttl"
        },
        "Type": {
          "Ref": "Type"
        }
      }
    }
  },
  "Parameters": {
    "Status": {
      "Default": "ENABLE",
      "Type": "String",
      "Description": "Allowed values: [ENABLE, DISABLE]",
      "AllowedValues": ["DISABLE", "ENABLE"]
    },
    "Rr": {
      "Type": "String",
      "Description": "The host record. For example, to resolve @.example.com, you must set the host record to an at sign (@). The record cannot be blank."
    },
    "value": {
      "Type": "String",
      "Description": "Record value"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone Id"
    },
    "Priority": {
      "Default": 10,
      "Type": "Number",
      "Description": "MX record priority, value range [1,10]. Default value: 10.",
      "MaxValue": 10,
      "MinValue": 1
    },
    "Ttl": {
      "Default": 60,
      "Type": "Number",
      "Description": "Survival time, default is 60"
    },
    "Type": {
      "Type": "String",
      "Description": "Analyze record type, currently only supports A, CNAME, TXT, MX, PTR",
      "AllowedValues": ["A", "CNAME", "MX", "PTR", "TXT"]
    }
  },
  "Outputs": {
    "RecordId": {
      "Description": "Parsing record Id",
      "Value": {
        "Fn::GetAtt": ["ZoneRecord", "RecordId"]
      }
    }
  }
}
```


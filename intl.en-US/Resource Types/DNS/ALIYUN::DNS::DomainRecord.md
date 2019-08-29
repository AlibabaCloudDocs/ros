# ALIYUN::DNS::DomainRecord {#concept_268247 .concept}

ALIYUN::DNS::DomainRecord is used to add a DNS record.

## Syntax {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::DNS::DomainRecord",
  "Properties": {
    "RR": String,
    "DomainName": String,
    "Value": String,
    "Priority": Integer,
    "TTL": Integer,
    "Line": String,
    "Type": String
  }
} 
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|RR|String|Yes|No|The host record. For example, to resolve @.example.com, you must set the host record to an at sign \(@\). The record cannot be blank.|None|
|DomainName|String|Yes|No|The domain name to be resolved.|None|
|Value|String|Yes|No|The value of the DNS record.|None|
|Priority|Integer|No|Yes|The priority of the MX record.|None|
|TTL|Integer|No|Yes|The time-to-live \(TTL\) of the record. Default value: 600. Unit: seconds. For more information, see [TTL definition](https://partners-intl.aliyun.com/help/doc-detail/34338.htm).|None|
|Line|String|No|Yes|The ISP line. Default value: default. For more information, see [ISP line enumeration](https://partners-intl.aliyun.com/help/doc-detail/34339.htm).|None|
|Type|String|Yes|No|The type of the DNS record. For more information, see [DNS record types](https://partners-intl.aliyun.com/help/doc-detail/34337.htm).|None|

## Response parameters {#section_y5a_2if_n88 .section}

 **Fn::GetAtt** 

RecordId: the ID of the DNS record.

## Examples {#section_omv_cs6_mhg .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DomainRecord": {
      "Type": "ALIYUN::DNS::DomainRecord",
      "Properties": {
        "RR": {
          "Ref": "RR"
        },
        "DomainName": {
          "Ref": "DomainName"
        },
        "Value": {
          "Ref": "Value"
        },
        "Priority": {
          "Ref": "Priority"
        },
        "TTL": {
          "Ref": "TTL"
        },
        "Line": {
          "Ref": "Line"
        },
        "Type": {
          "Ref": "Type"
        }
      }
    }
  },
  "Parameters": {
    "RR": {
      "Type": "String",
      "Description": "The host record. For example, to resolve @.example.com, you must set the host record to an at sign (@). The record cannot be blank."
    },
    "DomainName": {
      "Type": "String",
      "Description": "Domain name"
    },
    "Value": {
      "Type": "String",
      "Description": "Record value"
    },
    "Priority": {
      "Type": "Number",
      "Description": "The priority of the MX record. Valid values: [1, 10]. When the record type is MX record, this parameter must be specified.",
      "MaxValue": 10,
      "MinValue": 1
    },
    "TTL": {
      "Default": 600,
      "Type": "Number",
      "Description": "The resolution time is valid. The default value is 600 seconds (10 minutes). See the TTL definition."
    },
    "Line": {
      "Type": "String",
      "Description": "The ISP line. The default value is default. See ISP line enumeration."
    },
    "Type": {
      "Type": "String",
      "Description": "The record type. See DNS record types."
    }
  },
  "Outputs": {
    "RecordId": {
      "Description": "The ID of the DNS record",
      "Value": {
        "Fn::GetAtt": [
          "DomainRecord",
          "RecordId"
        ]
      }
    }
  }
}
```


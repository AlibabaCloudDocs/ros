# ALIYUN::DNS::DomainRecord

ALIYUN::DNS::DomainRecord is used to add a DNS record.

## Syntax

```
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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RR|String|Yes|No|The host record. For example, to resolve @.example.com, you must set the host record to an at sign \(@\). The record cannot be left empty.|None|
|DomainName|String|Yes|No|The domain name to be resolved.|None|
|Value|String|Yes|No|The value of the DNS record.|None|
|Priority|Integer|No|Yes|The priority of the MX-type DNS record.|None|
|TTL|Integer|No|Yes|The time-to-live \(TTL\) of the record. Unit: seconds. Default value: 600. For more information, see [TTL Definition Description](https://www.alibabacloud.com/help/doc-detail/34338.htm).|None|
|Line|String|No|Yes|The Internet service provider \(ISP\) line. Default value: default. For more information, see [Resolution Line Enumeration](https://www.alibabacloud.com/help/doc-detail/34339.htm).|None|
|Type|String|Yes|No|The type of the DNS record. For more information, see [Resolution Record Type Formats](https://www.alibabacloud.com/help/doc-detail/34337.htm).|Valid values: A, CNAME, NS, MX, TXT, SRV, CAA, REDIRECT\_URL, and FORWARD\_URL.|

## Response parameters

Fn::GetAtt

RecordId: the ID of the DNS record.

## Examples

```
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
      "Description": "Host record, if you want to resolve @.exmaple.com, the host record should fill in \"@\" instead of empty"
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
      "Description": "The priority of the MX record, the value range [1,10], when the record type is MX record, this parameter must be",
      "MaxValue": 10,
      "MinValue": 1
    },
    "TTL": {
      "Default": 600,
      "Type": "Number",
      "Description": "The resolution time is valid. The default is 600 seconds (10 minutes). See the TTL definition."
    },
    "Line": {
      "Type": "String",
      "Description": "Parse the line, the default is default. See parsing line enumeration"
    },
    "Type": {
      "Type": "String",
      "Description": "Parse record type, see parsing record type format"
    }
  },
  "Outputs": {
    "RecordId": {
      "Description": "Parse the ID of the record",
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


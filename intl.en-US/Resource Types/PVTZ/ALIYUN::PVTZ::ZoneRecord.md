# ALIYUN::PVTZ::ZoneRecord

ALIYUN::PVTZ::ZoneRecord is used to add a Domain Name Service \(DNS\) record to a private zone.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Status|String|Yes|Yes|The status of DNS resolution.|Valid values: -   ENABLE: DNS resolution is enabled.
-   DISABLE: DNS resolution is disabled. |
|Rr|String|Yes|Yes|The host record.|For example, to resolve `@.example.com`, you must set Rr to an at sign \(@\) instead of leaving it blank.|
|Value|String|Yes|Yes|The record value.|None|
|ZoneId|String|Yes|No|The ID of the private zone.|None|
|Priority|Integer|No|Yes|The priority of the MX-type DNS record.|Valid values: 1 to 99. Default value: 10. |
|Ttl|Integer|No|Yes|The time-to-live \(TTL\) of the record.|Default value: 60.|
|Type|String|Yes|Yes|The type of the DNS record.|Valid values: -   A
-   CNAME
-   TXT
-   MX
-   PTR |

## Response parameters

Fn::GetAtt

-   RecordId: the ID of the DNS record.
-   Record: the content of the DNS record.
-   ZoneId: the ID of the private zone.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Status": {
      "Type": "String",
      "Description": "Allowed values: [ENABLE, DISABLE]",
      "AllowedValues": [
        "DISABLE",
        "ENABLE"
      ],
      "Default": "ENABLE"
    },
    "Rr": {
      "Type": "String",
      "Description": "Host record, if you want to resolve @.exmaple.com, the host record should fill in \"@\" instead of empty"
    },
    "Type": {
      "Type": "String",
      "Description": "Analyze record type, currently only supports A, AAAA, CNAME, TXT, MX, PTR, SRV",
      "AllowedValues": [
        "A",
        "AAA",
        "CNAME",
        "TXT",
        "MX",
        "PTR",
        "SRV"
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone Id"
    },
    "Priority": {
      "Type": "Number",
      "Description": "MX record priority, value range [1,99]. Default to 10.",
      "MinValue": 1,
      "MaxValue": 99,
      "Default": 10
    },
    "Value": {
      "Type": "String",
      "Description": "Record value"
    },
    "Ttl": {
      "Type": "Number",
      "Description": "Survival time, default is 60",
      "Default": 60
    }
  },
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
        "Type": {
          "Ref": "Type"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "Priority": {
          "Ref": "Priority"
        },
        "Value": {
          "Ref": "Value"
        },
        "Ttl": {
          "Ref": "Ttl"
        }
      }
    }
  },
  "Outputs": {
    "ZoneId": {
      "Description": "Zone ID.",
      "Value": {
        "Fn::GetAtt": [
          "ZoneRecord",
          "ZoneId"
        ]
      }
    },
    "Record": {
      "Description": "Record data.",
      "Value": {
        "Fn::GetAtt": [
          "ZoneRecord",
          "Record"
        ]
      }
    },
    "RecordId": {
      "Description": "Parsing record Id",
      "Value": {
        "Fn::GetAtt": [
          "ZoneRecord",
          "RecordId"
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
  Priority:
    Default: 10
    Description: MX record priority, value range [1,99]. Default to 10.
    MaxValue: 99
    MinValue: 1
    Type: Number
  Rr:
    Description: Host record, if you want to resolve @.exmaple.com, the host record
      should fill in "@" instead of empty
    Type: String
  Status:
    AllowedValues:
    - DISABLE
    - ENABLE
    Default: ENABLE
    Description: 'Allowed values: [ENABLE, DISABLE]'
    Type: String
  Ttl:
    Default: 60
    Description: Survival time, default is 60
    Type: Number
  Type:
    AllowedValues:
    - A
    - AAA
    - CNAME
    - TXT
    - MX
    - PTR
    - SRV
    Description: Analyze record type, currently only supports A, AAAA, CNAME, TXT,
      MX, PTR, SRV
    Type: String
  Value:
    Description: Record value
    Type: String
  ZoneId:
    Description: Zone Id
    Type: String
Resources:
  ZoneRecord:
    Properties:
      Priority:
        Ref: Priority
      Rr:
        Ref: Rr
      Status:
        Ref: Status
      Ttl:
        Ref: Ttl
      Type:
        Ref: Type
      Value:
        Ref: Value
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::PVTZ::ZoneRecord
Outputs:
  Record:
    Description: Record data.
    Value:
      Fn::GetAtt:
      - ZoneRecord
      - Record
  RecordId:
    Description: Parsing record Id
    Value:
      Fn::GetAtt:
      - ZoneRecord
      - RecordId
  ZoneId:
    Description: Zone ID.
    Value:
      Fn::GetAtt:
      - ZoneRecord
      - ZoneId
```

For more examples, see [PVTZ.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json) and [PVTZ.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml). In the examples, the ALIYUN::PVTZ::Zone, ALIYUN::PVTZ::ZoneRecord, and ALIYUN::PVTZ::ZoneVpcBinder resource types are involved.


# ALIYUN::PVTZ::Zone

ALIYUN::PVTZ::Zone is used to create a private zone.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ProxyPattern|String|No|Yes|The proxy mode.|Valid values:-   ZONE: DNS records for the entire zone are hijacked.
-   RECORD: Recursive resolution of public DNS records is enabled. |
|Remark|String|No|Yes|The description of the zone.|The description can be up to 50 characters in length.|
|ZoneName|String|Yes|No|The name of the zone.|None|

## Response parameters

Fn::GetAtt

-   ZoneName: the name of the zone.
-   ZoneId: the ID of the zone.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ZoneName": {
      "Type": "String",
      "Description": "Zone name"
    },
    "ProxyPattern": {
      "Type": "String",
      "Description": "ZONE: completely hijack the entire zone.\nRECORD: Incomplete hijacking, recursive resolution agent.\nDefault to ZONE.",
      "AllowedValues": [
        "RECORD",
        "ZONE"
      ],
      "Default": "ZONE"
    },
    "Remark": {
      "Type": "String",
      "Description": "50 characters at most. It can only contain numbers, Chinese, English and special characters: \ " _ - , \".",
      "AllowedPattern": "^[-_,.\\uff0c\\u3002a-zA-Z0-9\\u4e00-\\u9fa5]{0,50}$",
      "MaxLength": 50
    }
  },
  "Resources": {
    "Zone": {
      "Type": "ALIYUN::PVTZ::Zone",
      "Properties": {
        "ZoneName": {
          "Ref": "ZoneName"
        },
        "ProxyPattern": {
          "Ref": "ProxyPattern"
        },
        "Remark": {
          "Ref": "Remark"
        }
      }
    }
  },
  "Outputs": {
    "ZoneName": {
      "Description": "Zone name",
      "Value": {
        "Fn::GetAtt": [
          "Zone",
          "ZoneName"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone ID",
      "Value": {
        "Fn::GetAtt": [
          "Zone",
          "ZoneId"
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
  ProxyPattern:
    AllowedValues:
    - RECORD
    - ZONE
    Default: ZONE
    Description: 'ZONE: completely hijack the entire zone.

      RECORD: Incomplete hijacking, recursive resolution agent.

      Default to ZONE.'
    Type: String
  Remark:
    AllowedPattern: ^[-_,.\uff0c\u3002a-zA-Z0-9\u4e00-\u9fa5]{0,50}$
    Description: "50 characters at most. It can only contain numbers, Chinese, English\
      \ and special characters: \"_-,.\uFF0C\u3002\"."
    MaxLength: 50
    Type: String
  ZoneName:
    Description: Zone name
    Type: String
Resources:
  Zone:
    Properties:
      ProxyPattern:
        Ref: ProxyPattern
      Remark:
        Ref: Remark
      ZoneName:
        Ref: ZoneName
    Type: ALIYUN::PVTZ::Zone
Outputs:
  ZoneId:
    Description: Zone ID
    Value:
      Fn::GetAtt:
      - Zone
      - ZoneId
  ZoneName:
    Description: Zone name
    Value:
      Fn::GetAtt:
      - Zone
      - ZoneName
```

For more examples, see [PVTZ.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json) and [PVTZ.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml). In the examples, the ALIYUN::PVTZ::Zone, ALIYUN::PVTZ::ZoneRecord, and ALIYUN::PVTZ::ZoneVpcBinder resource types are involved.


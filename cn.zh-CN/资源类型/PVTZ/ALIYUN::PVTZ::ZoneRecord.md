# ALIYUN::PVTZ::ZoneRecord

ALIYUN::PVTZ::ZoneRecord类型用于添加PrivateZone的解析记录。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Status|String|是|是|状态。|取值： -   ENABLE：启用解析。
-   DISABLE：暂停解析。 |
|Rr|String|是|是|主机记录。|如果要解析`@.exmaple.com`，主机记录要填写at（@），而不是空。|
|Value|String|是|是|记录值。|无|
|ZoneId|String|是|否|可用区ID。|无|
|Priority|Integer|否|是|MX记录的优先级。|取值范围：1~99。默认值：10。 |
|Ttl|Integer|否|是|生存时间。|默认值：60。|
|Type|String|是|是|解析记录类型。|取值： -   A
-   CNAME
-   TXT
-   MX
-   PTR |

## 返回值

Fn::GetAtt

-   RecordId：解析记录ID。
-   Record：解析记录内容。
-   ZoneId：可用区ID。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建PrivateZone、添加PrivateZone解析记录和绑定或解绑Zone与专有网络列表的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml)。


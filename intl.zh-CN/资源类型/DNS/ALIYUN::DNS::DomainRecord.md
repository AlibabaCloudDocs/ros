# ALIYUN::DNS::DomainRecord

ALIYUN::DNS::DomainRecord类型用于添加解析记录。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RR|String|是|否|主机记录，如果要解析@.exmaple.com，主机记录要填写”@”，而不是空。|无。|
|DomainName|String|是|否|域名名称。|无。|
|Value|String|是|否|记录值。|无。|
|Priority|Integer|否|是|MX记录的优先级。|无。|
|TTL|Integer|否|是|解析生效时间，默认为600秒（10分钟），参见[TTL定义说明](https://www.alibabacloud.com/help/doc-detail/34338.htm)。|无。|
|Line|String|否|是|解析线路，默认为default，参见[解析线路枚举](https://www.alibabacloud.com/help/doc-detail/34339.htm)。|无。|
|Type|String|是|否|解析记录类型，参见[解析记录类型格式](https://www.alibabacloud.com/help/doc-detail/34337.htm)。|取值范围：A、CNAME、NS、MX、TXT、SRV、CAA、REDIRECT\_URL、FORWARD\_URL。|

## 返回值

Fn::GetAtt

RecordId：解析记录的ID。

## 示例

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


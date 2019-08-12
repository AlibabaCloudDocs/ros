# ALIYUN::PVTZ::ZoneRecord {#concept_rsp_kcy_dhb .concept}

ALIYUN::PVTZ::ZoneRecord 用于添加prviate zone的解析记录。

## 语法 {#section_hrg_dcy_dhb .section}

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

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Status|String|是|是|状态。-   ENABLE: 启用解析
-   DISABLE: 暂停解析

|可用值：ENABLE、DISABLE。|
|Rr|String|是|是|主机记录，如果要解析@.exmaple.com，主机记录要填写"@”，而不是空。|无。|
|Value|String|是|是|记录值。|无。|
|ZoneId|String|是|否|zone Id。|无。|
|Priority|Integer|否|是|MX记录的优先级。|取值范围\[1,10\]。|
|Ttl|Integer|否|是|生存时间，默认为60。|无。|
|Type|String|是|是|解析记录类型，目前仅支持A, CNAME, TXT, MX, PTR。|可用值：A、CNAME、TXT、 MX、 PTR。|

## 返回值 {#section_utp_2wq_dhb .section}

**FN::GetAtt**

RecordId:Parsing record Id。

## 示例 {#section_mn3_wwq_dhb .section}

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
      "Description": "Host record, if you want to resolve @.exmaple.com, the host record should fill in \"@\" instead of empty"
    },
    "Value": {
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
      "Description": "MX record priority, value range [1,10]. Default to 10.",
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


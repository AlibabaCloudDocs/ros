# ALIYUN::PVTZ::Zone {#concept_omw_1cy_dhb .concept}

ALIYUN::PVTZ::Zone 用于创建private zone。

## 语法 {#section_hrg_dcy_dhb .section}

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

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProxyPattern|String|否|是| ZONE：完全劫持整个Zone

 RECORD：不完全劫持，进行递归解析代理。

 |可用值：ZONE、RECORD。|
|Remark|String|否|是|备注。|最大长度50个字符。|
|ZoneName|String|是|否|zone名称。|无。|

## 返回值 {#section_utp_2wq_dhb .section}

**FN::GetAtt**

ZoneId:Zone ID。

## 示例 {#section_mn3_wwq_dhb .section}

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
      "Description": "ZONE: completely hijack the entire zone.\nRECORD: Incomplete hijacking, recursive resolution agent.\nDefault to ZONE.",
      "AllowedValues": ["RECORD", "ZONE"]
    },
    "Remark": {
      "AllowedPattern": "^[-_,.\\uff0c\\u3002a-zA-Z0-9\\u4e00-\\u9fa5]{0,50}$",
      "Type": "String",
      "Description": "50 characters at most. It can only contain numbers, Chinese, English and special characters: \"_-,.\uff0c\u3002\".",
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
      "Value": {
        "Fn::GetAtt": ["Zone", "ZoneId"]
      }
    }
  }
}
```


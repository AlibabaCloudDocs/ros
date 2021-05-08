# ALIYUN::PVTZ::Zone

ALIYUN::PVTZ::Zone用于创建PrivateZone。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProxyPattern|String|否|是|代理模式。|取值：-   ZONE：完全劫持整个Zone。
-   RECORD：不完全劫持，进行递归解析代理。 |
|Remark|String|否|是|备注信息。|最大支持50个字符。|
|ZoneName|String|是|否|可用区名称。|无|

## 返回值

Fn::GetAtt

-   ZoneName：可用区名称。
-   ZoneId：可用区ID。

## 示例

`JSON`格式

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
      "Description": "50 characters at most. It can only contain numbers, Chinese, English and special characters: \"_-,.，。\".",
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

`YAML`格式

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

更多示例，请参见创建PrivateZone、添加PrivateZone解析记录和绑定或解绑Zone与专有网络列表的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml)。


# ALIYUN::PVTZ::ZoneVpcBinder

ALIYUN::PVTZ::ZoneVpcBinder用于绑定或者解绑Zone与专有网络列表。

## 语法

```
{
  "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
  "Properties": {
    "Vpcs": List,
    "ZoneId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Vpcs|List|是|是|专有网络列表。|最多支持10个专有网络。更多信息，请参见[Vpcs属性](#section_yqf_c2y_dhb)。 |
|ZoneId|String|是|否|可用区ID。|无|

## Vpcs语法

```
"Vpcs": [
  {
    "VpcId": String,
    "RegionId": String
  }
]
```

## Vpcs属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|专有网络ID。|无|
|RegionId|String|是|否|地域ID。|无|

## 返回值

Fn::GetAtt

-   ZoneId：可用区ID。
-   Vpcs：绑定的VPC。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Vpcs": {
      "Type": "Json",
      "Description": "",
      "MinLength": 0,
      "MaxLength": 10
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone Id"
    }
  },
  "Resources": {
    "ZoneVpcBinder": {
      "Type": "ALIYUN::PVTZ::ZoneVpcBinder",
      "Properties": {
        "Vpcs": {
          "Ref": "Vpcs"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        }
      }
    }
  },
  "Outputs": {
    "Vpcs": {
      "Description": "Vpc list",
      "Value": {
        "Fn::GetAtt": [
          "ZoneVpcBinder",
          "Vpcs"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone Id",
      "Value": {
        "Fn::GetAtt": [
          "ZoneVpcBinder",
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
  Vpcs:
    Description: ''
    MaxLength: 10
    MinLength: 0
    Type: Json
  ZoneId:
    Description: Zone Id
    Type: String
Resources:
  ZoneVpcBinder:
    Properties:
      Vpcs:
        Ref: Vpcs
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::PVTZ::ZoneVpcBinder
Outputs:
  Vpcs:
    Description: Vpc list
    Value:
      Fn::GetAtt:
      - ZoneVpcBinder
      - Vpcs
  ZoneId:
    Description: Zone Id
    Value:
      Fn::GetAtt:
      - ZoneVpcBinder
      - ZoneId
```

更多示例，请参见创建PrivateZone、添加PrivateZone解析记录和绑定或解绑Zone与专有网络列表的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/JSON/PVTZ.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/PVTZ/YAML/PVTZ.yml)。


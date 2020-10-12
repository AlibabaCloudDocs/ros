# ALIYUN::RDS::DBInstanceParameterGroup

ALIYUN::RDS::DBInstanceParameterGroup类型用于修改数据库参数列表。

## 语法

```
{
  "Type": "ALIYUN::RDS::DBInstanceParameterGroup",
  "Properties": {
    "Forcerestart": String,
    "DBInstanceId": String,
    "Parameters": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DBInstanceId|String|是|否|数据库实例ID。|无|
|Parameters|List|是|否|实例参数。|详情请参见[Parameters属性](#section_nvv_kg2_29b)。|
|Forcerestart|String|否|否|是否强制重启数据库实例。|取值范围： -   true：强制重启。
-   false（默认值）：不强制重启。 |

## Parameters语法

```
"Parameters": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Parameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|参数|无|
|Value|String|是|否|参数值|无|

## 返回值

Fn::GetAtt

无。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Parameters": {
      "Type": "Json",
      "Description": "Parameters to update for selected database instance."
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "Database InstanceId to update properties."
    },
    "Forcerestart": {
      "Type": "String",
      "Description": "whether restart database instance.",
      "AllowedValues": [
        "true",
        "false"
      ],
      "Default": "false"
    }
  },
  "Resources": {
    "DBInstanceParameterGroup": {
      "Type": "ALIYUN::RDS::DBInstanceParameterGroup",
      "Properties": {
        "Parameters": {
          "Ref": "Parameters"
        },
        "DBInstanceId": {
          "Ref": "DBInstanceId"
        },
        "Forcerestart": {
          "Ref": "Forcerestart"
        }
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  Parameters:
    Type: Json
    Description: Parameters to update for selected database instance.
  DBInstanceId:
    Type: String
    Description: Database InstanceId to update properties.
  Forcerestart:
    Type: String
    Description: whether restart database instance.
    AllowedValues:
      - 'true'
      - 'false'
    Default: 'false'
Resources:
  DBInstanceParameterGroup:
    Type: 'ALIYUN::RDS::DBInstanceParameterGroup'
    Properties:
      Parameters:
        Ref: Parameters
      DBInstanceId:
        Ref: DBInstanceId
      Forcerestart:
        Ref: Forcerestart
```


# Aliyun::Serverless::TableStore::Table

Aliyun::Serverless::TableStore::Table类型用于使用主键列表创建 TableStore（OTS）表。

## 语法

```
{
  "Type": "Aliyun::Serverless::TableStore::Table",
  "Properties": {
    "PrimaryKeyList": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PrimaryKeyList|List|是|否|要用作表主键的列表项的属性名称和类型。|更多信息，请参见[PrimaryKeyList属性](#section_jyo_w3g_bey)。|

## PrimaryKeyList语法

```
"PrimaryKeyList": [
  {
    "Type": String,
    "Name": String
  }
]
```

## PrimaryKeyList属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|否|主键的类型。|取值：-   INTEGER：整数。
-   STRING：字符串。
-   BINARY：二进制。 |
|Name|String|是|否|主键的名称。|无|

## 返回值

Fn::GetAtt

TableName：表名。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Parameters": {
    "ClusterType": {
      "Type": "String",
      "Default": "HYBRID"
    },
    "PK": {
      "Type": "Json",
      "Default": [
        {
          "Name": "count_name",
          "Type": "STRING"
        }
      ]
    }
  },
  "Resources": {
    "MyInstance": {
      "Type": "Aliyun::Serverless::TableStore",
      "Properties": {
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "Description": "Description for MyOtsInstance"
      },
      "MyTable": {
        "Type": "Aliyun::Serverless::TableStore::Table",
        "Properties": {
          "PrimaryKeyList": {
            "Ref": "PK"
          }
        }
      }
    }
  },
  "Outputs": {
    "TableName": {
      "Value": {
        "Fn::GetAtt": [
          "MyInstanceMyTable",
          "TableName"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Parameters:
  ClusterType:
    Type: String
    Default: HYBRID
  PK:
    Type: Json
    Default:
      - Name: count_name
        Type: STRING
Resources:
  MyInstance:
    Type: 'Aliyun::Serverless::TableStore'
    Properties:
      ClusterType:
        Ref: ClusterType
      Description: Description for MyOtsInstance
    MyTable:
      Type: 'Aliyun::Serverless::TableStore::Table'
      Properties:
        PrimaryKeyList:
          Ref: PK
Outputs:
  TableName:
    Value:
      'Fn::GetAtt':
        - MyInstanceMyTable
        - TableName
```


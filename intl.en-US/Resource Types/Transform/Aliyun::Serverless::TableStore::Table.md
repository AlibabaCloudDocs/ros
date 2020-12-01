# Aliyun::Serverless::TableStore::Table

Aliyun::Serverless::TableStore::Table is used to create a table based on one or more primary key columns.

## Syntax

```
{
  "Type": "Aliyun::Serverless::TableStore::Table",
  "Properties": {
    "PrimaryKeyList": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PrimaryKeyList|List|Yes|No|The list of primary key column names and types used in the table.|For more information, see [PrimaryKeyList properties](#section_jyo_w3g_bey).|

## PrimaryKeyList syntax

```
"PrimaryKeyList": [
  {
    "Type": String,
    "Name": String
  }
]
```

## PrimaryKeyList properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|Yes|No|The type of the primary key column.|Valid values:-   INTEGER
-   STRING
-   BINARY |
|Name|String|Yes|No|The name of the primary key column.|None|

## Response parameters

Fn::GetAtt

TableName: the name of the table.

## Examples

`JSON` format

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

`YAML` format

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


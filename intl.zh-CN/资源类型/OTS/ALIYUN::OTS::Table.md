# ALIYUN::OTS::Table

ALIYUN::OTS::Table类型用于根据指定的表结构信息创建相应的表。

## 语法

```
{
  "Type": "ALIYUN::OTS::Table",
  "Properties": {
    "ReservedThroughput": Map,
    "MaxVersions": Integer,
    "TableName": String,
    "SecondaryIndices": List,
    "DeviationCellVersionInSec": Integer,
    "TimeToLive": Integer,
    "InstanceName": String,
    "PrimaryKey": List,
    "Columns": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ReservedThroughput|Map|否|是|表的初始预留读或写吞吐量设定。|任何表的预留读吞吐量与预留写吞吐量均不能超过5000次/秒。 详情请参见[ReservedThroughput属性](#section_hea_478_miu)。 |
|MaxVersions|Integer|否|是|表保留的最大版本数。|取值范围：1~2,147,483,647。 默认值：1。 |
|TableName|String|是|否|表的名称。|无|
|SecondaryIndices|List|否|否|表的二级指标。|详情请参见[SecondaryIndices属性](#section_b0o_gdl_hkl)。|
|DeviationCellVersionInSec|Integer|否|是|最高版本偏差。|用于禁止写入与预期较大的数据。例如：当前时间戳为10000，如果将DeviationCellVersionInSec设置为1000，则允许写入的时间戳范围为：9000~11000。 取值范围：1~9,223,372,036,854,775807。

默认值：86,400。 |
|TimeToLive|Integer|否|是|表中数据的保留时间。|最大值：2,147,483,647。

默认值：1。

单位：秒。

-1表示永不过期。 |
|InstanceName|String|是|否|表所在的OTS实例的名称。|无|
|PrimaryKey|List|是|否|表全部的主键列。|取值范围：1~4。 详情请参见[PrimaryKey属性](#section_7cy_pd9_flv)。 |
|Columns|List|否|否|表存储的属性列。|详情请参见[Columns属性](#section_7s0_myl_zkh)。|

## ReservedThroughput语法

```
"ReservedThroughput": {
  "Read": Integer,
  "Write": Integer
}
```

## ReservedThroughput属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Read|Integer|是|是|使用的读服务能力单元或表的预留读吞吐量。|默认值：0。|
|Write|Integer|是|是|使用的写服务能力单元或表的预留写吞吐量。|默认值：0。|

## SecondaryIndices语法

```
"SecondaryIndices": [
  {
    "IndexName": String,
    "IndexType": String,
    "Columns": List,
    "PrimaryKeys": List
  }
]
```

## SecondaryIndices属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IndexName|String|是|否|索引名称|无|
|IndexType|String|否|否|索引类型|取值： -   Global
-   Local |
|Columns|List|是|否|索引列|无|
|PrimaryKeys|List|是|否|主键|无|

## PrimaryKey语法

```
"PrimaryKey": [
  {
    "Type": String,
    "Name": String
  }
]
```

## PrimaryKey属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|否|主键的类型|取值：-   INTEGER：整数
-   STRING：字符串
-   BINARY：二进制 |
|Name|String|是|否|主键的名称|无|

## Columns语法

```
"Columns": [
  {
    "Type": String,
    "Name": String
  }
]
```

## Columns属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|否|列的类型|无|
|Name|String|是|否|列的名字|无|

## 返回值

Fn::GetAtt

TableName：表名。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Table": {
      "Type": "ALIYUN::OTS::Table",
      "Properties": {
        "ReservedThroughput": {
          "Ref": "ReservedThroughput"
        },
        "MaxVersions": {
          "Ref": "MaxVersions"
        },
        "TableName": {
          "Ref": "TableName"
        },
        "SecondaryIndices": {
          "Ref": "SecondaryIndices"
        },
        "DeviationCellVersionInSec": {
          "Ref": "DeviationCellVersionInSec"
        },
        "TimeToLive": {
          "Ref": "TimeToLive"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "PrimaryKey": {
          "Ref": "PrimaryKey"
        },
        "Columns": {
          "Ref": "Columns"
        }
      }
    }
  },
  "Parameters": {
    "ReservedThroughput": {
      "Type": "Json",
      "Description": "The initial reserved read/write throughput setting of the table to be created, the reserved read throughput and reserved write throughput of any table cannot exceed 5000."
    },
    "MaxVersions": {
      "Default": 1,
      "Type": "Number",
      "Description": "The maximum number of versions stored in this table. The valid value is 1-2147483647. Default to 1.",
      "MaxValue": 2147483647,
      "MinValue": 1
    },
    "TableName": {
      "AllowedPattern": "[_a-zA-Z][_a-zA-Z0-9]{0,254}",
      "Type": "String",
      "Description": "The table name of the OTS instance."
    },
    "SecondaryIndices": {
      "Type": "Json",
      "Description": "The secondary indices of the table.",
      "Default": [
        {
          "IndexName": "service_name_index",
          "IndexType": "Global",
          "Columns": ["event_name"],
          "PrimaryKeys": ["account", "service_name"]
        }
      ]
    },
    "DeviationCellVersionInSec": {
      "Default": 86400,
      "Type": "Number",
      "Description": "Maximum version deviation. The purpose is mainly to prohibit writing and expected large data, such as setting the deviation_cell_version_in_sec to 1000, and if the current timestamp is 10000, the timestamp range allowed to be written is [10000 - 1000, 10000 + 1000]. The valid value is 1-9223372036854775807. Defaults to 86400.",
      "MaxValue": 9223372036854775807,
      "MinValue": 1
    },
    "TimeToLive": {
      "Default": -1,
      "Type": "Number",
      "Description": "The retention time of data stored in this table (unit: second). The value maximum is 2147483647 and -1 means never expired. Default to -1.",
      "MaxValue": 2147483647,
      "MinValue": -1
    },
    "InstanceName": {
      "AllowedPattern": "[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]",
      "Type": "String",
      "Description": "The name of the OTS instance in which table will locate."
    },
    "PrimaryKey": {
      "MinLength": 1,
      "Type": "Json",
      "Description": "It describes the attribute value of primary key. The number of primary_key should not be less than one and not be more than four.",
      "MaxLength": 4
    },
    "Columns": {
      "Type": "Json",
      "Description": "Attribute column for table store."
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Table:
    Type: 'ALIYUN::OTS::Table'
    Properties:
      ReservedThroughput:
        Ref: ReservedThroughput
      MaxVersions:
        Ref: MaxVersions
      TableName:
        Ref: TableName
      SecondaryIndices:
        Ref: SecondaryIndices
      DeviationCellVersionInSec:
        Ref: DeviationCellVersionInSec
      TimeToLive:
        Ref: TimeToLive
      InstanceName:
        Ref: InstanceName
      PrimaryKey:
        Ref: PrimaryKey
      Columns:
        Ref: Columns
Parameters:
  ReservedThroughput:
    Type: Json
    Description: >-
      The initial reserved read/write throughput setting of the table to be
      created, the reserved read throughput and reserved write throughput of any
      table cannot exceed 5000.
  MaxVersions:
    Default: 1
    Type: Number
    Description: >-
      The maximum number of versions stored in this table. The valid value is
      1-2147483647. Default to 1.
    MaxValue: 2147483647
    MinValue: 1
  TableName:
    AllowedPattern: '[_a-zA-Z][_a-zA-Z0-9]{0,254}'
    Type: String
    Description: The table name of the OTS instance.
  SecondaryIndices:
    Type: Json
    Description: The secondary indices of the table.
    Default:
      - IndexName: service_name_index
        IndexType: Global
        Columns:
          - event_name
        PrimaryKeys:
          - account
          - service_name
  DeviationCellVersionInSec:
    Default: 86400
    Type: Number
    Description: >-
      Maximum version deviation. The purpose is mainly to prohibit writing and
      expected large data, such as setting the deviation_cell_version_in_sec to
      1000, and if the current timestamp is 10000, the timestamp range allowed
      to be written is [10000 - 1000, 10000 + 1000]. The valid value is
      1-9223372036854775807. Defaults to 86400.
    MaxValue: 9223372036854776000
    MinValue: 1
  TimeToLive:
    Default: -1
    Type: Number
    Description: >-
      The retention time of data stored in this table (unit: second). The value
      maximum is 2147483647 and -1 means never expired. Default to -1.
    MaxValue: 2147483647
    MinValue: -1
  InstanceName:
    AllowedPattern: '[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]'
    Type: String
    Description: The name of the OTS instance in which table will locate.
  PrimaryKey:
    MinLength: 1
    Type: Json
    Description: >-
      It describes the attribute value of primary key. The number of primary_key
      should not be less than one and not be more than four.
    MaxLength: 4
  Columns:
    Type: Json
    Description: Attribute column for table store.
```


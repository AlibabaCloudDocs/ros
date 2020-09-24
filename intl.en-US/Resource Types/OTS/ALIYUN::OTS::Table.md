# ALIYUN::OTS::Table

ALIYUN::OTS::Table is used to create a table based on a specified schema.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ReservedThroughput|Map|No|Yes|The initial reserved read/write throughput settings of the table.|The reserved read/write throughput of a table cannot exceed 5,000 per second. For more information, see [ReservedThroughput properties](#section_hea_478_miu). |
|MaxVersions|Integer|No|Yes|The maximum number of data versions that can be retained in the table.|Valid values: 1 to 2147483647. Default value: 1. |
|TableName|String|Yes|No|The name of the table.|None|
|SecondaryIndices|List|No|No|The secondary indices of the table.|For more information, see [SecondaryIndices properties](#section_b0o_gdl_hkl).|
|DeviationCellVersionInSec|Integer|No|Yes|The maximum time deviation between the timestamp of written data and current system time.|This parameter is used to prevent users from writing data that is larger than expected. For example, if the current timestamp is 10000 and the DeviationCellVersionInSec parameter is set to 1000, the allowed timestamp range during data writing is \[10000 - 1000, 10000 + 1000\]. Valid values: 1 to 9223372036854775807.

 Default value: 86400. |
|TimeToLive|Integer|No|Yes|The retention period of data stored in the table.|Maximum value: 2147483647.

 Default value: 1.

 Unit: seconds.

 A value of -1 indicates that the data never expires. |
|InstanceName|String|Yes|No|The name of the instance where the table resides.|None|
|PrimaryKey|List|Yes|No|All primary key columns of the table.|Valid values: 1 to 4. For more information, see [PrimaryKey properties](#section_7cy_pd9_flv). |
|Columns|List|No|No|The attribute columns of the table.|For more information, see [Columns properties](#section_7s0_myl_zkh).|

## ReservedThroughput syntax

```
"ReservedThroughput": {
  "Read": Integer,
  "Write": Integer
}
```

## ReservedThroughput properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Read|Integer|Yes|Yes|The number of consumed read CUs or the reserved read throughput of the table.|Default value: 0.|
|Write|Integer|Yes|Yes|The number of consumed write CUs or the reserved write throughput of the table.|Default value: 0.|

## SecondaryIndices syntax

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

## SecondaryIndices properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|IndexName|String|Yes|No|The name of the index.|None|
|IndexType|String|No|No|The type of the index.|Valid values: -   Global
-   Local |
|Columns|List|Yes|No|The columns of the index.|None|
|PrimaryKeys|List|Yes|No|The primary keys of the index.|None|

## PrimaryKey syntax

```
"PrimaryKey": [
  {
    "Type": String,
    "Name": String
  }
]
```

## PrimaryKey properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|Yes|No|The type of the primary key.|Valid values: -   INTEGER
-   STRING
-   BINARY |
|Name|String|Yes|No|The name of the primary key.|None|

## Columns syntax

```
"Columns": [
  {
    "Type": String,
    "Name": String
  }
]
```

## Columns properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|Yes|No|The type of the column.|None|
|Name|String|Yes|No|The name of the column.|None|

## Response parameters

Fn::GetAtt

TableName: the name of the table.

## Examples

`JSON` format

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

`YAML` format

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


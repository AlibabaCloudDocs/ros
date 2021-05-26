# ALIYUN::OTS::SearchIndex

ALIYUN::OTS::SearchIndex is used to create a search index for a table. You can create multiple search indexes for a table.

## Syntax

```
{
  "Type": "ALIYUN::OTS::SearchIndex",
  "Properties": {
    "IndexName": String,
    "InstanceName": String,
    "TableName": String,
    "FieldSchemas": List,
    "IndexSort": Map,
    "IndexSetting": Map
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|IndexName|String|Yes|No|The name of the search index.|None|
|InstanceName|String|Yes|No|The name of the instance to which the table belongs.|None|
|TableName|String|Yes|No|The name of the table.|None|
|FieldSchemas|List|Yes|No|The structure of the field.|None|
|IndexSort|Map|No|No|The presorting settings of the index. By default, data is sorted by primary key.|Search indexes that contain NEST fields do not support IndexSort. For more information, see [IndexSort properties](#section_82g_t6r_sry). |
|IndexSetting|Map|No|No|The index settings.|For more information, see [IndexSetting properties](#section_7ua_ubr_g9f).|

## IndexSort syntax

```
"IndexSort": {
  "Sorters": List
}
```

## IndexSort properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Sorters|List|Yes|No|The presorting method for the index.|PrimaryKeySort and FieldSort are supported. For more information, see [t122106.dita\#concept\_yw3\_cck\_pgb](/intl.en-US/SDK Reference/Python SDK/Search Index/Sorting and pagination.md) and [Sorters properties](#section_lts_ul6_etm). |

## Sorters syntax

```
"Sorters": [
  {
    "FieldSort": Map,
    "PrimaryKeySort": Map,
    "ScoreSort": Map,
    "GeoDistanceSort": Map
  }
]
```

## Sorters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|FieldSort|Map|No|No|Specifies that data is sorted by field value.|For more information, see [FieldSort properties](#section_nie_q1d_soy).|
|PrimaryKeySort|Map|No|No|Specifies that data is sorted by primary key.|For more information, see [PrimaryKeySort properties](#section_291_el6_anp).|
|ScoreSort|Map|No|No|Specifies that the query result is sorted based on the BM25-based keyword relevance score. ScoreSort is applicable to scenarios such as full-text search.|You must set ScoreSort to sort the matched data by keyword relevance score. Otherwise, the matched data is sorted based on the IndexSort field value. For more information, see [ScoreSort properties](#section_jsp_0qc_6c4). |
|GeoDistanceSort|Map|No|No|Specifies that data is sorted by geographic distance.|For more information, see [GeoDistanceSort properties](#section_awf_ci4_y8c).|

## FieldSort syntax

```
"FieldSort": {
  "SortMode": String,
  "SortOrder": String,
  "FieldName": String
}
```

## FieldSort properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SortMode|String|No|No|The sorting method used when the field has multiple values.|None|
|SortOrder|String|No|No|The sorting order.|Default value: ASC. Valid values:-   ASC: the ascending order.
-   DESC: the descending order. |
|FieldName|String|Yes|No|The name of the field to be sorted.|None|

## PrimaryKeySort syntax

```
"PrimaryKeySort": {
  "SortOrder": String
}
```

## PrimaryKeySort properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SortOrder|String|No|No|The sorting order.|Default value: ASC. Valid values:-   ASC: the ascending order.
-   DESC: the descending order. |

## ScoreSort syntax

```
"ScoreSort": {
  "SortOrder": String
}
```

## ScoreSort properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SortOrder|String|No|No|The sorting order.|Default value: ASC. Valid values:-   ASC: the ascending order.
-   DESC: the descending order. |

## GeoDistanceSort syntax

```
"GeoDistanceSort": {
  "Points": List,
  "SortMode": String,
  "SortOrder": String,
  "FieldName": String
}
```

## GeoDistanceSort properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Points|List|Yes|No|The coordinates of the points that compose the polygon. You can specify a polygon by using multiple coordinates.|The format is `latitude,longitude`. Valid values of latitude: \[-90,+90\]. Valid values of longitude: \[-180,+180\]. Example: `35.8,-45.91`.|
|SortMode|String|No|No|The sorting method used when the field has multiple values.|None|
|SortOrder|String|No|No|The sorting order.|Default value: ASC. Valid values:-   ASC: the ascending order.
-   DESC: the descending order. |
|FieldName|String|Yes|No|The name of the field to be sorted.|None|

## IndexSetting syntax

```
"IndexSetting": {
  "RoutingFields": List
}
```

## IndexSetting properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RoutingFields|List|No|No|The custom routing fields.|You can specify some primary key columns as routing fields. Tablestore distributes data that is written to a search index to different partitions based on the specified routing fields. The data that has the same routing field value is distributed to the same data partition.|

## FieldSchemas syntax

```
"FieldSchemas": [
  {
    "Index": Boolean,
    "IsArray": Boolean,
    "Analyzer": String,
    "EnableSortAndAgg": Boolean,
    "Store": Boolean,
    "SubFieldSchemas": List,
    "FieldName": String,
    "FieldType": String
  }
]
```

## FieldSchemas properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Index|Boolean|No|No|Specifies whether to enable indexing.|Valid values:-   true
-   false |
|IsArray|Boolean|No|No|Specifies whether the value of the field is an array.|Valid values:-   true
-   false |
|Analyzer|String|No|No|The type of the analyzer.|If the field type is set to Text, you can set this parameter. Otherwise, the type of the analyzer is set to single-word tokenization by default. For more information, see [t288253.dita\#concept\_354503](/intl.en-US/Function Introduction/Search Index/Operations/Tokenization.md). |
|EnableSortAndAgg|Boolean|No|No|Specifies whether to enable the sorting and aggregation features.|None|
|Store|Boolean|No|No|Specifies whether to store the value of the field in the search index.|A value of true indicates that the value of the field is stored in the search index. You can read the value of the field directly from the search index without the need to query the table. This optimizes query performance.|
|SubFieldSchemas|List|No|No|The list of field schemas for subfields. If the field is a NEST field, you must specify this parameter to configure the index types of subfields in the NEST field.|None|
|FieldName|String|Yes|No|The name of the field in the search index, which is also called the column name.|A field in a search index can be a primary key column or an attribute column.|
|FieldType|String|Yes|No|The type of the field.|Use FieldType.XXX to set the type. For more information, see [Data types of column values](/intl.en-US/Function Introduction/Search Index/Operations/Overview.md). |

## SubFieldSchemas syntax

```
"SubFieldSchemas": [
  {
    "Index": Boolean,
    "IsArray": Boolean,
    "Analyzer": String,
    "EnableSortAndAgg": Boolean,
    "Store": Boolean,
    "FieldName": String,
    "FieldType": String
  }
]
```

## SubFieldSchemas properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Index|Boolean|No|No|Specifies whether to enable indexing.|None|
|IsArray|Boolean|No|No|Specifies whether the value of the field is an array.|None|
|Analyzer|String|No|No|The type of the analyzer.|If the field type is set to Text, you can set this parameter. Otherwise, the type of the analyzer is set to single-word tokenization by default. For more information, see [t288253.dita\#concept\_354503](/intl.en-US/Function Introduction/Search Index/Operations/Tokenization.md). |
|EnableSortAndAgg|Boolean|No|No|Specifies whether to enable the sorting and aggregation features.|Valid values:-   true
-   false |
|Store|Boolean|No|No|Specifies whether to store the value of the field in the search index.|Valid values:-   true
-   false

A value of true indicates that the value of the field is stored in the search index. You can read the value of the field directly from the search index without the need to query the table. This optimizes query performance.|
|FieldName|String|Yes|No|The name of the field in the search index, which is also called the column name.|A field in a search index can be a primary key column or an attribute column.|
|FieldType|String|Yes|No|The type of the field.|Use FieldType.XXX to set the type. For more information, see [Data types of column values](/intl.en-US/Function Introduction/Search Index/Operations/Overview.md). |

## Response parameters

Fn::GetAtt

IndexName: the name of the search index.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "IndexName": {
      "Type": "String",
      "Description": "The index name."
    },
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the OTS instance in which table will locate.",
      "AllowedPattern": "[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]"
    },
    "TableName": {
      "Type": "String",
      "Description": "The table name of the OTS instance.",
      "AllowedPattern": "[_a-zA-Z][_a-zA-Z0-9]{0,254}"
    },
    "FieldSchemas": {
      "Type": "Json",
      "Description": "list of field_schema."
    },
    "IndexSort": {
      "Type": "Json",
      "Description": "This parameter specifies how data is sorted. \nBy default, the data is sorted in the same way as the primary key of the table. \nIf the search index contains NESTED fields, data is not sorted by default."
    },
    "IndexSetting": {
      "Type": "Json",
      "Description": "Index settings"
    }
  },
  "Resources": {
    "SearchIndex": {
      "Type": "ALIYUN::OTS::SearchIndex",
      "Properties": {
        "IndexName": {
          "Ref": "IndexName"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "TableName": {
          "Ref": "TableName"
        },
        "FieldSchemas": {
          "Ref": "FieldSchemas"
        },
        "IndexSort": {
          "Ref": "IndexSort"
        },
        "IndexSetting": {
          "Ref": "IndexSetting"
        }
      }
    }
  },
  "Outputs": {
    "IndexName": {
      "Description": "Index name.",
      "Value": {
        "Fn::GetAtt": [
          "SearchIndex",
          "IndexName"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  IndexName:
    Type: String
    Description: The index name.
  InstanceName:
    Type: String
    Description: The name of the OTS instance in which table will locate.
    AllowedPattern: '[a-zA-Z][-a-zA-Z0-9]{1,14}[a-zA-Z0-9]'
  TableName:
    Type: String
    Description: The table name of the OTS instance.
    AllowedPattern: '[_a-zA-Z][_a-zA-Z0-9]{0,254}'
  FieldSchemas:
    Type: Json
    Description: list of field_schema.
  IndexSort:
    Type: Json
    Description: >-
      This parameter specifies how data is sorted. 

      By default, the data is sorted in the same way as the primary key of the
      table. 

      If the search index contains NESTED fields, data is not sorted by default.
  IndexSetting:
    Type: Json
    Description: Index settings
Resources:
  SearchIndex:
    Type: 'ALIYUN::OTS::SearchIndex'
    Properties:
      IndexName:
        Ref: IndexName
      InstanceName:
        Ref: InstanceName
      TableName:
        Ref: TableName
      FieldSchemas:
        Ref: FieldSchemas
      IndexSort:
        Ref: IndexSort
      IndexSetting:
        Ref: IndexSetting
Outputs:
  IndexName:
    Description: Index name.
    Value:
      'Fn::GetAtt':
        - SearchIndex
        - IndexName
```

For more examples, visit [OTS.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OTS/JSON/OTS.json) and [OTS.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OTS/YAML/OTS.yml). In the examples, the ALIYUN::OTS::Instance, ALIYUN::OTS::SearchIndex, ALIYUN::OTS::Table, and ALIYUN::OTS::VpcBinder resource types are involved.


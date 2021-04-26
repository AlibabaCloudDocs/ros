# ALIYUN::OTS::SearchIndex

ALIYUN::OTS::SearchIndex类型用于在数据表上创建一个多元索引。一个数据表可以创建多个多元索引。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IndexName|String|是|否|多元索引名称。|无|
|InstanceName|String|是|否|数据表所属的实例名称。|无|
|TableName|String|是|否|数据表名称。|无|
|FieldSchemas|List|是|否|字段结构。|无|
|IndexSort|Map|否|否|索引预排序设置。默认按照主键排序。|含有Nested类型的索引不支持IndexSort，没有预排序。更多信息，请参见[IndexSort属性](#section_82g_t6r_sry)。 |
|IndexSetting|Map|否|否|索引设置。|更多信息，请参见[IndexSetting属性](#section_7ua_ubr_g9f)。|

## IndexSort语法

```
"IndexSort": {
  "Sorters": List
}
```

## IndexSort属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Sorters|List|是|否|索引的预排序方式。|支持按照主键排序和字段值排序。更多信息，请参见[t122106.dita\#concept\_yw3\_cck\_pgb](/cn.zh-CN/SDK 参考/Python SDK/多元索引/排序和翻页.md)和[Sorters属性](#section_lts_ul6_etm)。 |

## Sorters语法

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

## Sorters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FieldSort|Map|否|否|按照字段值排序。|更多信息，请参见[FieldSort属性](#section_nie_q1d_soy)。|
|PrimaryKeySort|Map|否|否|按照主键排序。|更多信息，请参见[PrimaryKeySort属性](#section_291_el6_anp)。|
|ScoreSort|Map|否|否|按照查询结果的相关性（BM25算法）分数进行排序，适用于有相关性的场景，例如：全文检索等。|如果需要按照相关性打分进行排序，必须手动设置ScoreSort，否则会按照索引设置的IndexSort进行排序。更多信息，请参见[ScoreSort属性](#section_jsp_0qc_6c4)。 |
|GeoDistanceSort|Map|否|否|根据地理位置距离进行排序。|更多信息，请参见[GeoDistanceSort属性](#section_awf_ci4_y8c)。|

## FieldSort语法

```
"FieldSort": {
  "SortMode": String,
  "SortOrder": String,
  "FieldName": String
}
```

## FieldSort属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SortMode|String|否|否|当字段存在多个值时的排序方式。|无|
|SortOrder|String|否|否|排序的顺序。|取值：-   升序（默认值）：ASC。
-   降序：DESC。 |
|FieldName|String|是|否|排序的字段名。|无|

## PrimaryKeySort语法

```
"PrimaryKeySort": {
  "SortOrder": String
}
```

## PrimaryKeySort属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SortOrder|String|否|否|排序的顺序。|取值：-   升序（默认值）：ASC。
-   降序：DESC。 |

## ScoreSort语法

```
"ScoreSort": {
  "SortOrder": String
}
```

## ScoreSort属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SortOrder|String|否|否|排序顺序。|取值：-   升序（默认值）：ASC。
-   降序：DESC。 |

## GeoDistanceSort语法

```
"GeoDistanceSort": {
  "Points": List,
  "SortMode": String,
  "SortOrder": String,
  "FieldName": String
}
```

## GeoDistanceSort属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Points|List|是|否|组成多边形范围的坐标，通过多个坐标可以确定一个唯一的多边形。|格式为`纬度,经度`，纬度在前，经度在后，且纬度范围为\[-90,+90\]，经度范围\[-180,+180\]。例如：`35.8,-45.91`。|
|SortMode|String|否|否|当字段存在多个值时的排序方式。|无|
|SortOrder|String|否|否|排序顺序。|取值：-   升序（默认值）：ASC。
-   降序：DESC。 |
|FieldName|String|是|否|排序的字段名。|无|

## IndexSetting语法

```
"IndexSetting": {
  "RoutingFields": List
}
```

## IndexSetting属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RoutingFields|List|否|否|自定义路由字段。|您可以选择部分主键列作为路由字段，在进行索引数据写入时，会根据路由字段的值计算索引数据的分布位置，路由字段的值相同的记录会被索引到相同的数据分区中。|

## FieldSchemas语法

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

## FieldSchemas属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Index|Boolean|否|否|是否开启索引。|取值：-   true
-   false |
|IsArray|Boolean|否|否|是否为数组。|取值：-   true
-   false |
|Analyzer|String|否|否|分词器类型。|当字段类型为Text时，可以设置此参数；否则，则默认分词器类型为单字分词。更多信息，请参见[t288253.dita\#concept\_354503](/cn.zh-CN/功能介绍/多元索引/使用/分词.md)。 |
|EnableSortAndAgg|Boolean|否|否|是否开启排序与统计聚合功能。|无|
|Store|Boolean|否|否|是否在多元索引中附加存储该字段的值。|开启后，可以直接从多元索引中读取该字段的值，而不必反查数据表，可用于查询性能优化。|
|SubFieldSchemas|List|否|否|当字段类型为Nested类型时，需要通过此参数设置嵌套文档中子列的索引类型。|无|
|FieldName|String|是|否|创建多元索引的字段名，即列名。|多元索引中的字段可以是主键列或者属性列。|
|FieldType|String|是|否|字段类型。|取值为为FieldType.XXX。更多信息，请参见[字段](/cn.zh-CN/功能介绍/多元索引/使用/概述.md)。 |

## SubFieldSchemas语法

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

## SubFieldSchemas属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Index|Boolean|否|否|是否开启索引。|无|
|IsArray|Boolean|否|否|是否为数组。|无|
|Analyzer|String|否|否|分词器类型。|当字段类型为Text时，可以设置此参数；否则，则默认分词器类型为单字分词。更多信息，请参见[t288253.dita\#concept\_354503](/cn.zh-CN/功能介绍/多元索引/使用/分词.md)。 |
|EnableSortAndAgg|Boolean|否|否|是否开启排序与统计聚合功能。|取值：-   true
-   false |
|Store|Boolean|否|否|是否在多元索引中附加存储该字段的值。|取值：-   true
-   false

开启后，可以直接从多元索引中读取该字段的值，而不必反查数据表，可用于查询性能优化。|
|FieldName|String|是|否|创建多元索引的字段名，即列名。|多元索引中的字段可以是主键列或者属性列。|
|FieldType|String|是|否|字段类型。|取值为为FieldType.XXX。更多信息，请参见[字段](/cn.zh-CN/功能介绍/多元索引/使用/概述.md)。 |

## 返回值

Fn::GetAtt

IndexName：多元索引名称。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建表格存储实例、在数据表上创建一个多元索引、创建表和将表格存储实例绑定VPC的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OTS/JSON/OTS.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OTS/YAML/OTS.yml)。


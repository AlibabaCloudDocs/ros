# ALIYUN::SLS::Index

ALIYUN::SLS::Index is used to create an index for a specified Logstore.

## Syntax

```
{
  "Type": "ALIYUN::SLS::Index",
  "Properties": {
    "ProjectName": String,
    "FullTextIndex": Map,
    "LogstoreName": String,
    "KeyIndices": List,
    "LogReduce": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ProjectName|String|Yes|No|The name of the Log Service project.|The name must be 3 to 36 characters in length and can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\). It must start with a lowercase letter or digit.|
|FullTextIndex|Map|Yes|Yes|The full-text index configurations.|For more information, see [FullTextIndex properties](#section_i6q_ofb_6dk).|
|LogstoreName|String|Yes|No|The name of the Logstore.|None|
|KeyIndices|List|No|Yes|The field index configurations.|You must specify at least one of the FullTextIndex and KeyIndices parameters. For more information, see [Properties](#section_1zx_gy0_w02). |
|LogReduce|Boolean|No|Yes|Specifies whether to enable LogReduce.|Default value: false. Valid values: -   true
-   false |

## FullTextIndex syntax

```
"FullTextIndex": {
  "CaseSensitive": Boolean,
  "Delimiter": String,
  "IncludeChinese": Boolean,
  "Enable": Boolean
}
```

## FullTextIndex properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Enable|Boolean|Yes|Yes|Specifies whether to enable full-text indexing.|Default value: true. Valid values: -   true
-   false |
|CaseSensitive|Boolean|No|Yes|Specifies whether the field is case-sensitive.|Default value: false. Valid values: -   true
-   false |
|Delimiter|String|No|Yes|The delimiter that is used to separate keywords.|Valid values:```
,'";=()[]{}? @&<>/:\n\t\r
``` |
|IncludeChinese|Boolean|No|Yes|Specifies whether to support Chinese word segmentation.|Default value: false. Valid values: -   true
-   false |

## KeyIndices syntax

```
"KeyIndices": [
  {
    "Name": String,
    "EnableAnalytics": Boolean,
    "Delimiter": String,
    "CaseSensitive": Boolean,
    "JsonKeyIndices": List,
    "Alias": String,
    "IncludeChinese": String,
    "Type": String
  }
]
```

## KeyIndices properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|Yes|Yes|The name of the field.|You can use a nested name that is separated with periods \(.\). Example: k1.k2.k3.|
|EnableAnalytics|Boolean|No|Yes|Specifies whether to enable statistical analysis on the field.|Default value: true. Valid values: -   true
-   false |
|Delimiter|String|No|Yes|The delimiter that is used to separate keywords.|Valid values:```
,'";=()[]{}? @&<>/:\n\t\r
``` |
|CaseSensitive|Boolean|No|Yes|Specifies whether the field is case-sensitive.|Default value: false. Valid values: -   true
-   false

This parameter takes effect only when the Type parameter is set to text or json.|
|JsonKeyIndices|List|No|Yes|The JSON index configurations. Format: `[{"key1": "value1", "key2": "value2", ...}]`.|Supported keys are Name, Alias, Type, and EnableAnalytics. For more information, see [JsonKeyIndices properties](#section_y1e_mtq_3xd). |
|Alias|String|No|Yes|The alias of the field.|None|
|IncludeChinese|Boolean|No|Yes|Specifies whether to support Chinese word segmentation.|Default value: false. Valid values: -   true
-   false

This parameter takes effect only when the Type parameter is set to text.|
|Type|String|Yes|Yes|The type of the field.|Default value: text. Valid values: -   text
-   long
-   double
-   json |

## JsonKeyIndices syntax

```
"JsonKeyIndices": [
  {
    "Type": String,
    "Alias": String,
    "EnableAnalytics": Boolean,
    "Name": String
  }
]  
```

## JsonKeyIndices properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|Yes|Yes|The name of the field.|None|
|EnableAnalytics|Boolean|No|Yes|Specifies whether to enable statistical analysis on the field.|Valid values: -   true
-   false |
|Alias|String|No|Yes|The alias of the field.|None|
|Type|String|Yes|Yes|The type of the field.|None|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Index": {
      "Type": "ALIYUN::SLS::Index",
      "Properties": {
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "FullTextIndex": {
          "Ref": "FullTextIndex"
        },
        "LogstoreName": {
          "Ref": "LogstoreName"
        },
        "KeyIndices": {
          "Ref": "KeyIndices"
        },
        "LogReduce": {
          "Ref": "LogReduce"
        }
      }
    }
  },
  "Parameters": {
    "ProjectName": {
      "Type": "String",
      "Description": "Project name:1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3. The name length is 3-63 characters.",
      "MinLength": 3,
      "MaxLength": 63
    },
    "FullTextIndex": {
      "Type": "Map",
      "Description": "Full-text indexing configuration.Full-text indexing and key indexing must have at least one enabled."
    },
    "LogstoreName": {
      "Type": "String",
      "Description": "Logstore name:1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3. The name length is 3-63 characters.",
      "MinLength": 3,
      "MaxLength": 63
    },
    "KeyIndices": {
      "Type": "List",
      "Description": "Key index configurations.Full-text indexing and key indexing must have at least one enabled."
    },
    "LogReduce": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to enable log reduce. Default to false.",
      "AllowedValues": [
        true,
        false
      ]
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Index:
    Type: ALIYUN::SLS::Index
    Properties:
      ProjectName:
        Ref: ProjectName
      FullTextIndex:
        Ref: FullTextIndex
      LogstoreName:
        Ref: LogstoreName
      KeyIndices:
        Ref: KeyIndices
      LogReduce:
        Ref: LogReduce
Parameters:
  ProjectName:
    MinLength: 3
    MaxLength: 63
    Type: String
    Description: Project name:1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3.
      The name length is 3-63 characters.
  FullTextIndex:
    Type: Map
    Description: Full-text indexing configuration.Full-text indexing and key indexing
      must have at least one enabled.
  LogstoreName:
    MinLength: 3
    MaxLength: 63
    Type: String
    Description: Logstore name:1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3.
      The name length is 3-63 characters.
  KeyIndices:
    Type: List
    Description: Key index configurations.Full-text indexing and key indexing must
      have at least one enabled.
  LogReduce:
    Default: false
    Type: Boolean
    Description: Whether to enable log reduce. Default to false.
    AllowedValues:
    - true
    - false
            
```


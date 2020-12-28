# ALIYUN::OOS::Parameter

ALIYUN::OOS::Parameter类型用于创建一个普通参数。

## 语法

```
{
  "Type": "ALIYUN::OOS::Parameter",
  "Properties": {
    "Type": String,
    "Constraints": String,
    "Description": String,
    "Value": String,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|否|参数类型。|取值：-   String
-   StringList |
|Constraints|String|否|否|参数的约束条件。|取值：-   AllowedValues：参数允许值。支持数组类型的字符串。
-   AllowedPattern：正则表达式。
-   MinLength：参数最小长度。
-   MaxLength：参数最大长度。 |
|Description|String|否|是|参数的描述信息。|长度不超过200个字符。|
|Value|String|是|是|参数值。|长度不超过4096个字符。|
|Name|String|是|否|参数名称。|长度不超过200个字符。不能以`ALIYUN`、`ACS`、`ALIBABA`、`ALICLOUD`、`OOS`开头，可包含英文字母、数字、短划线（-）和下划线（\_）。|

## 返回值

Fn::GetAtt

-   Name：参数名称。
-   Value：参数值。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Type": {
      "Type": "String",
      "Description": "The data type of the common parameter. \nValid values: String and StringList.",
      "AllowedValues": [
        "String",
        "StringList"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the parameter. \nThe description must be 1 to 200 characters in length."
    },
    "Constraints": {
      "Type": "String",
      "Description": "The constraints of the parameter. \nBy default, this parameter is null. Valid values:\nAllowedValues: The value that is allowed for the parameter. It must be an array string.\nAllowedPattern: The pattern that is allowed for the parameter. It must be a regular expression.\nMinLength: The minimum length of the parameter.\nMaxLength: The maximum length of the parameter."
    },
    "Value": {
      "Type": "String",
      "Description": "The value of the parameter. \nThe value must be 1 to 4096 characters in length."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the parameter. \nThe name must be 1 to 200 characters in length,and can contain letters, digits, hyphens (-), and underscores (_). \nIt cannot start with ALIYUN, ACS, ALIBABA, ALICLOUD, or OOS."
    }
  },
  "Resources": {
    "Parameter": {
      "Type": "ALIYUN::OOS::Parameter",
      "Properties": {
        "Type": {
          "Ref": "Type"
        },
        "Description": {
          "Ref": "Description"
        },
        "Constraints": {
          "Ref": "Constraints"
        },
        "Value": {
          "Ref": "Value"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "Value": {
      "Description": "The Value of the parameter.",
      "Value": {
        "Fn::GetAtt": [
          "Parameter",
          "Value"
        ]
      }
    },
    "Name": {
      "Description": "The Name of the parameter.",
      "Value": {
        "Fn::GetAtt": [
          "Parameter",
          "Name"
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
  Type:
    Type: String
    Description: |-
      The data type of the common parameter. 
      Valid values: String and StringList.
    AllowedValues:
      - String
      - StringList
  Description:
    Type: String
    Description: |-
      The description of the parameter. 
      The description must be 1 to 200 characters in length.
  Constraints:
    Type: String
    Description: >-
      The constraints of the parameter. 

      By default, this parameter is null. Valid values:

      AllowedValues: The value that is allowed for the parameter. It must be an
      array string.

      AllowedPattern: The pattern that is allowed for the parameter. It must be
      a regular expression.

      MinLength: The minimum length of the parameter.

      MaxLength: The maximum length of the parameter.
  Value:
    Type: String
    Description: |-
      The value of the parameter. 
      The value must be 1 to 4096 characters in length.
  Name:
    Type: String
    Description: >-
      The name of the parameter. 

      The name must be 1 to 200 characters in length,and can contain letters,
      digits, hyphens (-), and underscores (_). 

      It cannot start with ALIYUN, ACS, ALIBABA, ALICLOUD, or OOS.
Resources:
  Parameter:
    Type: 'ALIYUN::OOS::Parameter'
    Properties:
      Type:
        Ref: Type
      Description:
        Ref: Description
      Constraints:
        Ref: Constraints
      Value:
        Ref: Value
      Name:
        Ref: Name
Outputs:
  Value:
    Description: The Value of the parameter.
    Value:
      'Fn::GetAtt':
        - Parameter
        - Value
  Name:
    Description: The Name of the parameter.
    Value:
      'Fn::GetAtt':
        - Parameter
        - Name
```


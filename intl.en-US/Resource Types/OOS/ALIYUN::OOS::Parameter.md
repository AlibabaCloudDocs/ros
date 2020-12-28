# ALIYUN::OOS::Parameter

ALIYUN::OOS::Parameter is used to create a common parameter.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|Yes|No|The data type of the parameter.|Valid values:-   String
-   StringList |
|Constraints|String|No|No|The constraints of the parameter.|Valid values:-   AllowedValues: the valid values of the parameter. This value can be a string in the array format.
-   AllowedPattern: the regular expression of the parameter.
-   MinLength: the minimum length of the parameter.
-   MaxLength: the maximum length of the parameter. |
|Description|String|No|Yes|The description of the parameter.|The description can be up to 200 characters in length.|
|Value|String|Yes|Yes|The parameter value.|The parameter value can be up to 4,096 characters in length.|
|Name|String|Yes|No|The name of the parameter.|The name can be up to 200 characters in length. It cannot start with `ALIYUN`, `ACS`, `ALIBABA`, `ALICLOUD`, or `OOS`. It can contain letters, digits, hyphens \(-\), and underscores \(\_\).|

## Response parameters

Fn::GetAtt

-   Name: the name of the parameter.
-   Value: the value of the parameter.

## Examples

`JSON` format

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

`YAML` format

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


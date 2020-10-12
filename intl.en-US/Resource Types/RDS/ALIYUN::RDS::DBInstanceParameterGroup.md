# ALIYUN::RDS::DBInstanceParameterGroup

ALIYUN::RDS::DBInstanceParameterGroup is used to modify parameters of an ApsaraDB for RDS instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DBInstanceId|String|Yes|No|The ID of the ApsaraDB for RDS instance.|None|
|Parameters|List|Yes|No|The parameters of the instance.|For more information, see [Parameters properties](#section_nvv_kg2_29b).|
|Forcerestart|String|No|No|Specifies whether to forcibly restart the instance.|Default value: false. Valid values: -   true: The system forcibly restarts the instance.
-   false: The system does not forcibly restart the instance. |

## Parameters syntax

```
"Parameters": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Parameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The name of the parameter.|None|
|Value|String|Yes|No|The value of the parameter.|None|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

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

`YAML` format

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


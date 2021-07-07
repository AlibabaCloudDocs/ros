# ALIYUN::SLS::Etl

ALIYUN::SLS::Etl is used to create a data transformation task.

## Syntax

```
{
  "Type": "ALIYUN::SLS::Etl",
  "Properties": {
    "Description": String,
    "Configuration": Map,
    "ProjectName": String,
    "Schedule": Map,
    "DisplayName": String,
    "Name": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the task.|None|
|Configuration|Map|Yes|No|The configurations of the task.|For more information, see [Configuration properties](#section_ksg_wmp_lnm).|
|ProjectName|String|Yes|No|The name of the destination Log Service project of the task.|None|
|Schedule|Map|Yes|No|The scheduling policy of the task.|For more information, see [Schedule properties](#section_kxq_s74_ep3).|
|DisplayName|String|Yes|No|The display name of the task.|None|
|Name|String|Yes|No|The name of the task.|None|

## Configuration syntax

```
"Configuration": {
  "Script": String,
  "Sinks": List,
  "Parameters": Map,
  "ToTime": Number,
  "Version": Number,
  "Logstore": String,
  "FromTime": Number,
  "RoleArn": String
}
```

## Configuration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Script|String|Yes|No|The syntax of the task.|None|
|Sinks|List|Yes|No|The storage destination configurations of the task.|Storage destinations include Log Service projects and Logstores. For more information, see [Sinks properties](#section_8sd_ct0_9n0). |
|Parameters|Map|No|No|The configurations of advanced parameters of the task.|None|
|ToTime|Number|No|No|The time when the task ends.|Default value: None.|
|Version|Number|No|No|The script version of the task.|None|
|Logstore|String|Yes|No|The source Logstore of the task.|None|
|FromTime|Number|No|No|The time when the task starts.|The default start time is the current time.|
|RoleArn|String|No|No|The Alibaba Cloud Resource Name \(ARN\) of the role that the user must assume by using Security Token Service \(STS\) to access the destination Logstore of the task.|None|

## Sinks syntax

```
"Sinks": [
  {
    "Project": String,
    "Type": String,
    "Endpoint": String,
    "Logstore": String,
    "RoleArn": String,
    "Name": String
  }
]
```

## Sinks properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Project|String|Yes|No|The destination Log Service project of the task.|None|
|Type|String|No|No|The storage destination type of the task.|Storage destinations include Log Service projects and Logstores. Default value: AliyunLOG. |
|Endpoint|String|No|No|The endpoint of the server to which the destination Log Service project of the task belongs.|None|
|Logstore|String|Yes|No|The destination Logstore of the task.|None|
|RoleArn|String|No|No|The ARN of the role that the user must assume by using STS to access the destination Logstore of the task.|None|
|Name|String|Yes|No|The storage destination name of the task.|Storage destinations include Log Service projects and Logstores.|

## Schedule syntax

```
"Schedule": {
  "Type": String
}
```

## Schedule properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Type|String|Yes|No|The scheduling policy type of the task.|Set the value to Resident.|

## Response parameters

Fn::GetAtt

Name: the name of the task.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "ETL description message."
    },
    "Configuration": {
      "Type": "Json",
      "Description": "The configuration of ETL task"
    },
    "ProjectName": {
      "Type": "String",
      "Description": "Project name"
    },
    "Schedule": {
      "Type": "Json",
      "Description": "Task scheduling strategy"
    },
    "DisplayName": {
      "Type": "String",
      "Description": "ETL display name"
    },
    "Name": {
      "Type": "String",
      "Description": "ETL name"
    }
  },
  "Resources": {
    "Etl": {
      "Type": "ALIYUN::SLS::Etl",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "Configuration": {
          "Ref": "Configuration"
        },
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "Schedule": {
          "Ref": "Schedule"
        },
        "DisplayName": {
          "Ref": "DisplayName"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "Name": {
      "Description": "ETL name.",
      "Value": {
        "Fn::GetAtt": [
          "Etl",
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
  Configuration:
    Description: The configuration of ETL task
    Type: Json
  Description:
    Description: ETL description message.
    Type: String
  DisplayName:
    Description: ETL display name
    Type: String
  Name:
    Description: ETL name
    Type: String
  ProjectName:
    Description: Project name
    Type: String
  Schedule:
    Description: Task scheduling strategy
    Type: Json
Resources:
  Etl:
    Properties:
      Configuration:
        Ref: Configuration
      Description:
        Ref: Description
      DisplayName:
        Ref: DisplayName
      Name:
        Ref: Name
      ProjectName:
        Ref: ProjectName
      Schedule:
        Ref: Schedule
    Type: ALIYUN::SLS::Etl
Outputs:
  Name:
    Description: ETL name.
    Value:
      Fn::GetAtt:
      - Etl
      - Name
```


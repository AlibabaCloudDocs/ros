# ALIYUN::SLS::Etl

ALIYUN::SLS::Etl类型用于创建数据加工任务。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|数据加工任务的描述。|无|
|Configuration|Map|是|否|数据加工任务的配置。|更多信息，请参见[Configuration属性](#section_ksg_wmp_lnm)。|
|ProjectName|String|是|否|数据加工任务的目标日志项目名称。|无|
|Schedule|Map|是|否|数据加工任务的调度策略。|更多信息，请参见[Schedule属性](#section_kxq_s74_ep3)。|
|DisplayName|String|是|否|数据加工任务的显示名称。|无|
|Name|String|是|否|数据加工任务的名称。|无|

## Configuration语法

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

## Configuration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Script|String|是|否|数据加工任务的语法。|无|
|Sinks|List|是|否|数据加工任务的存储目标配置。|存储目标包括日志项目、日志库等。更多信息，请参见[Sinks属性](#section_8sd_ct0_9n0)。 |
|Parameters|Map|否|否|数据加工任务的高级参数配置。|无|
|ToTime|Number|否|否|数据加工任务的结束时间。|默认值：None。|
|Version|Number|否|否|数据加工任务的脚本版本。|无|
|Logstore|String|是|否|数据加工任务的日志库（源日志库）。|无|
|FromTime|Number|否|否|数据加工任务的开始时间。|默认从当前时间开始。|
|RoleArn|String|否|否|数据加工任务的目标日志库中的STS角色信息。|无|

## Sinks语法

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

## Sinks属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|是|否|数据加工任务的目标日志项目。|无|
|Type|String|否|否|数据加工任务的存储目标类型。|存储目标包括日志项目、日志库等。默认值：AliyunLOG。 |
|Endpoint|String|否|否|数据加工任务的目标日志项目所在的服务端地址。|无|
|Logstore|String|是|否|数据加工任务的目标日志库。|无|
|RoleArn|String|否|否|数据加工任务的目标日志库中的STS角色信息。|无|
|Name|String|是|否|数据加工任务的存储目标名称。|存储目标包括日志项目、日志库等。|

## Schedule语法

```
"Schedule": {
  "Type": String
}
```

## Schedule属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|否|数据加工任务的调度策略类型。|取值：Resident。|

## 返回值

Fn::GetAtt

Name：数据加工任务名称。

## 示例

`JSON`格式

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

`YAML`格式

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


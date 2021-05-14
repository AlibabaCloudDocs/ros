# ALIYUN::VPC::FlowLog

ALIYUN::VPC::FlowLog类型用于创建流日志。

## 语法

```
{
  "Type": "ALIYUN::VPC::FlowLog",
  "Properties": {
    "FlowLogName": String,
    "Description": String,
    "LogStoreName": String,
    "ResourceId": String,
    "ProjectName": String,
    "ResourceType": String,
    "TrafficType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FlowLogName|String|否|是|流日志名称。|长度为2~128个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|
|Description|String|否|是|流日志的描述。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|LogStoreName|String|是|否|存储捕获到的流量的日志库名称。|无|
|ResourceId|String|是|否|要捕获流量的资源ID。|资源ID可以为专有网络、交换机、弹性网卡实例ID。如果专有网络含有以下ECS实例规格组中的任一实例，则不支持为该资源创建流日志：ecs.c1、ecs.c2、ecs.c4、ecs.c5、ecs.ce4、ecs.cm4、ecs.d1、ecs.e3、ecs.e4、ecs.ga1、ecs.gn4、ecs.gn5、ecs.i1、ecs.m1、ecs.m2、ecs.mn4、ecs.n1、ecs.n2、ecs.n4、ecs.s1、ecs.s2、ecs.s3、ecs.se1、ecs.sn1、ecs.sn2、ecs.t1、ecs.xn4。

如需创建流日志，请先升级实例规格。更多信息，请参见[包年包月实例升配规格](/intl.zh-CN/实例/升降配实例/修改实例规格/包年包月实例升配规格.md)和[按量付费实例变配规格](/intl.zh-CN/实例/升降配实例/修改实例规格/按量付费实例变配规格.md)。**说明：** 如果您的专有网络中含有ECS实例规格族限制中的任一实例，且您已经创建了流日志，为了保证正常使用流日志功能，请升级实例规格。 |
|ProjectName|String|是|否|存储捕获到的流量的日志项目名称。|无|
|ResourceType|String|是|否|要捕获流量的资源类型。|取值：-   NetworkInterface：全部弹性网卡。
-   VSwitch：交换机内的全部弹性网卡。
-   VPC：专有网络内的全部弹性网卡。 |
|TrafficType|String|是|否|采集的流量类型。|取值：-   All：全部流量。
-   Allow：访问控制允许的流量。
-   Drop：访问控制拒绝的流量。 |

## 返回值

Fn::GetAtt

-   FlowLogName：流日志名称。
-   Description：流日志描述。
-   LogStoreName：日志库名称。
-   ResourceId：资源ID。
-   ProjectName：日志项目名称。
-   ResourceType：资源类型。
-   FlowLogId：流日志ID。
-   TrafficType：流量类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "FlowLogName": {
      "Type": "String",
      "Description": "The flow log name."
    },
    "Description": {
      "Type": "String",
      "Description": "The Description of flow log."
    },
    "LogStoreName": {
      "Type": "String",
      "Description": "The log store name."
    },
    "ResourceId": {
      "Type": "String",
      "Description": "The resource id."
    },
    "ProjectName": {
      "Type": "String",
      "Description": "The project name."
    },
    "ResourceType": {
      "Type": "String",
      "Description": "The resource type."
    },
    "TrafficType": {
      "Type": "String",
      "Description": "The traffic type."
    }
  },
  "Resources": {
    "VPCFlowLog": {
      "Type": "ALIYUN::VPC::FlowLog",
      "Properties": {
        "FlowLogName": {
          "Ref": "FlowLogName"
        },
        "Description": {
          "Ref": "Description"
        },
        "LogStoreName": {
          "Ref": "LogStoreName"
        },
        "ResourceId": {
          "Ref": "ResourceId"
        },
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "ResourceType": {
          "Ref": "ResourceType"
        },
        "TrafficType": {
          "Ref": "TrafficType"
        }
      }
    }
  },
  "Outputs": {
    "FlowLogName": {
      "Description": "The flow log name.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "FlowLogName"
        ]
      }
    },
    "Description": {
      "Description": "The Description of flow log.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "Description"
        ]
      }
    },
    "LogStoreName": {
      "Description": "The log store name.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "LogStoreName"
        ]
      }
    },
    "ResourceId": {
      "Description": "The resource id.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "ResourceId"
        ]
      }
    },
    "ProjectName": {
      "Description": "The project name.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "ProjectName"
        ]
      }
    },
    "ResourceType": {
      "Description": "The resource type.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "ResourceType"
        ]
      }
    },
    "FlowLogId": {
      "Description": "The flow log ID.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "FlowLogId"
        ]
      }
    },
    "TrafficType": {
      "Description": "The traffic type.",
      "Value": {
        "Fn::GetAtt": [
          "VPCFlowLog",
          "TrafficType"
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
  Description:
    Description: The Description of flow log.
    Type: String
  FlowLogName:
    Description: The flow log name.
    Type: String
  LogStoreName:
    Description: The log store name.
    Type: String
  ProjectName:
    Description: The project name.
    Type: String
  ResourceId:
    Description: The resource id.
    Type: String
  ResourceType:
    Description: The resource type.
    Type: String
  TrafficType:
    Description: The traffic type.
    Type: String
Resources:
  VPCFlowLog:
    Properties:
      Description:
        Ref: Description
      FlowLogName:
        Ref: FlowLogName
      LogStoreName:
        Ref: LogStoreName
      ProjectName:
        Ref: ProjectName
      ResourceId:
        Ref: ResourceId
      ResourceType:
        Ref: ResourceType
      TrafficType:
        Ref: TrafficType
    Type: ALIYUN::VPC::FlowLog
Outputs:
  Description:
    Description: The Description of flow log.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - Description
  FlowLogId:
    Description: The flow log ID.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - FlowLogId
  FlowLogName:
    Description: The flow log name.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - FlowLogName
  LogStoreName:
    Description: The log store name.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - LogStoreName
  ProjectName:
    Description: The project name.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - ProjectName
  ResourceId:
    Description: The resource id.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - ResourceId
  ResourceType:
    Description: The resource type.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - ResourceType
  TrafficType:
    Description: The traffic type.
    Value:
      Fn::GetAtt:
      - VPCFlowLog
      - TrafficType
```


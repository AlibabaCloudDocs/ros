# ALIYUN::FC::Trigger

ALIYUN::FC::Trigger类型用于触发函数执行的方式。

在事件驱动的计算模型中，事件源是事件的生产者，函数是事件的处理者，而触发器提供了一种集中和统一的方式来管理不同的事件源。在事件源中，当事件发生时，如果满足触发器定义的规则，事件源将调用触发器所对应的函数。

## 语法

```
{
  "Type": "ALIYUN::FC::Trigger",
  "Properties": {
    "TriggerConfig": Map,
    "InvocationRole": String,
    "FunctionName": String,
    "ServiceName": String,
    "TriggerName": String,
    "TriggerType": String,
    "Qualifier": String,
    "SourceArn": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceName|String|是|否|函数服务名称。|长度为1~128个字符。|
|FunctionName|String|是|否|要创建触发器的函数名称。|无|
|TriggerName|String|是|否|触发器名称。|长度为1~128个字符。以英文字母或下划线（\_）开头，可包含数字、英文字母、短划线（-）和下划线（\_）。|
|TriggerType|String|是|否|触发器类型。|取值： -   oss：OSS触发器。
-   log：日志服务触发器。
-   tablestore：Tablestore触发器。
-   timer：定时触发器。
-   mns\_topic：MNS主题触发器。
-   cdn\_events：CDN事件触发器。
-   http：HTTP触发器。

**说明：** HTTP触发器只能在创建函数时创建，且不能与其他类型的触发器同时存在。 |
|TriggerConfig|Map|是|是|触发器配置。|针对不同的触发器类型，触发器配置会有所不同。|
|InvocationRole|String|否|是|触发器角色，该角色授予事件源代表用户运行函数的权限。例如：`"acs:ram::1234567890:role/fc-test"`。|定时触发器和HTTP触发器无需指定该参数，其它类型触发器必须指定该参数。 不同类型触发器角色授权的可信实体及策略如下：

-   oss
    -   可信实体：阿里云服务oss.aliyuncs.com
    -   策略：Action：fc:InvokeFunction
-   log
    -   可信实体：阿里云服务log.aliyuncs.com
    -   策略：Action：log:PostLogStoreLogs
-   ots
    -   可信实体：阿里云账号1604337383174\*\*\*\*
    -   策略：Action：fc:InvokeFunction、ots:BatchGet\*、ots:Describe\*、ots:Get\*、ots:List\*
-   mns
    -   可信实体：阿里云服务mns.aliyuncs.com
    -   策略：Action：dm:BatchSendMail、dm:SingleSendMail、dm:Query
-   cdn
    -   可信实体：阿里云服务cdn.aliyuncs.com
    -   策略：Action：fc:InvokeFunction |
|SourceArn|String|否|否|事件源ARN。|定时触发器和HTTP触发器不指定该参数，其它类型触发器必须指定该参数。 不同触发器的事件源ARN格式及示例值如下：

-   oss
    -   格式：`acs:oss:<RegionId>:<TenantId>:<OssBucketName>`
    -   示例值：`acs:oss:cn-hangzhou:12345****:test-trigger-bucket`
-   log
    -   格式：`acs:log:<RegionId>:<TenantId>:project/<LogConfig属性中Project的值>`
    -   示例值：`acs:log:cn-hangzhou:12345****:project/logtrigger`
-   ots
    -   格式：`acs:ots:<RegionId>:<TenantId>:instance/<OtsInstance>/table/<OtsTable>`
    -   示例值：`acs:ots:cn-hangzhou:12345****:instance/otstrigger/table/tb`
-   mns
    -   格式：`acs:mns:<RegionId>:<TenantId>:/topics/<MnsTopic>`
    -   示例值：`acs:mns:cn-hangzhou:12345****:/topics/triggertopic`
-   cdn
    -   格式：`acs:cdn:*:<TenantId>`
    -   示例值：`acs:cdn:*:123456789`

**说明：** `TenantId`为阿里云主账号ID。 |
|Qualifier|String|否|是|触发版本。|默认值：LATEST。|

## oss-TriggerConfig语法

```
"TriggerConfig": {
  "BucketName": String,
  "Events": List,
  "Filter": Map
}      
```

## oss-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|BucketName|String|是|否|Bucket名称。|请在对象存储服务Object Storage Service（OSS）选择合适的Bucket作为事件源。选择框将展示同一个地域的Bucket。|
|Events|String|是|是|触发事件，表示您对阿里云资源执行的操作。|示例值：`oss:ObjectCreated:*`。|
|Filter|Map|否|是|触发规则，用于避免循环触发。|Prefix和Suffix的取值为自定义字符串。 示例：

```
"Filter": {
  "Key": {
    "Prefix": "prefix",
    "Suffix": "suffix"
  }
}
``` |

## log-TriggerConfig语法

```
"TriggerConfig": {
  "SourceConfig": Map,
  "LogConfig": Map,
  "JobConfig": Map,
  "FunctionParameter": Map,
  "Enable": Boolean
}
```

## log-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SourceConfig|Map|是|否|配置日志仓库。|示例值：`{"LogStore": "<SLS_LogStore>"}`。|
|LogConfig|Map|是|是|配置日志项目和触发器日志。|日志项目必须指定且不可更新。触发器日志不强制指定，可以更新，且不能与SourceConfig设置的LogStore相同。

示例值：`{"Project": "<SLS_Project>", "LogStore": "SLS_LogStore"}`。|
|JobConfig|Map|是|是|工作配置，用于设置重试次数和触发间隔。|触发间隔单位：秒。

重试次数取值范围：0~100。

示例值：`{"MaxRetryTime": 3, "TriggerInterval": 60}`。 |
|FunctionParameter|Map|是|是|函数配置，用于为函数传递参数。|不指定任何参数时请填写大括号（\{ \}）。|
|Enable|Boolean|是|是|日志服务触发器启用状态。|取值： -   true
-   false |

## timer-TriggerConfig语法

```
"TriggerConfig": {
  "Payload": String,
  "CronExpression": String,
  "Enabled": Boolean
}
```

## timer-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Payload|String|否|是|触发消息。|无|
|CronExpression|String|是|是|Cron表达式，用于设置触发时间。|Cron以UTC时间运行，即北京时间减去8个小时。更多信息，请参见[CronExpression](https://help.aliyun.com/document_detail/68172.html#h3-cronexpression-)。 |
|Enabled|Boolean|是|是|是否启用触发器。|取值： -   true
-   false |

## tablestore-TriggerConfig语法

```
"TriggerConfig",: {
  "InstanceName": String,
  "TableName": String
}
```

## tablestore-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceName|String|是|否|表格存储实例名称。|无|
|TableName|String|是|否|数据表名称。|无|

## mns\_topic-TriggerConfig语法

```
"TriggerConfig": {
  "NotifyStrategy": String,
  "NotifyContentFormat": String,
  "FilterTag": String
}
```

## mns\_topic-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NotifyStrategy|String|是|否|重试策略。|取值： -   BACKOFF\_RETRY：退避重试。
-   EXPONENTIAL\_DECAY\_RETRY：指数衰减。

更多信息，请参见[NotifyStrategy]()。|
|NotifyContentFormat|String|是|否|Event格式。|取值： -   STREAM
-   JSON |
|FilterTag|String|否|否|过滤标签。|无|

## cdn-TriggerConfig语法

```
"TriggerConfig": {
  "EventName": String,
  "EventVersion": String,
  "Notes": String,
  "Filter": List
}
```

## cdn-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EventName|String|是|否|触发事件。|取值： -   CachedObjectsBlocked
-   CachedObjectsPushed
-   CachedObjectsRefreshed
-   LogFileCreated
-   CdnDomainStarted
-   CdnDomainStopped
-   CdnDomainAdded
-   CdnDomainDeleted |
|EventVersion|String|是|否|触发事件版本。|无|
|Notes|String|是|是|备注。|无|
|Filter|List|是|是|过滤器。|每个过滤器的键均为`Domain`，至少一个添加一个过滤器。示例值：`[{"Domain": "test.com"}, {"Domain": "pre.com"}, ...]`。|

## http-TriggerConfig语法

**说明：** HTTP触发器只能在创建函数时创建，且不能与其他类型的触发器同时存在。

```
"TriggerConfig": {
  "AuthType": String,
  "Methods": List
}
```

## http-TriggerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AuthType|String|是|否|认证方式。|取值： -   anonymous
-   function |
|Methods|List|是|否|请求方式。|取值： -   GET
-   POST
-   PUT
-   DELETE
-   HEAD
-   PATCH

示例值：`["GET"]`或`["POST", "PUT"]`。|

## 返回值

Fn::GetAtt

-   TriggerId：系统为每个触发器生成的唯一ID。
-   ServiceName：函数服务的名称。
-   FunctionName：函数名称。
-   TriggerName：触发器名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ServiceName": {
      "Type": "String"
    },
    "FunctionName": {
      "Type": "String"
    },
    "CdnDomain": {
      "Type": "Json"
    },
    "SourceConfigLogStore": {
      "Type": "String"
    },
    "LogConfig": {
      "Type": "Json",
      "Description": "for example: {\"Project\": \"testviper\", \"LogStore\": \"vipertest\"}"
    },
    "MnsTopic": {
      "Type": "String"
    },
    "OssBucketName": {
      "Type": "String"
    },
    "OtsInstance": {
      "Type": "String"
    },
    "OtsTable": {
      "Type": "String"
    },
    "OtsInvocationRoleArn": {
      "Type": "String"
    }
  },
  "Resources": {
    "Service": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        }
      }
    },
    "Function": {
      "DependsOn": "Service",
      "Type": "ALIYUN::FC::Function",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Code": {
          "SourceCode": "def handler(event, context):\n\treturn 'Hello World!'"
        },
        "Handler": "index.handler",
        "Runtime": "python3",
        "FunctionName": {
          "Ref": "FunctionName"
        }
      }
    },
    "Role": {
      "Type": "ALIYUN::RAM::Role",
      "Properties": {
        "AssumeRolePolicyDocument": {
          "Version": 1,
          "Statement": [
            {
              "Action": "sts:AssumeRole",
              "Effect": "Allow",
              "Principal": {
                "Service": [
                  "cdn.aliyuncs.com",
                  "fc.aliyuncs.com",
                  "mns.aliyuncs.com",
                  "log.aliyuncs.com",
                  "oss.aliyuncs.com"
                ]
              }
            }
          ]
        },
        "Policies": [
          {
            "PolicyName": "FcTrigger",
            "PolicyDocument": {
              "Version": "1",
              "Statement": [
                {
                  "Effect": "Allow",
                  "Action": [
                    "fc:InvokeFunction",
                    "log:PostLogStoreLogs",
                    "dm:*",
                    "dm:BatchSendMail",
                    "dm:SingleSendMail",
                    "dm:Query*"
                  ],
                  "Resource": [
                    "*"
                  ]
                }
              ]
            }
          }
        ],
        "RoleName": "Trigger"
      }
    },
    "CdnTrigger": {
      "DependsOn": "Function",
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "TriggerName": "cdn",
        "TriggerType": "cdn_events",
        "SourceArn": {
          "Fn::Sub": "acs:cdn:*:${ALIYUN::TenantId}"
        },
        "InvocationRole": {
          "Fn::GetAtt": [
            "Role",
            "Arn"
          ]
        },
        "TriggerConfig": {
          "EventName": "CachedObjectsBlocked",
          "EventVersion": "1.0.0",
          "Notes": "test",
          "Filter": {
            "Domain": {
              "Ref": "CdnDomain"
            }
          }
        }
      }
    },
    "LogTrigger": {
      "DependsOn": "Function",
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "TriggerName": "log",
        "TriggerType": "log",
        "SourceArn": {
          "Fn::Join": [
            "",
            [
              {
                "Fn::Sub": "acs:log:${ALIYUN::Region}:${ALIYUN::TenantId}:project/"
              },
              {
                "Fn::Select": [
                  "Project",
                  {
                    "Ref": "LogConfig"
                  }
                ]
              }
            ]
          ]
        },
        "InvocationRole": {
          "Fn::GetAtt": [
            "Role",
            "Arn"
          ]
        },
        "TriggerConfig": {
          "SourceConfig": {
            "LogStore": {
              "Ref": "SourceConfigLogStore"
            }
          },
          "LogConfig": {
            "Ref": "LogConfig"
          },
          "JobConfig": {
            "MaxRetryTime": 3,
            "TriggerInterval": 60
          },
          "FunctionParameter": {},
          "Enable": false
        }
      }
    },
    "MnsTrigger": {
      "DependsOn": "Function",
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "TriggerName": "mns",
        "TriggerType": "mns_topic",
        "SourceArn": {
          "Fn::Sub": "acs:mns:${ALIYUN::Region}:${ALIYUN::TenantId}:/topics/${MnsTopic}"
        },
        "InvocationRole": {
          "Fn::GetAtt": [
            "Role",
            "Arn"
          ]
        },
        "TriggerConfig": {
          "NotifyStrategy": "BACKOFF_RETRY",
          "NotifyContentFormat": "STREAM",
          "FilterTag": "test"
        }
      }
    },
    "OssTrigger": {
      "DependsOn": "Function",
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "TriggerName": "oss",
        "TriggerType": "oss",
        "SourceArn": {
          "Fn::Sub": "acs:oss:${ALIYUN::Region}:${ALIYUN::TenantId}:${OssBucketName}"
        },
        "InvocationRole": {
          "Fn::GetAtt": [
            "Role",
            "Arn"
          ]
        },
        "TriggerConfig": {
          "BucketName": {
            "Ref": "OssBucketName"
          },
          "Events": [
            "oss:ObjectCreated:*"
          ],
          "Filter": {
            "Key": {
              "Prefix": "b",
              "Suffix": "a"
            }
          }
        }
      }
    },
    "OtsTrigger": {
      "DependsOn": "Function",
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "TriggerName": "ots",
        "TriggerType": "tablestore",
        "SourceArn": {
          "Fn::Sub": "acs:ots:${ALIYUN::Region}:${ALIYUN::TenantId}:instance/${OtsInstance}/table/${OtsTable}"
        },
        "InvocationRole": {
          "Ref": "OtsInvocationRoleArn"
        },
        "TriggerConfig": {
          "InstanceName": {
            "Ref": "OtsInstance"
          },
          "TableName": {
            "Ref": "OtsTable"
          }
        }
      }
    },
    "TimerTrigger": {
      "DependsOn": "Function",
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "TriggerName": "timer",
        "TriggerType": "timer",
        "TriggerConfig": {
          "CronExpression": "0 0/5 * * * *",
          "Enabled": true
        }
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  ServiceName:
    Type: String
  FunctionName:
    Type: String
  CdnDomain:
    Type: Json
  SourceConfigLogStore:
    Type: String
  LogConfig:
    Type: Json
    Description: 'for example: {"Project": "testviper", "LogStore": "vipertest"}'
  MnsTopic:
    Type: String
  OssBucketName:
    Type: String
  OtsInstance:
    Type: String
  OtsTable:
    Type: String
  OtsInvocationRoleArn:
    Type: String
Resources:
  Service:
    Type: 'ALIYUN::FC::Service'
    Properties:
      ServiceName:
        Ref: ServiceName
  Function:
    DependsOn: Service
    Type: 'ALIYUN::FC::Function'
    Properties:
      ServiceName:
        Ref: ServiceName
      Code:
        SourceCode: "def handler(event, context):\n\treturn 'Hello World!'"
      Handler: index.handler
      Runtime: python3
      FunctionName:
        Ref: FunctionName
  Role:
    Type: 'ALIYUN::RAM::Role'
    Properties:
      AssumeRolePolicyDocument:
        Version: 1
        Statement:
          - Action: 'sts:AssumeRole'
            Effect: Allow
            Principal:
              Service:
                - cdn.aliyuncs.com
                - fc.aliyuncs.com
                - mns.aliyuncs.com
                - log.aliyuncs.com
                - oss.aliyuncs.com
      Policies:
        - PolicyName: FcTrigger
          PolicyDocument:
            Version: '1'
            Statement:
              - Effect: Allow
                Action:
                  - 'fc:InvokeFunction'
                  - 'log:PostLogStoreLogs'
                  - 'dm:*'
                  - 'dm:BatchSendMail'
                  - 'dm:SingleSendMail'
                  - 'dm:Query*'
                Resource:
                  - '*'
      RoleName: Trigger
  CdnTrigger:
    DependsOn: Function
    Type: 'ALIYUN::FC::Trigger'
    Properties:
      ServiceName:
        Ref: ServiceName
      FunctionName:
        Ref: FunctionName
      TriggerName: cdn
      TriggerType: cdn_events
      SourceArn:
        'Fn::Sub': 'acs:cdn:*:${ALIYUN::TenantId}'
      InvocationRole:
        'Fn::GetAtt':
          - Role
          - Arn
      TriggerConfig:
        EventName: CachedObjectsBlocked
        EventVersion: 1.0.0
        Notes: test
        Filter:
          Domain:
            Ref: CdnDomain
  LogTrigger:
    DependsOn: Function
    Type: 'ALIYUN::FC::Trigger'
    Properties:
      ServiceName:
        Ref: ServiceName
      FunctionName:
        Ref: FunctionName
      TriggerName: log
      TriggerType: log
      SourceArn:
        'Fn::Join':
          - ''
          - - 'Fn::Sub': 'acs:log:${ALIYUN::Region}:${ALIYUN::TenantId}:project/'
            - 'Fn::Select':
                - Project
                - Ref: LogConfig
      InvocationRole:
        'Fn::GetAtt':
          - Role
          - Arn
      TriggerConfig:
        SourceConfig:
          LogStore:
            Ref: SourceConfigLogStore
        LogConfig:
          Ref: LogConfig
        JobConfig:
          MaxRetryTime: 3
          TriggerInterval: 60
        FunctionParameter: {}
        Enable: false
  MnsTrigger:
    DependsOn: Function
    Type: 'ALIYUN::FC::Trigger'
    Properties:
      ServiceName:
        Ref: ServiceName
      FunctionName:
        Ref: FunctionName
      TriggerName: mns
      TriggerType: mns_topic
      SourceArn:
        'Fn::Sub': 'acs:mns:${ALIYUN::Region}:${ALIYUN::TenantId}:/topics/${MnsTopic}'
      InvocationRole:
        'Fn::GetAtt':
          - Role
          - Arn
      TriggerConfig:
        NotifyStrategy: BACKOFF_RETRY
        NotifyContentFormat: STREAM
        FilterTag: test
  OssTrigger:
    DependsOn: Function
    Type: 'ALIYUN::FC::Trigger'
    Properties:
      ServiceName:
        Ref: ServiceName
      FunctionName:
        Ref: FunctionName
      TriggerName: oss
      TriggerType: oss
      SourceArn:
        'Fn::Sub': 'acs:oss:${ALIYUN::Region}:${ALIYUN::TenantId}:${OssBucketName}'
      InvocationRole:
        'Fn::GetAtt':
          - Role
          - Arn
      TriggerConfig:
        BucketName:
          Ref: OssBucketName
        Events:
          - 'oss:ObjectCreated:*'
        Filter:
          Key:
            Prefix: b
            Suffix: a
  OtsTrigger:
    DependsOn: Function
    Type: 'ALIYUN::FC::Trigger'
    Properties:
      ServiceName:
        Ref: ServiceName
      FunctionName:
        Ref: FunctionName
      TriggerName: ots
      TriggerType: tablestore
      SourceArn:
        'Fn::Sub': >-
          acs:ots:${ALIYUN::Region}:${ALIYUN::TenantId}:instance/${OtsInstance}/table/${OtsTable}
      InvocationRole:
        Ref: OtsInvocationRoleArn
      TriggerConfig:
        InstanceName:
          Ref: OtsInstance
        TableName:
          Ref: OtsTable
  TimerTrigger:
    DependsOn: Function
    Type: 'ALIYUN::FC::Trigger'
    Properties:
      ServiceName:
        Ref: ServiceName
      FunctionName:
        Ref: FunctionName
      TriggerName: timer
      TriggerType: timer
      TriggerConfig:
        CronExpression: 0 0/5 * * * *
        Enabled: true
```

更多示例，请参见创建函数服务、创建函数、执行函数、触发函数执行、发布版本、创建别名和创建预留实例的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/JSON/FunctionInvoker.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/YAML/FunctionInvoker.yml)。


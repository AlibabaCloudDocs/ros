# ALIYUN::FC::Trigger

ALIYUN::FC::Trigger is used to trigger the invocation of a function.

In an event-driven computing model, the source is the event producer, the function is the event processor, and the trigger manages different sources in a centralized manner. On the event source side, when an event that matches the rules defined by a trigger occurs, the event source invokes the corresponding function.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServiceName|String|Yes|No|The name of the Function Compute service.|The name must be 1 to 128 characters in length.|
|FunctionName|String|Yes|No|The name of the function for which you want to create a trigger.|None|
|TriggerName|String|Yes|No|The name of the trigger.|The name must be 1 to 128 characters in length and can contain digits, letters, hyphens \(-\), and underscores \(\_\). It must start with a letter or underscore \(\_\).|
|TriggerType|String|Yes|No|The type of the trigger.|Valid values: -   oss
-   log
-   tablestore
-   timer
-   mns\_topic
-   cdn\_events
-   http

**Note:** You can create an HTTP trigger only when you create a function. When an HTTP trigger is configured for a function, you cannot create other types of triggers for the function. |
|TriggerConfig|Map|Yes|Yes|The trigger configurations.|The configurations vary with the trigger type.|
|InvocationRole|String|No|Yes|The role that is used to grant an event source the permissions to invoke the function on behalf of users. Example: `"acs:ram::1234567890:role/fc-test"`.|This parameter is optional when TriggerType is set to timer or http. This parameter is required when TriggerType is set to a value other than timer and http. The following section lists the trusted entities and policies for role authorization for different types of triggers:

-   oss:
    -   Trusted entity: oss.aliyuncs.com
    -   Policy: Action: fc:InvokeFunction
-   log:
    -   Trusted entity: log.aliyuncs.com
    -   Policy: Action: log:PostLogStoreLogs
-   ots:
    -   Trusted entity: 1604337383174\*\*\*\*
    -   Policy: Action: fc:InvokeFunction, ots:BatchGet\*, ots:Describe\*, ots:Get\*, and ots:List\*
-   mns:
    -   Trusted entity: mns.aliyuncs.com
    -   Policy: Action: dm:BatchSendMail, dm:SingleSendMail, and dm:Query
-   cdn:
    -   Trusted entity: cdn.aliyuncs.com
    -   Policy: Action: fc:InvokeFunction |
|SourceArn|String|No|No|The Alibaba Cloud Resource Name \(ARN\) of the event source.|This parameter is optional when TriggerType is set to timer or http. This parameter is required when TriggerType is set to a value other than timer and http. The following section lists the formats and examples of event source ARNs for different triggers:

-   oss:
    -   Format: `acs:oss:<RegionId>:<TenantId>:<OssBucketName>`
    -   Example: `acs:oss:cn-hangzhou:12345****:test-trigger-bucket`
-   log:
    -   Format: `acs:log:<RegionId>:<TenantId>:project/<The value of Project in the LogConfig property>`
    -   Example: `acs:log:cn-hangzhou:12345****:project/logtrigger`
-   ots:
    -   Format: `acs:ots:<RegionId>:<TenantId>:instance/<OtsInstance>/table/<OtsTable>`
    -   Example: `acs:ots:cn-hangzhou:12345****:instance/otstrigger/table/tb`
-   mns:
    -   Format: `acs:mns:<RegionId>:<TenantId>:/topics/<MnsTopic>`
    -   Example: `acs:mns:cn-hangzhou:12345****:/topics/triggertopic`
-   cdn:
    -   Format: `acs:cdn:*:<TenantId>`
    -   Example: `acs:cdn:*:123456789`

**Note:** Set `TenantId` to the ID of the Alibaba Cloud account. |
|Qualifier|String|No|Yes|The version of the trigger.|Default value: LATEST.|

## oss-TriggerConfig syntax

```
"TriggerConfig": {
  "BucketName": String,
  "Events": List,
  "Filter": Map
}      
```

## oss-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|BucketName|String|Yes|No|The name of the bucket.|You must select an OSS bucket as the event source. The buckets in the same region are displayed in the Bucket drop-down list.|
|Events|String|Yes|Yes|The triggering event that indicates the operations you performed on Alibaba Cloud resources.|Example: `oss:ObjectCreated:*`.|
|Filter|Map|No|Yes|The trigger rules that are used to avoid cyclic triggering.|The values of Prefix and Suffix must be custom strings. Example:

```
"Filter": {
  "Key": {
    "Prefix": "prefix",
    "Suffix": "suffix"
  }
}
``` |

## log-TriggerConfig syntax

```
"TriggerConfig": {
  "SourceConfig": Map,
  "LogConfig": Map,
  "JobConfig": Map,
  "FunctionParameter": Map,
  "Enable": Boolean
}
```

## log-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SourceConfig|Map|Yes|No|The Logstore configurations.|Example: `{"LogStore": "<SLS_LogStore>"}`.|
|LogConfig|Map|Yes|Yes|The configurations of the Log Service project and the Logstore for the trigger.|The Log Service project is required and cannot be updated. The Logstore for the trigger is optional and can be updated. It cannot be the same as the value of LogStore in the SourceConfig property.

Example: `{"Project": "<SLS_Project>", "LogStore": "SLS_LogStore"}`.|
|JobConfig|Map|Yes|Yes|The task configurations. This parameter is used to set the maximum allowable number of retries and the trigger interval.|The trigger interval is measured in seconds.

The maximum allowable number of retries ranges from 0 to 100.

Example: `{"MaxRetryTime": 3, "TriggerInterval": 60}`. |
|FunctionParameter|Map|Yes|Yes|The function configurations that are used to pass parameters to the function.|If no parameters are specified, enter braces \(\{\}\).|
|Enable|Boolean|Yes|Yes|Specifies whether to enable the trigger.|Valid values: -   true
-   false |

## timer-TriggerConfig syntax

```
"TriggerConfig": {
  "Payload": String,
  "CronExpression": String,
  "Enabled": Boolean
}
```

## timer-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Payload|String|No|Yes|The event that is triggered.|None|
|CronExpression|String|Yes|Yes|The cron expression that is used to set the trigger time.|The cron expression runs in Coordinated Universal Time \(UTC\).|
|Enabled|Boolean|Yes|Yes|Specifies whether to enable the trigger.|Valid values: -   true
-   false |

## tablestore-TriggerConfig syntax

```
"TriggerConfig",: {
  "InstanceName": String,
  "TableName": String
}
```

## tablestore-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceName|String|Yes|No|The name of the Tablestore instance.|None|
|TableName|String|Yes|No|The name of the table.|None|

## mns\_topic-TriggerConfig syntax

```
"TriggerConfig": {
  "NotifyStrategy": String,
  "NotifyContentFormat": String,
  "FilterTag": String
}
```

## mns\_topic-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NotifyStrategy|String|Yes|No|The retry policy.|Valid values: -   BACKOFF\_RETRY
-   EXPONENTIAL\_DECAY\_RETRY

For more information, see [NotifyStrategy]().|
|NotifyContentFormat|String|Yes|No|The format of the event.|Valid values: -   STREAM
-   JSON |
|FilterTag|String|No|No|The filtering tag.|None|

## cdn-TriggerConfig syntax

```
"TriggerConfig": {
  "EventName": String,
  "EventVersion": String,
  "Notes": String,
  "Filter": List
}
```

## cdn-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EventName|String|Yes|No|The event that is triggered.|Valid values: -   CachedObjectsBlocked
-   CachedObjectsPushed
-   CachedObjectsRefreshed
-   LogFileCreated
-   CdnDomainStarted
-   CdnDomainStopped
-   CdnDomainAdded
-   CdnDomainDeleted |
|EventVersion|String|Yes|No|The version of the event.|None|
|Notes|String|Yes|Yes|The comments.|None|
|Filter|List|Yes|Yes|The filters.|The key of each filter is `Domain`. You must specify at least one filter. Example: `[{"Domain": "test.com"}, {"Domain": "pre.com"}, ...]`.|

## http-TriggerConfig syntax

**Note:** You can create an HTTP trigger only when you create a function. When an HTTP trigger is configured for a function, you cannot create other types of triggers for the function.

```
"TriggerConfig": {
  "AuthType": String,
  "Filter": List
}
```

## http-TriggerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AuthType|String|Yes|No|The authentication method.|Valid values: -   anonymous
-   function |
|Methods|List|Yes|No|The methods that are used to make the request.|Valid values: -   GET
-   POST
-   PUT
-   DELETE
-   HEAD
-   PATCH

Example: `["GET"]` or `["POST", "PUT"]`.|

## Response parameters

Fn::GetAtt

-   TriggerId: the unique ID generated by the system for each trigger.
-   ServiceName: the name of the service to which the function belongs.
-   FunctionName: the name of the function.
-   TriggerName: the name of the trigger.

## Examples

`JSON` format

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

`YAML` format

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


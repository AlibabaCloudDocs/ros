# ALIYUN::FC::Service

ALIYUN::FC::Service类型用于创建服务。服务下的所有函数共享一些相同的设置，例如：服务授权、配置日志。同一服务下有多个函数，这些函数共享服务配置的资源（例如：日志库、服务角色等）。

服务能帮助您更清晰的组织业务逻辑，是运维管理的基本单位。一个服务可以表示一个应用，构建同一应用的不同函数将放到同一服务下。服务之间不共享任何资源，没有任何依赖。

## 语法

```
{
  "Type": "ALIYUN::FC::Service",
  "Properties": {
    "Description": String,
    "VpcConfig": Map,
    "ServiceName": String,
    "Role": String,
    "DeletionForce": Boolean,
    "Tags": List,
    "NasConfig": Map,
    "LogConfig": Map,
    "TracingConfig": Map,
    "InternetAccess": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|服务的描述。|无|
|VpcConfig|Map|否|是|专有网络配置，配置后函数可以访问指定专有网络。|更多信息，请参见[VpcConfig属性](#section_9l4_hcb_3f6)。更新资源栈时，若要删除网络配置，取值为：

```
{
  "VpcId": "",
  "VSwitchIds": [],
  "SecurityGroupId": ""
}
``` |
|ServiceName|String|是|否|服务名称。|长度为1~128个字符，以英文字母或下划线（\_）开头，可包含英文字母、数字、下划线（\_）和短划线（-）。|
|Role|String|否|是|授予函数计算所需权限的RAM角色ARN，使用场景包含： -   把函数产生的日志发送到用户的日志库中。
-   为函数在执行中访问其它云资源生成Token。

|无|
|NasConfig|Map|否|是|NAS配置， 配置后函数可以访问指定NAS资源。|更多信息，请参见[NasConfig属性](#section_zgf_pgd_3o9)。更新资源栈时，若要删除NAS配置，取值为：

```
{
  "MountPoints": [],
  "UserId": -1,
  "GroupId": -1
}
``` |
|LogConfig|Map|否|是|日志配置，函数产生的日志会写入此处配置的日志库中。|更多信息，请参见[LogConfig属性](#section_axf_5ea_8q5)。|
|TracingConfig|Map|否|是|链路追踪配置。当函数计算与链路追踪集成后，您可以记录请求在函数计算的耗时时间、查看函数的冷启动时间、记录函数内部时间的消耗等。|更多信息，请参见[TracingConfig属性](#section_qy0_g7q_l0g)。|
|InternetAccess|Boolean|否|是|函数是否可以访问公网。|取值： -   true
-   false |
|DeletionForce|Boolean|否|是|是否强制删除。|取值： -   true
-   false（默认值）

指定 VpcConfig时该参数生效。

-   当DeletionForce为true时，会直接删除此服务，而不等待由函数计算为此服务所创建的ENI被函数清理掉。
-   当DeletionForce不填或为false时，会等待由函数计算为此服务所创建的所有ENI被函数计算清理掉，然后再删除此服务。

如果在当前Stack中创建了交换机或安全组，并基于它们创建了此服务，在删除时无需指定DeletionForce，并要求在一小时内不要触发此服务的函数调用，这样其ENI才能被正常删除，进而正常删除整个Stack。

如果创建此服务所用到的交换机或安全组为参数传入，则在删除时可指定DeletionForce为true，以跳过等待，从而减少删除时间。 |
|Tags|List|否|是|标签。|最多支持20个标签。 更多信息，请参见[Tags属性](#section_4zh_1ll_zwf)。 |

## LogConfig语法

```
"LogConfig": {
  "Project": String,
  "Logstore": String,
  "EnableRequestMetrics": Boolean
}
```

## LogConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|否|是|日志中枢中的Project名称。|无|
|Logstore|String|否|是|日志中枢中的日志库名称。|无|
|EnableRequestMetrics|Boolean|否|是|是否启用请求监控。|取值：-   true
-   false |

## VpcConfig语法

```
"VpcConfig": {
  "SecurityGroupId": String,
  "VSwitchIds": List,
  "VpcId": String
}
```

## VpcConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|安全组ID。|无|
|VSwitchIds|List|是|是|一个或多个交换机ID。|多个交换机ID之间用半角逗号（,）分隔，例如：\[VSwitchId1, VSwitchId2\]。|
|VpcId|String|是|是|专有网络ID。|无|

## NasConfig语法

```
"NasConfig": {
  "MountPoints": List,
  "UserId": Integer,
  "GroupId": Integer
}
```

## NasConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MountPoints|List|是|是|挂载点。|更多信息，请参见[MountPoints属性](#section_zgf_pgd_319)。|
|UserId|Integer|是|是|用户ID。|取值范围：-1~65,534。|
|GroupId|Integer|是|是|群组ID。|取值范围：-1~65,534。|

## TracingConfig语法

```
"TracingConfig": {
  "Type": String,
  "Params": Map
}
```

## TracingConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|否|是|链路追踪系统的类型。|无|
|Params|Map|否|是|链路追踪的参数。|无|

## MountPoints语法

```
"MountPoints": [
  {
    "ServerAddr": String,
    "MountDir": String
  }
]
```

## MountPoints属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerAddr|String|是|是|NAS服务器地址。|无|
|MountDir|String|是|是|本地挂载目录。|无|

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   ServiceId：系统为每个服务生成的唯一ID。
-   ServiceName：服务名称。
-   Tags：标签。
-   Role：RAM角色。
-   LogProject：日志项目。
-   Logstore：日志库。
-   InternetAccess：函数是否可以访问公网。
-   VpcId：专有网络ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Role": {
      "Type": "String",
      "Description": "The role grants Function Compute the permission to access user’s cloud resources, such as pushing logs to user’s log store. The temporary STS token generated from this role can be retrieved from function context and used to access cloud resources. "
    },
    "InternetAccess": {
      "Type": "Boolean",
      "Description": "Set it to true to enable Internet access.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "Service description"
    },
    "DeletionForce": {
      "Type": "Boolean",
      "Description": "Whether force delete the service without waiting for network interfaces to be cleaned up if VpcConfig is specified. Default value is false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "TracingConfig": {
      "Type": "Json",
      "Description": "The Tracing Analysis configuration. After Function Compute integrates with Tracing Analysis, you can record the stay time of a request in Function Compute, view the cold start time for a function, and record the execution time of a function."
    },
    "VpcConfig": {
      "Type": "Json",
      "Description": "VPC configuration. Function Compute uses the config to setup ENI in the specific VPC."
    },
    "ServiceName": {
      "Type": "String",
      "Description": "Service name",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to service. Max support 20 tags to add during create service. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "NasConfig": {
      "Type": "Json",
      "Description": "NAS configuration. Function Compute uses a specified NAS configured on the service."
    },
    "LogConfig": {
      "Type": "Json",
      "Description": "Log configuration. Function Compute pushes function execution logs to the configured log store."
    }
  },
  "Resources": {
    "Service": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "Role": {
          "Ref": "Role"
        },
        "InternetAccess": {
          "Ref": "InternetAccess"
        },
        "Description": {
          "Ref": "Description"
        },
        "DeletionForce": {
          "Ref": "DeletionForce"
        },
        "TracingConfig": {
          "Ref": "TracingConfig"
        },
        "VpcConfig": {
          "Ref": "VpcConfig"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "NasConfig": {
          "Ref": "NasConfig"
        },
        "LogConfig": {
          "Ref": "LogConfig"
        }
      }
    }
  },
  "Outputs": {
    "Role": {
      "Description": "Role of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "Role"
        ]
      }
    },
    "InternetAccess": {
      "Description": "Whether enable Internet access",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "InternetAccess"
        ]
      }
    },
    "VpcId": {
      "Description": "VPC ID",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "VpcId"
        ]
      }
    },
    "ServiceName": {
      "Description": "The service name",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "ServiceName"
        ]
      }
    },
    "Logstore": {
      "Description": "Log store of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "Logstore"
        ]
      }
    },
    "Tags": {
      "Description": "Tags of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "Tags"
        ]
      }
    },
    "LogProject": {
      "Description": "Log project of service",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "LogProject"
        ]
      }
    },
    "ServiceId": {
      "Description": "The service ID",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "ServiceId"
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
  DeletionForce:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Whether force delete the service without waiting for network interfaces
      to be cleaned up if VpcConfig is specified. Default value is false.
    Type: Boolean
  Description:
    Description: Service description
    Type: String
  InternetAccess:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Set it to true to enable Internet access.
    Type: Boolean
  LogConfig:
    Description: Log configuration. Function Compute pushes function execution logs
      to the configured log store.
    Type: Json
  NasConfig:
    Description: NAS configuration. Function Compute uses a specified NAS configured
      on the service.
    Type: Json
  Role:
    Description: "The role grants Function Compute the permission to access user\u2019\
      s cloud resources, such as pushing logs to user\u2019s log store. The temporary\
      \ STS token generated from this role can be retrieved from function context\
      \ and used to access cloud resources. "
    Type: String
  ServiceName:
    Description: Service name
    MaxLength: 128
    MinLength: 1
    Type: String
  Tags:
    Description: Tags to attach to service. Max support 20 tags to add during create
      service. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  TracingConfig:
    Description: The Tracing Analysis configuration. After Function Compute integrates
      with Tracing Analysis, you can record the stay time of a request in Function
      Compute, view the cold start time for a function, and record the execution time
      of a function.
    Type: Json
  VpcConfig:
    Description: VPC configuration. Function Compute uses the config to setup ENI
      in the specific VPC.
    Type: Json
Resources:
  Service:
    Properties:
      DeletionForce:
        Ref: DeletionForce
      Description:
        Ref: Description
      InternetAccess:
        Ref: InternetAccess
      LogConfig:
        Ref: LogConfig
      NasConfig:
        Ref: NasConfig
      Role:
        Ref: Role
      ServiceName:
        Ref: ServiceName
      Tags:
        Ref: Tags
      TracingConfig:
        Ref: TracingConfig
      VpcConfig:
        Ref: VpcConfig
    Type: ALIYUN::FC::Service
Outputs:
  InternetAccess:
    Description: Whether enable Internet access
    Value:
      Fn::GetAtt:
      - Service
      - InternetAccess
  LogProject:
    Description: Log project of service
    Value:
      Fn::GetAtt:
      - Service
      - LogProject
  Logstore:
    Description: Log store of service
    Value:
      Fn::GetAtt:
      - Service
      - Logstore
  Role:
    Description: Role of service
    Value:
      Fn::GetAtt:
      - Service
      - Role
  ServiceId:
    Description: The service ID
    Value:
      Fn::GetAtt:
      - Service
      - ServiceId
  ServiceName:
    Description: The service name
    Value:
      Fn::GetAtt:
      - Service
      - ServiceName
  Tags:
    Description: Tags of service
    Value:
      Fn::GetAtt:
      - Service
      - Tags
  VpcId:
    Description: VPC ID
    Value:
      Fn::GetAtt:
      - Service
      - VpcId
```

更多示例，请参见创建函数服务、创建函数、执行函数、触发函数执行、发布版本、创建别名和创建预留实例的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/JSON/FunctionInvoker.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/YAML/FunctionInvoker.yml)。


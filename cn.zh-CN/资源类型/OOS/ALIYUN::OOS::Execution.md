# ALIYUN::OOS::Execution

ALIYUN::OOS::Execution类型用于启动一个执行。

## 语法

```
{
  "Type": "ALIYUN::OOS::Execution",
  "Properties": {
    "ResourceOptions": Map,
    "Parameters": Map,
    "Tags": Map,
    "TemplateName": String,
    "ParentExecutionId": String,
    "SafetyCheck": String,
    "Mode": String,
    "TemplateVersion": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceOptions|Map|否|否|ROS使用的资源选项。|更多信息，请参见[ResourceOptions属性](#section_s9q_6bm_ry1)。|
|Parameters|Map|否|否|由参数集合组成的JSON字符串。|示例值：`{"Status": "Running"}`。默认值：\{\}。 |
|Tags|Map|否|否|标签，由键值对组成。例如：\{“k1”:”v1”, ”k2”:”v2”\}。|最多支持20个标签。|
|TemplateName|String|是|否|模板名称。|最长为200个字符，不能以ALIYUN、ACS、ALIBABA开头。可包含英文字母、数字、短划线（-）和下划线（\_）。|
|ParentExecutionId|String|否|否|父执行ID。|无|
|SafetyCheck|String|否|否|安全检查模式。|取值： -   Skip：表示客户了解风险，无需确认即可执行任何Action，无论什么风险等级。当Mode取值为Automatic时有效。
-   ConfirmEveryHighRiskAction（默认值）：要求客户确认每一个高风险的Action。客户通过调用NotifyExecution接口进行确认或取消。 |
|Mode|String|否|否|执行模式。|取值范围： -   Debug
-   Automatic（默认值） |
|TemplateVersion|String|否|否|版本号。|如果不填默认为最新的版本号。|

## ResourceOptions语法

```
"ResourceOptions": {
  "SuccessStatuses": List,
  "Timeout": Number,
  "CancelOnDelete": Boolean,
  "FailureStatuses": List
}
```

## ResourceOptions属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SuccessStatuses|List|否|否|ROS使用该属性判断资源是否创建成功。|取值： -   Started
-   Queued
-   Running
-   Waiting
-   Success（默认值）
-   Failed
-   Cancelled

如果Execution的状态在FailureStatuses中，则判定为失败。如果Execution的状态在SuccessStatuses中，则判定为成功。如果上述条件不符合，则一直等待，直到超时（Timeout）。|
|Timeout|Number|否|否|超时时间。|单位：秒。默认值：1800。 |
|CancelOnDelete|Boolean|否|否|删除资源时，如果执行未完成是否取消执行。|取值：-   true
-   false（默认值） |
|FailureStatuses|List|否|否|ROS使用该属性判断资源是否创建失败。FailureStatuses优先级高于SuccessStatuses。|取值： -   Started
-   Queued
-   Running
-   Waiting
-   Success
-   Failed
-   Cancelled

默认值：`["Failed", "Cancelled"]`。 |

## 返回值

Fn::GetAtt

-   Status：执行状态。
-   WindowsCurlCli：为Windows提供curl CLI命令前缀，可用于发出处理完成或失败的信号。更多信息，请参见[NotifyExecution]()。
-   PowerShellCurlCli：为PowerShell提供curl CLI命令前缀，可用于发出信号处理完成或失败。
-   Outputs：执行输出结果。
-   ExecutionId：执行的唯一标识。
-   CurlCli：curl命令。
-   StatusMessage：状态信息。
-   Counters：执行数。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ParentExecutionId": {
      "Type": "String",
      "Description": "Parent execution ID."
    },
    "ResourceOptions": {
      "Type": "Json",
      "Description": "Resource options user by ROS."
    },
    "Parameters": {
      "Type": "Json",
      "Description": "Parameters for the execution of template."
    },
    "SafetyCheck": {
      "Type": "String",
      "Description": "Security check mode. Allowed values:\n- Skip: This option means that customers understand the risks, you can do anything without confirmation Action, no matter what the level of risk. It takes effect only if Mode is Automatic.\n- ConfirmEveryHighRiskAction (default): This option would require customers to confirm each Action a high risk. NotifyExecution by calling customer interface to confirm or cancel.",
      "AllowedValues": [
        "ConfirmEveryHighRiskAction",
        "Skip"
      ],
      "Default": "ConfirmEveryHighRiskAction"
    },
    "Mode": {
      "Type": "String",
      "Description": "Execution mode.",
      "AllowedValues": [
        "Automatic",
        "Debug"
      ],
      "Default": "Automatic"
    },
    "TemplateName": {
      "Type": "String",
      "Description": "Template name. Content is limited to letters, numbers, underlined, underline, the length of 200 characters, and can not begin to ALIYUN, ACS, ALIBABA.",
      "MaxLength": 200
    },
    "TemplateVersion": {
      "Type": "String",
      "Description": "Version number of template. Default to the latest version."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tag value and the key mapping, the label of the key number can be up to 20.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "Execution": {
      "Type": "ALIYUN::OOS::Execution",
      "Properties": {
        "ParentExecutionId": {
          "Ref": "ParentExecutionId"
        },
        "ResourceOptions": {
          "Ref": "ResourceOptions"
        },
        "Parameters": {
          "Ref": "Parameters"
        },
        "SafetyCheck": {
          "Ref": "SafetyCheck"
        },
        "Mode": {
          "Ref": "Mode"
        },
        "TemplateName": {
          "Ref": "TemplateName"
        },
        "TemplateVersion": {
          "Ref": "TemplateVersion"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "Status": {
      "Description": "Execution status.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "Status"
        ]
      }
    },
    "CurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix, which can be used to notify oos execution instead of OOS API NotifyExecution.\nYou can notify approve to oos execution by adding --data-binary '{\"data\": {\"NotifyType\": \"Approve\"}}' \nFor more parameters in data, refer to https://help.aliyun.com/document_detail/120777.html.\nYou can also notify execution via ROS API SignalResource. API parameters Status and UniqueId are ignored. Use API parameter Data to pass data.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "CurlCli"
        ]
      }
    },
    "WindowsCurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix for Windows, which can be used to notify oos execution instead of OOS API NotifyExecution.\nYou can notify approve to oos execution by adding --data-binary \"{\\\"data\\\": {\\\"NotifyType\\\": \\\"Approve\\\"}}\" \nFor more parameters in data, refer to https://help.aliyun.com/document_detail/120777.html.You can also notify execution via ROS API SignalResource. API parameters Status and UniqueId are ignored. Use API parameter Data to pass data.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "WindowsCurlCli"
        ]
      }
    },
    "Outputs": {
      "Description": "Execution output.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "Outputs"
        ]
      }
    },
    "Counters": {
      "Description": "Task statistics: FailedTasks, SuccessTasks, TotalTasks.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "Counters"
        ]
      }
    },
    "PowerShellCurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix for PowerShell, which can be used to notify oos execution instead of OOS API NotifyExecution.\nYou can notify approve to oos execution by adding -Body '{\"data\": {\"NotifyType\": \"Approve\"}}' \nFor more parameters in data, refer to https://help.aliyun.com/document_detail/120777.html.You can also notify execution via ROS API SignalResource. API parameters Status and UniqueId are ignored. Use API parameter Data to pass data.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "PowerShellCurlCli"
        ]
      }
    },
    "ExecutionId": {
      "Description": "Execution ID.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "ExecutionId"
        ]
      }
    },
    "StatusMessage": {
      "Description": "Execution status information.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "StatusMessage"
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
  Mode:
    AllowedValues:
    - Automatic
    - Debug
    Default: Automatic
    Description: Execution mode.
    Type: String
  Parameters:
    Description: Parameters for the execution of template.
    Type: Json
  ParentExecutionId:
    Description: Parent execution ID.
    Type: String
  ResourceOptions:
    Description: Resource options user by ROS.
    Type: Json
  SafetyCheck:
    AllowedValues:
    - ConfirmEveryHighRiskAction
    - Skip
    Default: ConfirmEveryHighRiskAction
    Description: 'Security check mode. Allowed values:

      - Skip: This option means that customers understand the risks, you can do anything
      without confirmation Action, no matter what the level of risk. It takes effect
      only if Mode is Automatic.

      - ConfirmEveryHighRiskAction (default): This option would require customers
      to confirm each Action a high risk. NotifyExecution by calling customer interface
      to confirm or cancel.'
    Type: String
  Tags:
    Description: Tag value and the key mapping, the label of the key number can be
      up to 20.
    MaxLength: 20
    Type: Json
  TemplateName:
    Description: Template name. Content is limited to letters, numbers, underlined,
      underline, the length of 200 characters, and can not begin to ALIYUN, ACS, ALIBABA.
    MaxLength: 200
    Type: String
  TemplateVersion:
    Description: Version number of template. Default to the latest version.
    Type: String
Resources:
  Execution:
    Properties:
      Mode:
        Ref: Mode
      Parameters:
        Ref: Parameters
      ParentExecutionId:
        Ref: ParentExecutionId
      ResourceOptions:
        Ref: ResourceOptions
      SafetyCheck:
        Ref: SafetyCheck
      Tags:
        Ref: Tags
      TemplateName:
        Ref: TemplateName
      TemplateVersion:
        Ref: TemplateVersion
    Type: ALIYUN::OOS::Execution
Outputs:
  Counters:
    Description: 'Task statistics: FailedTasks, SuccessTasks, TotalTasks.'
    Value:
      Fn::GetAtt:
      - Execution
      - Counters
  CurlCli:
    Description: "Convenience attribute, provides curl CLI command prefix, which can\
      \ be used to notify oos execution instead of OOS API NotifyExecution.\nYou can\
      \ notify approve to oos execution by adding --data-binary '{\"data\": {\"NotifyType\"\
      : \"Approve\"}}' \nFor more parameters in data, refer to https://help.aliyun.com/document_detail/120777.html.\n\
      You can also notify execution via ROS API SignalResource. API parameters Status\
      \ and UniqueId are ignored. Use API parameter Data to pass data."
    Value:
      Fn::GetAtt:
      - Execution
      - CurlCli
  ExecutionId:
    Description: Execution ID.
    Value:
      Fn::GetAtt:
      - Execution
      - ExecutionId
  Outputs:
    Description: Execution output.
    Value:
      Fn::GetAtt:
      - Execution
      - Outputs
  PowerShellCurlCli:
    Description: "Convenience attribute, provides curl CLI command prefix for PowerShell,\
      \ which can be used to notify oos execution instead of OOS API NotifyExecution.\n\
      You can notify approve to oos execution by adding -Body '{\"data\": {\"NotifyType\"\
      : \"Approve\"}}' \nFor more parameters in data, refer to https://help.aliyun.com/document_detail/120777.html.You\
      \ can also notify execution via ROS API SignalResource. API parameters Status\
      \ and UniqueId are ignored. Use API parameter Data to pass data."
    Value:
      Fn::GetAtt:
      - Execution
      - PowerShellCurlCli
  Status:
    Description: Execution status.
    Value:
      Fn::GetAtt:
      - Execution
      - Status
  StatusMessage:
    Description: Execution status information.
    Value:
      Fn::GetAtt:
      - Execution
      - StatusMessage
  WindowsCurlCli:
    Description: "Convenience attribute, provides curl CLI command prefix for Windows,\
      \ which can be used to notify oos execution instead of OOS API NotifyExecution.\n\
      You can notify approve to oos execution by adding --data-binary \"{\\\"data\\\
      \": {\\\"NotifyType\\\": \\\"Approve\\\"}}\" \nFor more parameters in data,\
      \ refer to https://help.aliyun.com/document_detail/120777.html.You can also\
      \ notify execution via ROS API SignalResource. API parameters Status and UniqueId\
      \ are ignored. Use API parameter Data to pass data."
    Value:
      Fn::GetAtt:
      - Execution
      - WindowsCurlCli
```

更多示例，请参见创建模板和启动一个执行的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OOS/JSON/OOS.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OOS/YAML/OOS.yml)。


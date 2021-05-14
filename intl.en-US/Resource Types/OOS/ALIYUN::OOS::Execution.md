# ALIYUN::OOS::Execution

ALIYUN::OOS::Execution is used to start an execution.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceOptions|Map|No|No|The resource options used by Resource Orchestration Service \(ROS\).|For more information, see the [ResourceOptions properties](#section_s9q_6bm_ry1) section in this topic.|
|Parameters|Map|No|No|The JSON-formatted strings that consist of parameters.|Example: `{"Status": "Running"}`. Default value: \{\}. |
|Tags|Map|No|No|Tags. A tag is a key-value pair. Example: \{"k1":"v1","k2":"v2"\}.|A maximum of 20 tags can be specified.|
|TemplateName|String|Yes|No|The name of the template.|The template name can be up to 200 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\). It cannot start with ALIYUN, ACS, or ALIBABA.|
|ParentExecutionId|String|No|No|The ID of the parent execution.|None|
|SafetyCheck|String|No|No|The safety check mode.|Default value: ConfirmEveryHighRiskAction. Valid values: -   Skip: specifies that you are aware of the risks. The system executes all actions in the execution without manual confirmation, regardless of the risk level. This parameter is valid only when Mode is set to Automatic.
-   ConfirmEveryHighRiskAction: requires you to confirm every high-risk action. You can call the NotifyExecution operation to confirm or cancel an action. |
|Mode|String|No|No|The execution mode.|Default value: Automatic. Valid values: -   Debug
-   Automatic |
|TemplateVersion|String|No|No|The version number.|If you do not specify this parameter, the system uses the latest version.|

## ResourceOptions syntax

```
"ResourceOptions": {
  "SuccessStatuses": List,
  "Timeout": Number,
  "CancelOnDelete": Boolean,
  "FailureStatuses": List
}
```

## ResourceOptions properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SuccessStatuses|List|No|No|Specifies whether resources are created.|Default value: Success. Valid values: -   Started
-   Queued
-   Running
-   Waiting
-   Success
-   Failed
-   Cancelled

If the Status value is included in the FailureStatuses value, the creation is considered failed. If the Status value is included in the SuccessStatuses value, the creation is considered successful. If neither of the preceding conditions is met, the system waits till the stack creation request times out.|
|Timeout|Number|No|No|The timeout period.|Unit: seconds. Default value: 1800. |
|CancelOnDelete|Boolean|No|No|Specifies whether to cancel the execution that has not been completed when the resource is being deleted.|Default value: false. Valid values:-   true
-   false |
|FailureStatuses|List|No|No|Specifies whether resources fail to be created. FailureStatuses takes precedence over SuccessStatuses.|Valid values: -   Started
-   Queued
-   Running
-   Waiting
-   Success
-   Failed
-   Cancelled

Default value: `["Failed", "Cancelled"]`. |

## Response parameters

Fn::GetAtt

-   Status: the execution status.
-   WindowsCurlCli: provides Windows with cURL CLI command prefixes and sends a message that indicates whether the execution is completed or failed.
-   PowerShellCurlCli: provides PowerShell with cURL CLI command prefixes and sends a message that indicates whether the execution is completed or failed.
-   Outputs: the output of the execution.
-   ExecutionId: the unique ID of the execution.
-   CurlCli: the cURL command.
-   StatusMessage: the status information.
-   Counters: the number of executions.

## Examples

`JSON` format

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
      "Description": "Convenience attribute, provides curl CLI command prefix, which can be used to notify oos execution instead of OOS API NotifyExecution.\nYou can notify approve to oos execution by adding --data-binary '{\"data\": {\"NotifyType\": \"Approve\"}}' \nYou can also notify execution via ROS API SignalResource. API parameters Status and UniqueId are ignored. Use API parameter Data to pass data.",
      "Value": {
        "Fn::GetAtt": [
          "Execution",
          "CurlCli"
        ]
      }
    },
    "WindowsCurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix for Windows, which can be used to notify oos execution instead of OOS API NotifyExecution.\nYou can notify approve to oos execution by adding --data-binary \"{\\\"data\\\": {\\\"NotifyType\\\": \\\"Approve\\\"}}\" \nYou can also notify execution via ROS API SignalResource. API parameters Status and UniqueId are ignored. Use API parameter Data to pass data.",
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
      "Description": "Convenience attribute, provides curl CLI command prefix for PowerShell, which can be used to notify oos execution instead of OOS API NotifyExecution.\nYou can notify approve to oos execution by adding -Body '{\"data\": {\"NotifyType\": \"Approve\"}}' \nYou can also notify execution via ROS API SignalResource. API parameters Status and UniqueId are ignored. Use API parameter Data to pass data.",
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

`YAML` format

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
      : \"Approve\"}}' \n\
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
      : \"Approve\"}}' \You\
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
      \": {\\\"NotifyType\\\": \\\"Approve\\\"}}\" \nYou can also\
      \ notify execution via ROS API SignalResource. API parameters Status and UniqueId\
      \ are ignored. Use API parameter Data to pass data."
    Value:
      Fn::GetAtt:
      - Execution
      - WindowsCurlCli
```

For more examples, visit [OOS.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OOS/JSON/OOS.json) and [OOS.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/OOS/YAML/OOS.yml). In the examples, the ALIYUN::OOS::Template and ALIYUN::OOS::Execution resource types are involved.


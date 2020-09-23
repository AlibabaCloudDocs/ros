# ALIYUN::ECS::Command

ALIYUN::ECS::Command is used to create a Cloud Assistant command.

## Syntax

```
{
  "Type": "ALIYUN::ECS::Command",
  "Properties": {
    "Name": String,
    "WorkingDir": String,
    "CommandContent": String,
    "Timeout": Integer,
    "Type": String,
    "Description": String,
    "EnableParameter": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|No|Yes|The name of the command.|The name must be 1 to 128 characters in length. All character sets are supported.|
|WorkingDir|String|No|Yes|The working directory on the ECS instance where the command will be run.|Default value: -   Linux instance: the home directory of the root user, which is the `/root` directory.
-   Windows instance: the directory where the Cloud Assistant client process resides, such as `C:\Windows\System32\`. |
|CommandContent|String|No|No|The Base64-encoded content of the command.|The parameter value must be Base64-encoded and cannot exceed 16 KB in size after encoding.The command content can be specified by using custom parameters. To enable custom parameters, you must set `EnableParameter` to true.

-   You can define parameters by enclosing them in nested braces \{\{\}\}. The spaces and line breaks before and after parameter names in \{\{\}\} are ignored.
-   The number of custom parameters cannot exceed 20.
-   The name of a custom parameter can contain letters and digits and is case-insensitive.
-   Each custom parameter name cannot exceed 64 characters in length. |
|Timeout|Integer|No|Yes|The timeout period that is specified for the command to run on ECS instances.|If the command fails to run within the specified period, the command times out and the command process is forcibly terminated.

Default value: 60.

Unit: seconds.|
|Type|String|Yes|No|The type of the command.|Valid values: -   RunBatScript: creates a batch command for a Windows instance.
-   RunPowerShellScript: creates a PowerShell command for a Windows instance.
-   RunShellScript: creates a Shell command for a Linux instance. |
|Description|String|No|Yes|The description of the command.|The description must be 1 to 512 characters in length. All character sets are supported.|
|EnableParameter|Boolean|No|No|Specifies whether the created command uses custom parameters.|Default value: false. Valid values: -   true
-   false |

## Response parameters

Fn::GetAtt

CommandId: the ID of the command.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "WorkingDir": {
      "Type": "String",
      "Description": "The path where command will be executed in the instance."
    },
    "CommandContent": {
      "Type": "String",
      "Description": "The content of command. Content requires base64 encoding. Maximum size support 16KB."
    },
    "Type": {
      "Type": "String",
      "Description": "The type of command."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of command."
    },
    "Timeout": {
      "Type": "Number",
      "Description": "Total timeout when the command is executed in the instance. Input the time unit as second. Default is 60s."
    },
    "EnableParameter": {
      "Type": "Boolean",
      "Description": "Specifies whether the script contains custom parameters.\nDefault value: false",
      "AllowedValues": [
        true,
        false
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "The name of command."
    }
  },
  "Resources": {
    "Command": {
      "Type": "ALIYUN::ECS::Command",
      "Properties": {
        "WorkingDir": {
          "Ref": "WorkingDir"
        },
        "CommandContent": {
          "Ref": "CommandContent"
        },
        "Type": {
          "Ref": "Type"
        },
        "Description": {
          "Ref": "Description"
        },
        "Timeout": {
          "Ref": "Timeout"
        },
        "EnableParameter": {
          "Ref": "EnableParameter"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "CommandId": {
      "Description": "The id of command created.",
      "Value": {
        "Fn::GetAtt": [
          "Command",
          "CommandId"
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
  WorkingDir:
    Type: String
    Description: The path where command will be executed in the instance.
  CommandContent:
    Type: String
    Description: >-
      The content of command. Content requires base64 encoding. Maximum size
      support 16KB.
  Type:
    Type: String
    Description: The type of command.
  Description:
    Type: String
    Description: The description of command.
  Timeout:
    Type: Number
    Description: >-
      Total timeout when the command is executed in the instance. Input the time
      unit as second. Default is 60s.
  EnableParameter:
    Type: Boolean
    Description: |-
      Specifies whether the script contains custom parameters.
      Default value: false
    AllowedValues:
      - true
      - false
  Name:
    Type: String
    Description: The name of command.
Resources:
  Command:
    Type: 'ALIYUN::ECS::Command'
    Properties:
      WorkingDir:
        Ref: WorkingDir
      CommandContent:
        Ref: CommandContent
      Type:
        Ref: Type
      Description:
        Ref: Description
      Timeout:
        Ref: Timeout
      EnableParameter:
        Ref: EnableParameter
      Name:
        Ref: Name
Outputs:
  CommandId:
    Description: The id of command created.
    Value:
      'Fn::GetAtt':
        - Command
        - CommandId
```


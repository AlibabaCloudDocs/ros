# ALIYUN::ROS::WaitConditionHandle

ALIYUN::ROS::WaitConditionHandle is used to create an instance that sends and receives messages when user data is being executed.

## Syntax

```
{
  "Type": "ALIYUN::ROS::WaitConditionHandle",
  "Properties": {
    "Count": Integer, 
    "Mode": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Count|Integer|No|Yes|The total number of messages to be received.|Default value: -1.|
|Mode|String|No|Yes|The working mode of the instance.|Default value: Full. Valid values:

-   Increment: All previous signals are deleted before they are updated. If this parameter is set to Increment, the Count value must be an incremental value instead of an integer.
-   Full: No previous signals are deleted unless the Count parameter is specified. If this parameter is set to Full, the Count value must be an integer. |

## Response parameters

Fn::GetAtt

-   CurlCli: A cURL command that is generated by the resource. You can use the command to send the user data execution result or status to ROS.
-   WindowsCurlCli: provides cURL CLI command prefixes for Windows and sends a message that indicates whether the execution succeeds or fails. Windows does not support the cURL command. Therefore, you must install curl.exe and add it to PATH. You can add `--data-binary "{\"status\": \" success \"}` to indicate that the execution succeeds and add `--data-binary "{\"status\": \" failure \"}` to indicate that the execution fails.
-   PowerShellCurlCli: provides cURL CLI command prefixes for PowerShell and sends a message that indicates whether the execution succeeds or fails. This cmdlet was introduced in PowerShell 3.0. Therefore, you must make sure that the version of PowerShell satisfies the constraint. You can use the `$PSVersionTable.PSVersion` command to obtain the version number. You can add `-Body '{"status": " success "}` to indicate that the execution succeeds and add `-Body '{"status": " failure "}` to indicate that the execution fails.
-   Headers: the HTTP POST request header used to send a message that indicates whether the execution succeeds or fails.
-   URL: the HTTP POST request URL used to send a message that indicates whether the execution succeeds or fails.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Mode": {
      "Type": "String",
      "Description": "If set to Increment, all old signals will be deleted before update. In this mode, WaitCondition.Count should reference an incremental value instead of a full value, such as ScalingGroupEnable.ScalingRuleArisExecuteResultNumberOfAddedInstances.\n\nIf set to Full, no old signal will be deleted unless Count is set. In this mode, WaitCondition.Count should reference a full value, such as the same value with InstanceGroup.MaxAmount. It is recommended to use this mode with Count.\n\nDefault to Full.",
      "AllowedValues": [
        "Increment",
        "Full"
      ],
      "Default": "Full"
    },
    "Count": {
      "Type": "Number",
      "Description": "There are 3 preconditions that make Count taking effect:\n1.Mode is set to Full.\n2.Count >= 0.\n3.The id of signal is not specified. If so, it will be a self-increasing integer started from 1. For example, the id of the first signal is 1, the id of the second signal is 2, and so on.\n\nIf Count takes effect, signals with id > Count will be deleted before update.\nThe default value is -1, which means no effect.\nIt is recommended to quote the same value with WaitCondition.Count.",
      "Default": -1
    }
  },
  "Resources": {
    "WaitConditionHandle": {
      "Type": "ALIYUN::ROS::WaitConditionHandle",
      "Properties": {
        "Mode": {
          "Ref": "Mode"
        },
        "Count": {
          "Ref": "Count"
        }
      }
    }
  },
  "Outputs": {
    "CurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix, which can be used for signalling handle completion or failure.  You can signal success by adding --data-binary '{\"status\": \"SUCCESS\"}' , or signal failure by adding --data-binary '{\"status\": \"FAILURE\"}'",
      "Value": {
        "Fn::GetAtt": [
          "WaitConditionHandle",
          "CurlCli"
        ]
      }
    },
    "WindowsCurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix for Windows, which can be used for signalling handle completion or failure. As Windows does not support curl command, you need to install curl.exe and add it to PATH first. You can signal success by adding --data-binary \"{\\\"status\\\": \\\"SUCCESS\\\"}\" , or signal failure by adding --data-binary \"{\\\"status\\\": \\\"FAILURE\\\"}\" ",
      "Value": {
        "Fn::GetAtt": [
          "WaitConditionHandle",
          "WindowsCurlCli"
        ]
      }
    },
    "Headers": {
      "Description": "HTTP POST Headers used for signalling handle completion or failure.",
      "Value": {
        "Fn::GetAtt": [
          "WaitConditionHandle",
          "Headers"
        ]
      }
    },
    "URL": {
      "Description": "HTTP POST URL used for signalling handle completion or failure.",
      "Value": {
        "Fn::GetAtt": [
          "WaitConditionHandle",
          "URL"
        ]
      }
    },
    "PowerShellCurlCli": {
      "Description": "Convenience attribute, provides curl CLI command prefix for PowerShell, which can be used for signalling handle completion or failure. As this cmdlet was introduced in PowerShell 3.0, ensure the version of PowerShell satisfies the constraint. (Show the version via $PSVersionTable.PSVersion.) You can signal success by adding -Body '{\"status\": \"SUCCESS\"}' , or signal failure by adding -Body '{\"status\": \"FAILURE\"}' ",
      "Value": {
        "Fn::GetAtt": [
          "WaitConditionHandle",
          "PowerShellCurlCli"
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
    Type: String
    Description: >-
      If set to Increment, all old signals will be deleted before update. In
      this mode, WaitCondition.Count should reference an incremental value
      instead of a full value, such as
      ScalingGroupEnable.ScalingRuleArisExecuteResultNumberOfAddedInstances.


      If set to Full, no old signal will be deleted unless Count is set. In this
      mode, WaitCondition.Count should reference a full value, such as the same
      value with InstanceGroup.MaxAmount. It is recommended to use this mode
      with Count.


      Default to Full.
    AllowedValues:
      - Increment
      - Full
    Default: Full
  Count:
    Type: Number
    Description: >-
      There are 3 preconditions that make Count taking effect:

      1.Mode is set to Full.

      2.Count >= 0.

      3.The id of signal is not specified. If so, it will be a self-increasing
      integer started from 1. For example, the id of the first signal is 1, the
      id of the second signal is 2, and so on.


      If Count takes effect, signals with id > Count will be deleted before
      update.

      The default value is -1, which means no effect.

      It is recommended to quote the same value with WaitCondition.Count.
    Default: -1
Resources:
  WaitConditionHandle:
    Type: 'ALIYUN::ROS::WaitConditionHandle'
    Properties:
      Mode:
        Ref: Mode
      Count:
        Ref: Count
Outputs:
  CurlCli:
    Description: >-
      Convenience attribute, provides curl CLI command prefix, which can be used
      for signalling handle completion or failure.  You can signal success by
      adding --data-binary '{"status": "SUCCESS"}' , or signal failure by adding
      --data-binary '{"status": "FAILURE"}'
    Value:
      'Fn::GetAtt':
        - WaitConditionHandle
        - CurlCli
  WindowsCurlCli:
    Description: >-
      Convenience attribute, provides curl CLI command prefix for Windows, which
      can be used for signalling handle completion or failure. As Windows does
      not support curl command, you need to install curl.exe and add it to PATH
      first. You can signal success by adding --data-binary "{\"status\":
      \"SUCCESS\"}" , or signal failure by adding --data-binary "{\"status\":
      \"FAILURE\"}" 
    Value:
      'Fn::GetAtt':
        - WaitConditionHandle
        - WindowsCurlCli
  Headers:
    Description: HTTP POST Headers used for signalling handle completion or failure.
    Value:
      'Fn::GetAtt':
        - WaitConditionHandle
        - Headers
  URL:
    Description: HTTP POST URL used for signalling handle completion or failure.
    Value:
      'Fn::GetAtt':
        - WaitConditionHandle
        - URL
  PowerShellCurlCli:
    Description: >-
      Convenience attribute, provides curl CLI command prefix for PowerShell,
      which can be used for signalling handle completion or failure. As this
      cmdlet was introduced in PowerShell 3.0, ensure the version of PowerShell
      satisfies the constraint. (Show the version via
      $PSVersionTable.PSVersion.) You can signal success by adding -Body
      '{"status": "SUCCESS"}' , or signal failure by adding -Body '{"status":
      "FAILURE"}' 
    Value:
      'Fn::GetAtt':
        - WaitConditionHandle
        - PowerShellCurlCli
```


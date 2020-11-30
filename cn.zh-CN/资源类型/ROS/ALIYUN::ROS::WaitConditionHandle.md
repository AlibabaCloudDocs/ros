# ALIYUN::ROS::WaitConditionHandle

ALIYUN::ROS::WaitConditionHandle用于创建在自定义数据执行过程中发送消息和接收消息的实例。

## 语法

```
{
  "Type": "ALIYUN::ROS::WaitConditionHandle",
  "Properties": {
    "Count": Integer, 
    "Mode": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Count|Integer|否|是|准备接收的消息总数。|默认值：-1。|
|Mode|String|否|是|模式。|取值范围：

-   Increment：所有旧信号将在更新前被删除。在这种模式下，Count应该引用一个增量值而不是一个完整值。
-   Full（默认值）：不会删除任何旧信号，除非设置了Count。在这种模式下，Count应该引用一个完整值。 |

## 返回值

Fn::GetAtt

-   CurlCli：该资源产生的curl命令。通过该命令发送自定义数据执行的结果或者状态到资源编排服务。
-   WindowsCurlCli：为Windows提供curl CLI命令前缀，可用于发出处理完成或失败的信号。由于Windows不支持curl命令，您需要先安装curl.exe并将其添加到PATH中。您可以通过添加`--data-binary "{\"status\": \" success \"}`表示成功、添加`--data-binary "{\"status\": \" failure \"}`表示失败。
-   PowerShellCurlCli：为PowerShell提供curl CLI命令前缀，可用于发出信号处理完成或失败。因为这个cmdlet是在PowerShell 3.0中引入的，所以要确保PowerShell的版本满足此约束。通过`$PSVersionTable.PSVersion`可以显示版本。您可以通过添加`-Body '{"status": " success "}`表示成功、添加`-Body '{"status": " failure "}`表示失败。
-   Headers：用于发信号通知成功或失败的HTTP POST请求头。
-   URL：用于发信号通知成功或失败的HTTP POST请求地址。

## 示例

`JSON`格式

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

`YAML`格式

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


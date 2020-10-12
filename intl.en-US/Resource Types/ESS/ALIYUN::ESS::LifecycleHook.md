# ALIYUN::ESS::LifecycleHook

ALIYUN::ESS::LifecycleHook is used to create a lifecycle hook for a scaling group.

## Syntax

```
{
  "Type": "ALIYUN::ESS::LifecycleHook",
  "Properties": {
    "LifecycleHookName": String,
    "NotificationArn": String,
    "HeartbeatTimeout": Integer,
    "NotificationMetadata": String,
    "ScalingGroupId": String,
    "DefaultResult": String,
    "LifecycleTransition": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|LifecycleHookName|String|No|Yes|The name of the lifecycle hook. Each name must be unique within a scaling group.|The name must be 2 to 40 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

The default value is the ID of the lifecycle hook. |
|NotificationArn|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the notification receiver that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook.|This receiver can be an OOS template, MNS queue, or MNS topic. Format: `acs:ess:{region}:{account-id}:{resource-relative-id}`. -   `region`: the region in which the scaling group is deployed.
-   `account-id`: the ID of the Alibaba Cloud account.

Examples:

-   MNS queue: `acs:ess:{region}:{account-id}:queue/{queuename}`
-   MNS topic: `acs:ess:{region}:{account-id}:topic/{topicname}`
-   OOS template: `acs:ess:{region}:{account-id}:oos/{template_name}` |
|HeartbeatTimeout|Integer|No|Yes|The waiting period before the lifecycle hook times out. When the lifecycle hook times out, the scaling group performs the action specified by the DefaultResult parameter. Unit: seconds. After you create a lifecycle hook, you can call the [RecordLifecycleActionHeartbeat](/intl.en-US/API Reference/Lifecycle Hook/RecordLifecycleActionHeartbeat.md) operation to extend the timeout period and keep the ECS instance in the wait state. You can also call the [CompleteLifecycleAction](/intl.en-US/API Reference/Lifecycle Hook/CompleteLifecycleAction.md) operation to terminate the wait state of a scaling activity.|Valid values: 30 to 21600. Unit: seconds.

Default value: 600. |
|NotificationMetadata|String|No|Yes|The fixed string that you want to include when Auto Scaling sends a message about the wait state of a scaling activity to the notification receiver.|The string can be up to 128 characters in length. Auto Scaling sends the specified `NotificationMetadata` parameter value along with the notification message so that you can easily categorize your notifications. The `NotificationMetadata` parameter takes effect only when you specify the `NotificationArn` parameter. |
|ScalingGroupId|String|Yes|No|The ID of the scaling group.|None|
|DefaultResult|String|No|Yes|The action that the scaling group takes when the lifecycle hook times out.

If the scaling group has multiple lifecycle hooks and one of them is terminated when `DefaultResult` is set to ABANDON during a `scale-in` event, the remaining lifecycle hooks within the same scaling group are also terminated. Otherwise, the scaling activity proceeds normally after the wait period times out and continues with the action specified by the DefaultResult parameter.|Default value: CONTINUE. Valid values: -   CONTINUE: The scaling group continues to respond to a scale-in or scale-out event.
-   ABANDON: The scaling group releases the created ECS instances if the scaling activity type is scale-out or removes the ECS instances to be scaled in if the scaling activity type is scale-in. |
|LifecycleTransition|String|Yes|Yes|The type of scaling activity to which the lifecycle hook applies.|Valid values: -   SCALE\_OUT: scale-out events of the scaling group
-   SCALE\_IN: scale-in events of the scaling group |

## Response parameters

Fn::GetAtt

LifecycleHookId: the ID of the lifecycle hook.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "LifecycleHookName": {
      "Type": "String",
      "Description": "The name of the lifecycle hook. Each name must be unique within a scaling group. The name must be 2 to 40 characters in length and can contain letters, numbers, Chinese characters, and special characters including underscores (_), hyphens (-) and periods (.).\nDefault value: Lifecycle Hook ID",
      "AllowedPattern": "^[a-zA-Z0-9\\u4e00-\\u9fa5][-_.a-zA-Z0-9\\u4e00-\\u9fa5]{1,63}$"
    },
    "NotificationArn": {
      "Type": "String",
      "Description": "The Alibaba Cloud Resource Name (ARN) of the notification target that Auto Scaling will use to notify you when an instance is in the transition state for the lifecycle hook. This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:{region}:{account-id}:{resource-relative-id}.\nregion: the region to which the scaling group locates\naccount-id: Alibaba Cloud ID\nFor example:\nMNS queue: acs:ess:{region}:{account-id}:queue/{queuename}\nMNS topic: acs:ess:{region}:{account-id}:topic/{topicname}\nOOS template: acs:ess:{region}:{account-id}:oos/{templatename}",
      "AllowedPattern": "^acs:ess:([a-zA-Z0-9-]+):(\\d+):(queue|topic|oos)/([a-zA-Z0-9][-_a-zA-Z0-9]{0,255})$",
      "MaxLength": 300
    },
    "ScalingGroupId": {
      "Type": "String",
      "Description": "The ID of the scaling group."
    },
    "LifecycleTransition": {
      "Type": "String",
      "Description": "The scaling activities to which lifecycle hooks apply Value range:\n SCALE_OUT: scale-out event\n SCALE_IN: scale-in event",
      "AllowedValues": [
        "SCALE_OUT",
        "SCALE_IN"
      ]
    },
    "HeartbeatTimeout": {
      "Type": "Number",
      "Description": "The time, in seconds, that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action (DefaultResult). The range is from 30 to 21,600 seconds. The default value is 600 seconds.\nYou can prevent the lifecycle hook from timing out by calling the RecordLifecycleActionHeartbeat operation. You can also terminate the lifecycle action by calling the CompleteLifecycleAction operation.",
      "MinValue": 30,
      "MaxValue": 21600
    },
    "NotificationMetadata": {
      "Type": "String",
      "Description": "The fixed string that you want to include when Auto Scaling sends a message about the wait state of the scaling activity to the notification target. The length of the parameter can be up to 256 characters. Auto Scaling will send the specified NotificationMetadata parameter along with the notification message so that you can easily categorize your notifications. The NotificationMetadata parameter will only take effect after you specify the NotificationArn parameter.",
      "MaxLength": 256
    },
    "DefaultResult": {
      "Type": "String",
      "Description": "The action that the scaling group takes when the lifecycle hook times out. Value range:\n CONTINUE: the scaling group continues with the scale-in or scale-out process.\n ABANDON: the scaling group stops any remaining action of the scale-in or scale-out event.\nDefault value: CONTINUE\nIf the scaling group has multiple lifecycle hooks and one of them is terminated by the DefaultResult=ABANDON parameter during a scale-in event (SCALE_IN), the remaining lifecycle hooks under the same scaling group will also be terminated. Otherwise, the action following the wait state is the next action, as specified in the parameter DefaultResult, after the last lifecycle event under the same scaling group.",
      "AllowedValues": [
        "CONTINUE",
        "ABANDON"
      ]
    }
  },
  "Resources": {
    "LifecycleHook": {
      "Type": "ALIYUN::ESS::LifecycleHook",
      "Properties": {
        "LifecycleHookName": {
          "Ref": "LifecycleHookName"
        },
        "NotificationArn": {
          "Ref": "NotificationArn"
        },
        "ScalingGroupId": {
          "Ref": "ScalingGroupId"
        },
        "LifecycleTransition": {
          "Ref": "LifecycleTransition"
        },
        "HeartbeatTimeout": {
          "Ref": "HeartbeatTimeout"
        },
        "NotificationMetadata": {
          "Ref": "NotificationMetadata"
        },
        "DefaultResult": {
          "Ref": "DefaultResult"
        }
      }
    }
  },
  "Outputs": {
    "LifecycleHookId": {
      "Description": "The lifecycle hook ID",
      "Value": {
        "Fn::GetAtt": [
          "LifecycleHook",
          "LifecycleHookId"
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
  LifecycleHookName:
    Type: String
    Description: >-
      The name of the lifecycle hook. Each name must be unique within a scaling
      group. The name must be 2 to 40 characters in length and can contain
      letters, numbers, Chinese characters, and special characters including
      underscores (_), hyphens (-) and periods (.).

      Default value: Lifecycle Hook ID
    AllowedPattern: '^[a-zA-Z0-9\u4e00-\u9fa5][-_.a-zA-Z0-9\u4e00-\u9fa5]{1,63}$'
  NotificationArn:
    Type: String
    Description: >-
      The Alibaba Cloud Resource Name (ARN) of the notification target that Auto
      Scaling will use to notify you when an instance is in the transition state
      for the lifecycle hook. This target can be either an MNS queue or an MNS
      topic. The format of the parameter value is
      acs:ess:{region}:{account-id}:{resource-relative-id}.

      region: the region to which the scaling group locates

      account-id: Alibaba Cloud ID

      For example:

      MNS queue: acs:ess:{region}:{account-id}:queue/{queuename}

      MNS topic: acs:ess:{region}:{account-id}:topic/{topicname}

      OOS template: acs:ess:{region}:{account-id}:oos/{templatename}
    AllowedPattern: >-
      ^acs:ess:([a-zA-Z0-9-]+):(\d+):(queue|topic|oos)/([a-zA-Z0-9][-_a-zA-Z0-9]{0,255})$
    MaxLength: 300
  ScalingGroupId:
    Type: String
    Description: The ID of the scaling group.
  LifecycleTransition:
    Type: String
    Description: |-
      The scaling activities to which lifecycle hooks apply Value range:
       SCALE_OUT: scale-out event
       SCALE_IN: scale-in event
    AllowedValues:
      - SCALE_OUT
      - SCALE_IN
  HeartbeatTimeout:
    Type: Number
    Description: >-
      The time, in seconds, that can elapse before the lifecycle hook times out.
      If the lifecycle hook times out, the scaling group performs the default
      action (DefaultResult). The range is from 30 to 21,600 seconds. The
      default value is 600 seconds.

      You can prevent the lifecycle hook from timing out by calling the
      RecordLifecycleActionHeartbeat operation. You can also terminate the
      lifecycle action by calling the CompleteLifecycleAction operation.
    MinValue: 30
    MaxValue: 21600
  NotificationMetadata:
    Type: String
    Description: >-
      The fixed string that you want to include when Auto Scaling sends a
      message about the wait state of the scaling activity to the notification
      target. The length of the parameter can be up to 256 characters. Auto
      Scaling will send the specified NotificationMetadata parameter along with
      the notification message so that you can easily categorize your
      notifications. The NotificationMetadata parameter will only take effect
      after you specify the NotificationArn parameter.
    MaxLength: 256
  DefaultResult:
    Type: String
    Description: >-
      The action that the scaling group takes when the lifecycle hook times out.
      Value range:
       CONTINUE: the scaling group continues with the scale-in or scale-out process.
       ABANDON: the scaling group stops any remaining action of the scale-in or scale-out event.
      Default value: CONTINUE

      If the scaling group has multiple lifecycle hooks and one of them is
      terminated by the DefaultResult=ABANDON parameter during a scale-in event
      (SCALE_IN), the remaining lifecycle hooks under the same scaling group
      will also be terminated. Otherwise, the action following the wait state is
      the next action, as specified in the parameter DefaultResult, after the
      last lifecycle event under the same scaling group.
    AllowedValues:
      - CONTINUE
      - ABANDON
Resources:
  LifecycleHook:
    Type: 'ALIYUN::ESS::LifecycleHook'
    Properties:
      LifecycleHookName:
        Ref: LifecycleHookName
      NotificationArn:
        Ref: NotificationArn
      ScalingGroupId:
        Ref: ScalingGroupId
      LifecycleTransition:
        Ref: LifecycleTransition
      HeartbeatTimeout:
        Ref: HeartbeatTimeout
      NotificationMetadata:
        Ref: NotificationMetadata
      DefaultResult:
        Ref: DefaultResult
Outputs:
  LifecycleHookId:
    Description: The lifecycle hook ID
    Value:
      'Fn::GetAtt':
        - LifecycleHook
        - LifecycleHookId
```


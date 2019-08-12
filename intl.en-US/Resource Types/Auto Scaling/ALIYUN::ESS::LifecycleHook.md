# ALIYUN::ESS::LifecycleHook {#concept_cjh_k11_rgb .concept}

ALIYUN::ESS::LifecycleHook is used to create a lifecycle hook for a scaling group.

## Syntax {#section_xxx_ff1_mfb .section}

```language-json
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

## Properties {#section_gmr_gf1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|LifecycleHookName|String|No|Yes|The name of the lifecycle hook. Each name must be unique within a scaling group.| The name must be 2 to 40 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

 The default value is the ID of the lifecycle hook.

 |
|NotificationArn|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the notification target that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook.|This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.-   `region`: the region where the scaling group resides.
-   `account-id`: the Alibaba Cloud account ID.

Examples:

-   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

|
|HeartbeatTimeout|Integer|No|Yes|The time that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](https://partners-intl.aliyun.com/help/doc-detail/73846.htm) operation. You can also terminate the lifecycle action by calling the [CompleteLifecycleAction](https://partners-intl.aliyun.com/help/doc-detail/73847.htm) operation.| Valid values: 30 to 21,600. Unit: second.

 Default value: 600.

 |
|NotificationMetadata|String|No|Yes|The fixed string that you want to include when Auto Scaling sends a message about the wait state of a scaling activity to the notification target.

Auto Scaling sends the specified `NotificationMetadata` parameter value along with the notification message so that you can easily categorize your notifications. The `NotificationMetadata` parameter is applicable only after you set the `NotificationArn` parameter.|The parameter value must be 1 to 128 characters in length.|
|ScalingGroupId|String|Yes|No|The ID of the scaling group.|None|
|DefaultResult|String|No|Yes|The action that the scaling group takes when the lifecycle hook times out.

If the scaling group has multiple lifecycle hooks and one of them is terminated by the `DefaultResult=ABANDON` parameter during a scale-in event \(`SCALE_IN`\), the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the action following the wait state is the next action, as specified in the DefaultResult parameter, after the last lifecycle event in the same scaling group.|Valid values:-   CONTINUE: The scaling group continues the scale-in or scale-out process.
-   ABANDON: The scaling group stops any remaining actions of the scale-in or scale-out event.

Default value: CONTINUE.

|
|LifecycleTransition|String|Yes|Yes|The type of a scaling activity to which the lifecycle hook applies.|Valid values:-   SCALE\_OUT: scale-out event
-   SCALE\_IN: scale-in event

|

## Response parameters {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

-   LifecycleHookId: the ID of the lifecycle hook.

## Examples {#section_mmh_mf1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "LifecycleHookName": {
      "Type": "String",
      "Description": "The name of the lifecycle hook. Each name must be unique within a scaling group. The name must be 2 to 40 characters in length and can contain letters, digits, underscores (_), hyphens (-), and periods (.). It must start with a letter or digit.
      "AllowedPattern": "^[a-zA-Z0-9\\u4e00-\\u9fa5][-_.a-zA-Z0-9\\u4e00-\\u9fa5]{1,63}$"
    },
    "NotificationArn": {
      "Type": "String",
      "Description": "The Alibaba Cloud Resource Name (ARN) of the notification target that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook. This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:{region}:{account-id}:{resource-relative-id}.\nregion: the region where the scaling group resides\naccount-id: the Alibaba Cloud account ID\nFor example:\nMNS queue: acs:ess:{region}:{account-id}:queue/{queuename}\nMNS topic: acs:ess:{region}:{account-id}:topic/{topicname}",
      "AllowedPattern": "^acs:ess:([a-zA-Z0-9-]+):(\\d+):(queue|topic)/([a-zA-Z0-9][a-zA-Z0-9-]{0,255})$",
      "MaxLength": "100",
    },
    "ScalingGroupId": {
      "Type": "String",
      "Description": "The ID of the scaling group."
    },
    "LifecycleTransition": {
      "Type": "String",
      "Description": "The type of a scaling activity to which the lifecycle hook applies Valid values:\n SCALE_OUT: scale-out event\n SCALE_IN: scale-in event",
      "AllowedValues": [
        "SCALE_OUT",
        "SCALE_IN"
      ]
    },
    "HeartbeatTimeout": {
      "Type": "Number",
      "Description": "The time that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action (DefaultResult). The range is from 30 to 21,600 seconds. The default value is 600 seconds.\nYou can prevent the lifecycle hook from timing out by calling the RecordLifecycleActionHeartbeat operation. You can also terminate the lifecycle action by calling the CompleteLifecycleAction operation.",
      "MinValue": 30,
      "MaxValue": 21600
    },
    "NotificationMetadata": {
      "Type": "String",
      "Description": "The fixed string that you want to include when Auto Scaling sends a message about the wait state of a scaling activity to the notification target. The parameter value must be 1 to 128 characters in length. Auto Scaling sends the specified NotificationMetadata parameter value along with the notification message so that you can easily categorize your notifications. The NotificationMetadata parameter is applicable only after you set the NotificationArn parameter.",
      "MaxLength": 128
    },
    "DefaultResult": {
      "Type": "String",
      "Description": "The action that the scaling group takes when the lifecycle hook times out. Valid values:\n CONTINUE: The scaling group continues the scale-in or scale-out process.\n ABANDON: The scaling group stops any remaining actions of the scale-in or scale-out event.\n Default value: CONTINUE\n If the scaling group has multiple lifecycle hooks and one of them is terminated by the DefaultResult=ABANDON parameter during a scale-in event (SCALE_IN), the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the action following the wait state is the next action, as specified in the DefaultResult parameter, after the last lifecycle event in the same scaling group.",
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


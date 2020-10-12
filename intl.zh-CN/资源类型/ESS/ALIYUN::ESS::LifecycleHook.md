# ALIYUN::ESS::LifecycleHook

ALIYUN::ESS::LifecycleHook类型用于为一个伸缩组创建生命周期挂钩。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|LifecycleHookName|String|否|是|生命周期挂钩名称，不能与当前伸缩组其他生命周期挂钩重名。|长度为2~40个字符，以数字、英文字母或汉字开头，可包含数字、英文字母、汉字、下划线（\_）、短划线（-）和英文句点（.）。

默认值：生命周期挂钩 ID。 |
|NotificationArn|String|否|是|生命周期挂钩通知对象标识符。|目前支持OOS模板、消息服务MNS队列或主题，参数取值格式：`acs:ess:{region}:{account-id}:{resource-relative-id}`。 -   `region`：伸缩组所在的地域。
-   `account-id`：阿里云账号ID。

例如：

-   MNS队列：`acs:ess:{region}:{account-id}:queue/{queuename}`。
-   MNS主题：`acs:ess:{region}:{account-id}:topic/{topicname}`。
-   OOS模板：`acs:ess:{region}:{account-id}:oos/{template_name}` |
|HeartbeatTimeout|Integer|否|是|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。创建了生命周期挂钩后，您可以调用[RecordLifecycleActionHeartbeat](/intl.zh-CN/API参考/生命周期挂钩/RecordLifecycleActionHeartbeat.md)接口延长ECS实例的等待时间，也可以调用[CompleteLifecycleAction](/intl.zh-CN/API参考/生命周期挂钩/CompleteLifecycleAction.md)接口提前结束伸缩活动的等待状态。|取值范围：30~21600。 单位：秒。

默认值：600。 |
|NotificationMetadata|String|否|是|伸缩活动的等待状态的固定字符串信息。|长度不超过128个字符。 弹性伸缩每次推送消息到通知对象时，会同时发送您预先指定的 `NotificationMetadata`参数值，便于管理和标记不同类别的通知信息。当您同时指定了`NotificationArn`参数时，`NotificationMetadata`参数方可生效。 |
|ScalingGroupId|String|是|否|伸缩组ID。|无|
|DefaultResult|String|否|是|等待状态结束后的下一步动作。

当伸缩组发生弹性收缩活动（`SCALE_IN`）并触发多个生命周期挂钩时，`DefaultResult=ABANDON`的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。|取值： -   CONTINUE（默认值）：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的ECS实例或者直接将弹性收缩活动中的ECS实例从伸缩组移除。 |
|LifecycleTransition|String|是|是|生命周期挂钩适用的伸缩活动类型。|取值： -   SCALE\_OUT：伸缩组弹性扩张活动。
-   SCALE\_IN：伸缩组弹性收缩活动。 |

## 返回值

Fn::GetAtt

LifecycleHookId：生命周期挂钩ID。

## 示例

`JSON`格式

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

`YAML`格式

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


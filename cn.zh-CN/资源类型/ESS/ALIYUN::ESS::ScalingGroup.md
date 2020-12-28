# ALIYUN::ESS::ScalingGroup

ALIYUN::ESS::ScalingGroup类型用于创建伸缩组。伸缩组是具有相同应用场景的ECS实例的集合，创建成功后不会立即生效，需要使用ALIYUN::ESS::ScalingGroupEnable启用伸缩组，才能触发伸缩活动，执行伸缩规则。

## 语法

```
{
  "Type": "ALIYUN::ESS::ScalingGroup",
  "Properties": {
    "MultiAZPolicy": String,
    "DesiredCapacity": Integer,
    "NotificationConfigurations": List,
    "ProtectedInstances": List,
    "LaunchTemplateId": String,
    "LaunchTemplateVersion": String,
    "ScalingGroupName": String,
    "VSwitchIds": List,
    "DefaultCooldown": Integer,
    "MinSize": Integer,
    "GroupDeletionProtection": Boolean,
    "MaxSize": Integer,
    "InstanceId": String,
    "VSwitchId": String,
    "LoadBalancerIds": List,
    "StandbyInstances": List,
    "RemovalPolicys": List,
    "HealthCheckType": String,
    "DBInstanceIds": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MinSize|Integer|是|是|伸缩组内ECS实例个数的最小值。|取值范围：0~1000。

当伸缩组内ECS实例数小于MinSize时，弹性伸缩会自动创建ECS实例。 |
|MaxSize|Integer|是|是|伸缩组内ECS实例个数的最大值。|取值范围：0~1000。

当伸缩组内ECS实例数大于MaxSize时，弹性伸缩会自动移出ECS实例。 |
|ScalingGroupName|String|否|是|伸缩组的显示名称。|长度为2~64个字符。以数字、英文字母或汉字开头，可包含英文字母、汉字、数字、下划线（\_）、短划线（-）和英文句点（.）。 同一账号同一地域内名称唯一。

默认值：ScalingGroupId。|
|LaunchTemplateId|String|否|是|实例启动模板ID，用于指定伸缩组从实例启动模板获取启动配置信息。|无|
|LaunchTemplateVersion|String|否|是|ECS实例启动模板的版本。|取值： -   固定的模板版本号。
-   Default：始终使用模板默认版本。
-   Latest：始终使用模板最新版本。 |
|RemovalPolicys|List|否|是|ECS实例移出伸缩组的策略。|取值： -   OldestInstance（默认值）：移出最早加入伸缩组的ECS实例。
-   NewestInstance：移出最新加入伸缩组的ECS实例。
-   OldestScalingConfiguration（默认值）：移出最早伸缩配置创建的ECS实例。 |
|VSwitchId|String|否|否|交换机ID。|无|
|LoadBalancerIds|List|否|是|负载均衡实例的ID。|取值可以是由多台负载均衡实例ID组成一个JSON数组，最多支持5个ID，ID之间用英文逗号（,）隔开。|
|DefaultCooldown|Integer|否|是|一次伸缩活动（添加或移出ECS实例）结束后的一段冷却时间。|-   取值范围：0~86,400。
-   单位：秒。
-   默认值：300 。

冷却时间内，该伸缩组不执行其它的伸缩活动，仅针对云监控报警任务触发的伸缩活动有效。 |
|DBInstanceIds|List|否|是|云数据库RDS版实例的ID。|取值可以是由多台RDS实例ID组成一个JSON数组，最多支持8个ID，ID之间用英文逗号（,）隔开。|
|VSwitchIds|List|否|否|多个交换机ID。|最多可指定5个交换机ID。当指定VSwitchIds时，将忽略VSwitchId的值。交换机的优先级按照指定顺序依次减小。 当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动选择下一优先级的虚拟交换机创建ECS实例。|
|MultiAZPolicy|String|否|否|多可用区伸缩组ECS实例扩缩容策略。|取值： -   PRIORITY：根据您定义的虚拟交换机扩缩容。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动使用下一优先级的虚拟交换机创建ECS实例。
-   BALANCE：在伸缩组指定的多可用区之间均匀分配ECS实例。
-   COST\_OPTIMIZED：按vCPU单价从低到高进行尝试创建。当伸缩配置设置了抢占式计费方式的多实例规格时，优先创建对应抢占式计费实例。当抢占式计费实例由于库存等原因无法创建时，自动尝试以按量付费的方式创建。 |
|NotificationConfigurations|List|否|是|事件及资源变化通知的配置列表。|更多信息，请参见[NotificationConfigurations属性](#section_ay8_o4w_pba)。|
|ProtectedInstances|List|否|是|伸缩组内处于保护模式的ECS实例个数。|最多支持1000个实例。|
|StandbyInstances|List|否|是|伸缩组内处于备用模式的ECS实例个数。|最多支持1000个实例。|
|HealthCheckType|String|否|是|健康检查类型。|取值： -   ECS
-   NONE |
|GroupDeletionProtection|Boolean|否|是|是否开启伸缩组删除保护。|取值： -   true：开启伸缩组删除保护，此时不能删除该伸缩组。
-   false（默认值）：关闭伸缩组删除保护。 |
|DesiredCapacity|Integer|否|是|伸缩组内ECS实例的期望数量，伸缩组会自动将ECS实例数量维持在期望实例数。|取值大于等于MinSize，小于等于MaxSize。|
|InstanceId|String|否|否|ECS实例的ID。创建伸缩组时，将从指定的实例获取所需的配置信息，并自动创建伸缩配置。|无|

## NotificationConfigurations语法

```
"NotificationConfigurations": [
  {
    "NotificationArn": String,
    "NotificationTypes": List
  }
]  
```

## NotificationConfigurations属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NotificationArn|String|是|否|生命周期挂钩通知对象标识符，支持消息服务MNS队列或主题。|取值格式： -   MNS队列：`acs:ess:{region}:{account-id}:queue/{queuename}`
-   MNS主题：`acs:ess:{region}:{account-id}:topic/{topicname}` |
|NotificationTypes|List|是|否|ESS事件和资源更改通知类型。|无|

## 返回值

Fn::GetAtt

ScalingGroupId：伸缩组的ID。由系统生成，全局唯一。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "Parameter VSwitchIds.N is used to create instance in multiple zones. Parameter VSwitchIds.N has a priority over parameter VSwitchId.\nThe valid range of N is [1, 5], and you can specify at most 5 VSwitches in a VPC.\nThe priority of VSwitches descends from 1 to 5, and 1 indicates the highest priority.\nWhen you fail to create an instance in the zone to which a specified VSwitch belongs, another VSwitch with less priority replaces the specified one automatically.",
      "MinLength": 0,
      "MaxLength": 5
    },
    "InstanceId": {
      "Type": "String",
      "Description": "The ID of the ECS instance from which the scaling group obtains configuration information of the specified instance."
    },
    "NotificationConfigurations": {
      "Type": "Json",
      "Description": "When a scaling event occurs in a scaling group, ESS will send a notification to Cloud Monitor or MNS."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "If you create a VPC scaling group, you must specify the ID of a VSwitch."
    },
    "LoadBalancerIds": {
      "Type": "CommaDelimitedList",
      "Description": "ID list of a Server Load Balancer instance. A Json Array with format: [ \"lb-id0\", \"lb-id1\", ... \"lb-idz\" ], support up to 100 Load Balancer instance.",
      "MaxLength": 100
    },
    "DesiredCapacity": {
      "Type": "Number",
      "Description": "The expected number of ECS instances in a scaling group. The scaling group automatically keeps the number of ECS instances as expected. The number of ECS instances cannot be greater than the value of MaxSize and cannot be less than the value of MinSize."
    },
    "GroupDeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether to enable deletion protection for scaling group.\nDefault to False.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "The ID of the instance launch template from which the scaling group obtains launch configurations."
    },
    "MaxSize": {
      "Type": "Number",
      "Description": "Maximum number of ECS instances in the scaling group. Value range: [0, 1000].",
      "MinValue": 0,
      "MaxValue": 1000
    },
    "ScalingGroupName": {
      "Type": "String",
      "Description": "Name shown for the scaling group, which must contain 2-40 characters (English or Chinese). The name must begin with a number, an upper/lower-case letter or a Chinese character and may contain numbers, \"_\", \"-\" or \".\". The account name is unique in the same region.\nIf this parameter is not specified, the default value is ScalingGroupId.",
      "AllowedPattern": "^[a-zA-Z0-9\\u4e00-\\u9fa5][-_.a-zA-Z0-9\\u4e00-\\u9fa5]{1,63}$"
    },
    "MinSize": {
      "Type": "Number",
      "Description": "Minimum number of ECS instances in the scaling group. Value range: [0, 1000].",
      "MinValue": 0,
      "MaxValue": 1000
    },
    "DefaultCooldown": {
      "Type": "Number",
      "Description": "Default cool-down time (in seconds) of the scaling group. Value range: [0, 86400].\nThe default value is 300s.",
      "MinValue": 0,
      "MaxValue": 86400
    },
    "StandbyInstances": {
      "Type": "CommaDelimitedList",
      "Description": "ECS instances of standby mode in the scaling group.",
      "MaxLength": 1000
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "The version of the instance launch template. Valid values:\nA fixed template version numbe.\nDefault: The default template version is always used.\nLatest: The latest template version is always used."
    },
    "MultiAZPolicy": {
      "Type": "String",
      "Description": "ECS scaling strategy for multi availability zone. Allow value:\n1. PRIORITY: scaling the capacity according to the virtual switch (VSwitchIds.N) you define. ECS instances are automatically created using the next priority virtual switch when the higher priority virtual switch cannot be created in the available zone.\n2. BALANCE: evenly allocate ECS instances between the multiple available zone specified by the scaling group.",
      "AllowedValues": [
        "PRIORITY",
        "BALANCE"
      ]
    },
    "ProtectedInstances": {
      "Type": "CommaDelimitedList",
      "Description": "ECS instances of protected mode in the scaling group.",
      "MaxLength": 1000
    },
    "RemovalPolicys": {
      "Type": "CommaDelimitedList",
      "AllowedValues": [
        "OldestScalingConfiguration",
        "OldestInstance",
        "NewestInstance"
      ],
      "Description": "Policy for removing ECS instances from the scaling group.\nOptional values:\nOldestInstance: removes the first ECS instance attached to the scaling group.\nNewestInstance: removes the first ECS instance attached to the scaling group.\nOldestScalingConfiguration: removes the ECS instance with the oldest scaling configuration.\nDefault values: OldestScalingConfiguration and OldestInstance. You can enter up to two removal policies.",
      "MaxLength": 2
    },
    "DBInstanceIds": {
      "Type": "CommaDelimitedList",
      "Description": "ID list of an RDS instance. A Json Array with format: [ \"rm-id0\", \"rm-id1\", ... \"rm-idz\" ], support up to 100 RDS instance.",
      "MaxLength": 100
    },
    "HealthCheckType": {
      "Type": "String",
      "Description": "The health check type. Allow values is \"ECS\" and \"NONE\", default to \"ECS\".",
      "AllowedValues": [
        "ECS",
        "NONE"
      ]
    }
  },
  "Resources": {
    "ScalingGroup": {
      "Type": "ALIYUN::ESS::ScalingGroup",
      "Properties": {
        "VSwitchIds": {
          "Ref": "VSwitchIds"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "NotificationConfigurations": {
          "Ref": "NotificationConfigurations"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "LoadBalancerIds": {
          "Ref": "LoadBalancerIds"
        },
        "DesiredCapacity": {
          "Ref": "DesiredCapacity"
        },
        "GroupDeletionProtection": {
          "Ref": "GroupDeletionProtection"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "MaxSize": {
          "Ref": "MaxSize"
        },
        "ScalingGroupName": {
          "Ref": "ScalingGroupName"
        },
        "MinSize": {
          "Ref": "MinSize"
        },
        "DefaultCooldown": {
          "Ref": "DefaultCooldown"
        },
        "StandbyInstances": {
          "Ref": "StandbyInstances"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "MultiAZPolicy": {
          "Ref": "MultiAZPolicy"
        },
        "ProtectedInstances": {
          "Ref": "ProtectedInstances"
        },
        "RemovalPolicys": {
          "Ref": "RemovalPolicys"
        },
        "DBInstanceIds": {
          "Ref": "DBInstanceIds"
        },
        "HealthCheckType": {
          "Ref": "HealthCheckType"
        }
      }
    }
  },
  "Outputs": {
    "ScalingGroupId": {
      "Description": "Scaling group Id",
      "Value": {
        "Fn::GetAtt": [
          "ScalingGroup",
          "ScalingGroupId"
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
  VSwitchIds:
    Type: CommaDelimitedList
    Description: >-
      Parameter VSwitchIds.N is used to create instance in multiple zones.
      Parameter VSwitchIds.N has a priority over parameter VSwitchId.

      The valid range of N is [1, 5], and you can specify at most 5 VSwitches in
      a VPC.

      The priority of VSwitches descends from 1 to 5, and 1 indicates the
      highest priority.

      When you fail to create an instance in the zone to which a specified
      VSwitch belongs, another VSwitch with less priority replaces the specified
      one automatically.
    MinLength: 0
    MaxLength: 5
  InstanceId:
    Type: String
    Description: >-
      The ID of the ECS instance from which the scaling group obtains
      configuration information of the specified instance.
  NotificationConfigurations:
    Type: Json
    Description: >-
      When a scaling event occurs in a scaling group, ESS will send a
      notification to Cloud Monitor or MNS.
  VSwitchId:
    Type: String
    Description: 'If you create a VPC scaling group, you must specify the ID of a VSwitch.'
  LoadBalancerIds:
    Type: CommaDelimitedList
    Description: >-
      ID list of a Server Load Balancer instance. A Json Array with format: [
      "lb-id0", "lb-id1", ... "lb-idz" ], support up to 100 Load Balancer
      instance.
    MaxLength: 100
  DesiredCapacity:
    Type: Number
    Description: >-
      The expected number of ECS instances in a scaling group. The scaling group
      automatically keeps the number of ECS instances as expected. The number of
      ECS instances cannot be greater than the value of MaxSize and cannot be
      less than the value of MinSize.
  GroupDeletionProtection:
    Type: Boolean
    Description: |-
      Whether to enable deletion protection for scaling group.
      Default to False.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  LaunchTemplateId:
    Type: String
    Description: >-
      The ID of the instance launch template from which the scaling group
      obtains launch configurations.
  MaxSize:
    Type: Number
    Description: >-
      Maximum number of ECS instances in the scaling group. Value range: [0,
      1000].
    MinValue: 0
    MaxValue: 1000
  ScalingGroupName:
    Type: String
    Description: >-
      Name shown for the scaling group, which must contain 2-40 characters
      (English or Chinese). The name must begin with a number, an
      upper/lower-case letter or a Chinese character and may contain numbers,
      "_", "-" or ".". The account name is unique in the same region.

      If this parameter is not specified, the default value is ScalingGroupId.
    AllowedPattern: '^[a-zA-Z0-9\u4e00-\u9fa5][-_.a-zA-Z0-9\u4e00-\u9fa5]{1,63}$'
  MinSize:
    Type: Number
    Description: >-
      Minimum number of ECS instances in the scaling group. Value range: [0,
      1000].
    MinValue: 0
    MaxValue: 1000
  DefaultCooldown:
    Type: Number
    Description: >-
      Default cool-down time (in seconds) of the scaling group. Value range: [0,
      86400].

      The default value is 300s.
    MinValue: 0
    MaxValue: 86400
  StandbyInstances:
    Type: CommaDelimitedList
    Description: ECS instances of standby mode in the scaling group.
    MaxLength: 1000
  LaunchTemplateVersion:
    Type: String
    Description: |-
      The version of the instance launch template. Valid values:
      A fixed template version numbe.
      Default: The default template version is always used.
      Latest: The latest template version is always used.
  MultiAZPolicy:
    Type: String
    Description: >-
      ECS scaling strategy for multi availability zone. Allow value:

      1. PRIORITY: scaling the capacity according to the virtual switch
      (VSwitchIds.N) you define. ECS instances are automatically created using
      the next priority virtual switch when the higher priority virtual switch
      cannot be created in the available zone.

      2. BALANCE: evenly allocate ECS instances between the multiple available
      zone specified by the scaling group.
    AllowedValues:
      - PRIORITY
      - BALANCE
  ProtectedInstances:
    Type: CommaDelimitedList
    Description: ECS instances of protected mode in the scaling group.
    MaxLength: 1000
  RemovalPolicys:
    Type: CommaDelimitedList
    AllowedValues:
      - OldestScalingConfiguration
      - OldestInstance
      - NewestInstance
    Description: >-
      Policy for removing ECS instances from the scaling group.

      Optional values:

      OldestInstance: removes the first ECS instance attached to the scaling
      group.

      NewestInstance: removes the first ECS instance attached to the scaling
      group.

      OldestScalingConfiguration: removes the ECS instance with the oldest
      scaling configuration.

      Default values: OldestScalingConfiguration and OldestInstance. You can
      enter up to two removal policies.
    MaxLength: 2
  DBInstanceIds:
    Type: CommaDelimitedList
    Description: >-
      ID list of an RDS instance. A Json Array with format: [ "rm-id0",
      "rm-id1", ... "rm-idz" ], support up to 100 RDS instance.
    MaxLength: 100
  HealthCheckType:
    Type: String
    Description: 'The health check type. Allow values is "ECS" and "NONE", default to "ECS".'
    AllowedValues:
      - ECS
      - NONE
Resources:
  ScalingGroup:
    Type: 'ALIYUN::ESS::ScalingGroup'
    Properties:
      VSwitchIds:
        Ref: VSwitchIds
      InstanceId:
        Ref: InstanceId
      NotificationConfigurations:
        Ref: NotificationConfigurations
      VSwitchId:
        Ref: VSwitchId
      LoadBalancerIds:
        Ref: LoadBalancerIds
      DesiredCapacity:
        Ref: DesiredCapacity
      GroupDeletionProtection:
        Ref: GroupDeletionProtection
      LaunchTemplateId:
        Ref: LaunchTemplateId
      MaxSize:
        Ref: MaxSize
      ScalingGroupName:
        Ref: ScalingGroupName
      MinSize:
        Ref: MinSize
      DefaultCooldown:
        Ref: DefaultCooldown
      StandbyInstances:
        Ref: StandbyInstances
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      MultiAZPolicy:
        Ref: MultiAZPolicy
      ProtectedInstances:
        Ref: ProtectedInstances
      RemovalPolicys:
        Ref: RemovalPolicys
      DBInstanceIds:
        Ref: DBInstanceIds
      HealthCheckType:
        Ref: HealthCheckType
Outputs:
  ScalingGroupId:
    Description: Scaling group Id
    Value:
      'Fn::GetAtt':
        - ScalingGroup
        - ScalingGroupId
```


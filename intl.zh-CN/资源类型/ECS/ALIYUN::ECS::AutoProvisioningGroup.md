# ALIYUN::ECS::AutoProvisioningGroup

ALIYUN::ECS::AutoProvisioningGroup类型用于创建弹性供应组。

## 语法

```
{
  "Type": "ALIYUN::ECS::AutoProvisioningGroup",
  "Properties": {
    "SpotInstancePoolsToUseCount": Integer,
    "AutoProvisioningGroupName": String,
    "ValidUntil": String,
    "Description": String,
    "PayAsYouGoAllocationStrategy": String,
    "MaxSpotPrice": Number,
    "LaunchTemplateId": String,
    "DefaultTargetCapacityType": String,
    "SpotInstanceInterruptionBehavior": String,
    "SpotTargetCapacity": String,
    "SpotAllocationStrategy": String,
    "PayAsYouGoTargetCapacity": String,
    "TotalTargetCapacity": String,
    "AutoProvisioningGroupType": String,
    "LaunchTemplateVersion": String,
    "ValidFrom": String,
    "ExcessCapacityTerminationPolicy": String,
    "TerminateInstances": Boolean,
    "TerminateInstancesWithExpiration": Boolean,
    "LaunchTemplateConfig": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SpotInstancePoolsToUseCount|Integer|否|否|表示弹性供应组选择价格最低的实例规格创建实例的数量，在SpotAllocationStrategy为lowest-price时生效。|取值：小于启动模板的扩展设置数量。|
|AutoProvisioningGroupName|String|否|否|弹性供应组的名称。|长度为2~128个字符，必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）或短划线（-）。|
|ValidUntil|String|否|否|弹性供应组的到期时间，和ValidFrom共同确定有效时段。|按照ISO8601标准表示，并使用UTC+0时间，格式为y`yyy-MM-ddTHH:mm:ssZ`。|
|Description|String|否|否|弹性供应组的描述信息。|无|
|PayAsYouGoAllocationStrategy|String|否|否|创建按量付费实例的策略。|取值： -   lowest-price（默认值）：成本优化策略。选择价格最低的实例规格。
-   prioritized：优先级策略。按照LaunchTemplateConfig设定的优先级创建实例。 |
|MaxSpotPrice|Number|否|是|弹性供应组内抢占式实例的最高价格。|同时设置MaxSpotPrice和扩展启动模板MaxPrice时，以最低值为准。|
|LaunchTemplateId|String|是|否|弹性供应组关联的实例启动模板的ID。您可以调用[DescribeLaunchTemplates](/intl.zh-CN/API参考/启动模板/DescribeLaunchTemplates.md)查询可用的实例启动模板。|无|
|DefaultTargetCapacityType|String|否|是|PayAsYouGoTargetCapacity和SpotTargetCapacity之和小于TotalTargetCapacity时，指定差额容量的计费方式。|取值： -   PayAsYouGo：按量付费实例。
-   Spot（默认值）：抢占式实例。 |
|SpotInstanceInterruptionBehavior|String|否|否|停止了超额抢占式实例后的下一步动作。|取值： -   stop（默认值）：保持停止状态。
-   terminate：释放。 |
|SpotTargetCapacity|String|否|是|弹性供应组内，抢占式实例的目标容量。|取值：小于TotalTargetCapacity参数取值。|
|SpotAllocationStrategy|String|否|否|创建抢占式实例的策略。|取值： -   lowest-price（默认值）：成本优化策略。选择价格最低的实例规格。
-   diversified：均衡可用区分布策略。在扩展启动模板指定的可用区内创建实例，均匀分布到各可用区。 |
|PayAsYouGoTargetCapacity|String|否|是|弹性供应组内，按量付费实例的目标容量。|取值：小于TotalTargetCapacity参数取值。|
|TotalTargetCapacity|String|是|是|弹性供应组的目标总容量。|取值（正整数）：总容量必须大于等于PayAsYouGoTargetCapacity（指定的按量付费实例目标容量）和SpotTargetCapacity（指定的抢占式实例目标容量）取值之和。|
|AutoProvisioningGroupType|String|否|否|弹性供应组的交付类型。|取值： -   request：一次性。供应组仅在启动时交付实例集群，调度失败后不再重试。
-   maintain（默认值）：持续供应。供应组在启动时尝试交付实例集群，并监控实时容量，未达到目标容量则尝试继续创建ECS实例。 |
|LaunchTemplateVersion|String|否|否|弹性供应组关联实例启动模板的版本，您可以调用[DescribeLaunchTemplateVersions](/intl.zh-CN/API参考/启动模板/DescribeLaunchTemplateVersions.md)查询可用的实例启动模板版本。|无|
|ValidFrom|String|否|否|弹性供应组的启动时间，和ValidUntil共同确定有效时段。|按照ISO8601标准表示，并使用UTC+0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。|
|ExcessCapacityTerminationPolicy|String|否|是|弹性供应组超过目标总容量时，是否停止超额的抢占式实例。|取值： -   no-termination（默认值）：继续运行。
-   termination：停止。停止后的下一步动作由SpotInstanceInterruptionBehavior指定。 |
|TerminateInstances|Boolean|否|否|删除弹性供应组时，是否释放组内实例。|取值： -   true
-   false（默认值） |
|TerminateInstancesWithExpiration|Boolean|否|是|弹性供应组到期时，是否停止抢占式实例。|取值： -   true：停止。停止后的下一步动作由SpotInstanceInterruptionBehavior指定。
-   false（默认值）：继续运行。 |
|LaunchTemplateConfig|List|否|否|启动模板的扩展设置。|最多支持20个扩展设置。|

## LaunchTemplateConfig 语法

```
"LaunchTemplateConfig": [
  {
    "Priority": Integer,
    "WeightedCapacity": Integer,
    "VSwitchId": String,
    "InstanceType": String,
    "MaxPrice": Integer
  }
]
```

## LaunchTemplateConfig 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Priority|Integer|否|否|扩展启动模板的优先级，取值为0时优先级最高。|取值：大于等于0。|
|WeightedCapacity|Integer|否|否|扩展启动模板中，实例规格的权重。取值越高，单台实例满足计算力需求的能力越大，所需的实例数量越小。|取值：大于0。您可以根据指定实例规格的计算力和集群单节点最低计算力得出权重值。例如：单节点最低计算力为8vCPU、60GiB，则8vCPU、60GiB的实例规格权重可以设置为1；16vCPU、120GiB的实例规格权重可以设置为2。|
|VSwitchId|String|是|否|扩展启动模板中，ECS实例加入的虚拟交换机的ID。扩展模板中启动的ECS实例可用区由虚拟交换机决定。|无|
|InstanceType|String|否|否|扩展启动模板对应的实例规格。|无|
|MaxPrice|Integer|是|否|扩展启动模板中，抢占式实例的价格上限。|无|

## 返回值

Fn::GetAtt

AutoProvisioningGroupId：弹性供应组的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AutoProvisioningGroup": {
      "Type": "ALIYUN::ECS::AutoProvisioningGroup",
      "Properties": {
        "SpotInstancePoolsToUseCount": {
          "Ref": "SpotInstancePoolsToUseCount"
        },
        "AutoProvisioningGroupName": {
          "Ref": "AutoProvisioningGroupName"
        },
        "ValidUntil": {
          "Ref": "ValidUntil"
        },
        "Description": {
          "Ref": "Description"
        },
        "PayAsYouGoAllocationStrategy": {
          "Ref": "PayAsYouGoAllocationStrategy"
        },
        "MaxSpotPrice": {
          "Ref": "MaxSpotPrice"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "DefaultTargetCapacityType": {
          "Ref": "DefaultTargetCapacityType"
        },
        "SpotInstanceInterruptionBehavior": {
          "Ref": "SpotInstanceInterruptionBehavior"
        },
        "SpotTargetCapacity": {
          "Ref": "SpotTargetCapacity"
        },
        "SpotAllocationStrategy": {
          "Ref": "SpotAllocationStrategy"
        },
        "PayAsYouGoTargetCapacity": {
          "Ref": "PayAsYouGoTargetCapacity"
        },
        "TotalTargetCapacity": {
          "Ref": "TotalTargetCapacity"
        },
        "AutoProvisioningGroupType": {
          "Ref": "AutoProvisioningGroupType"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "ValidFrom": {
          "Ref": "ValidFrom"
        },
        "ExcessCapacityTerminationPolicy": {
          "Ref": "ExcessCapacityTerminationPolicy"
        },
        "TerminateInstances": {
          "Ref": "TerminateInstances"
        },
        "TerminateInstancesWithExpiration": {
          "Ref": "TerminateInstancesWithExpiration"
        },
        "LaunchTemplateConfig": {
          "Ref": "LaunchTemplateConfig"
        }
      }
    }
  },
  "Parameters": {
    "SpotInstancePoolsToUseCount": {
      "Type": "Number",
      "Description": "This parameter takes effect when the SpotAllocationStrategy parameter is set to lowest-price. The auto provisioning group selects instance types of the lowest cost to create\ninstances."
    },
    "AutoProvisioningGroupName": {
      "Type": "String",
      "Description": "The name of the auto provisioning group to be created. It must be 2 to 128 characters\nin length. It must start with a letter but cannot start with http:// or https://.\nIt can contain letters, digits, colons (:), underscores (_), and hyphens (-)."
    },
    "ValidUntil": {
      "Type": "String",
      "Description": "The time when the auto provisioning group expires. The period of time between this\npoint in time and the point in time specified by the ValidFrom parameter is the effective time period of the auto provisioning group.\nBy default, an auto provisioning group never expires."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the auto provisioning group."
    },
    "PayAsYouGoAllocationStrategy": {
      "Type": "String",
      "Description": "The scale-out policy for pay-as-you-go instances. Valid values:\nlowest-price: The cost optimization policy the auto provisioning group follows to select instance\ntypes of the lowest cost to create instances.\nprioritized: The priority-based policy the auto provisioning group follows to create instances.\nThe priority of an instance type is specified by the LaunchTemplateConfig.N.Priority parameter.\nDefault value: lowest-price",
      "AllowedValues": [
        "lowest-price",
        "prioritized"
      ]
    },
    "MaxSpotPrice": {
      "Type": "Number",
      "Description": "The global maximum price for preemptible instances in the auto provisioning group.\nIf both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are specified, the maximum price is the lower value of the two."
    },
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "The ID of the instance launch template associated with the auto provisioning group.\nYou can call the DescribeLaunchTemplates operation to query available instance launch templates.\nAn auto provisioning group can be associated with only one instance launch template.\nBut you can configure multiple extended configurations for the launch template through\nthe LaunchTemplateConfig parameter."
    },
    "DefaultTargetCapacityType": {
      "Type": "String",
      "Description": "The type of supplemental instances. When the total value of PayAsYouGoTargetCapacity and SpotTargetCapacity is smaller than the value of TotalTargetCapacity, the auto provisioning group will create instances of the specified type to meet\nthe capacity requirements. Valid values:\nPayAsYouGo: Pay-as-you-go instances.\nSpot: Preemptible instances.\nDefault value: Spot",
      "AllowedValues": [
        "PayAsYouGo",
        "Spot"
      ]
    },
    "SpotInstanceInterruptionBehavior": {
      "Type": "String",
      "Description": "The default behavior after preemptible instances are shut down. Value values:\nstop: stops preemptible instances.\nterminate: releases preemptible instances.\nDefault value: stop",
      "AllowedValues": [
        "stop",
        "terminate"
      ]
    },
    "SpotTargetCapacity": {
      "Type": "String",
      "Description": "The target capacity of preemptible instances in the auto provisioning group."
    },
    "SpotAllocationStrategy": {
      "Type": "String",
      "Description": "The scale-out policy for preemptible instances. Valid values:\nlowest-price: The cost optimization policy the auto provisioning group follows to select instance\ntypes of the lowest cost to create instances.\ndiversified: The distribution balancing policy the auto provisioning group follows to evenly create\ninstances across zones specified in multiple extended template configurations.\nDefault value: lowest-price",
      "AllowedValues": [
        "diversified",
        "lowest-price"
      ]
    },
    "PayAsYouGoTargetCapacity": {
      "Type": "String",
      "Description": "The target capacity of pay-as-you-go instances in the auto provisioning group."
    },
    "TotalTargetCapacity": {
      "Type": "String",
      "Description": "The total target capacity of the auto provisioning group. The target capacity consists\nof the following three parts:\nThe target capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity parameter\nThe target capacity of preemptible instances specified by the SpotTargetCapacity parameter\nThe supplemental capacity besides PayAsYouGoTargetCapacity and SpotTargetCapacity"
    },
    "AutoProvisioningGroupType": {
      "Type": "String",
      "Description": "The type of the auto provisioning group. Valid values:\nrequest: One-time delivery. After the auto provisioning group is started, it only attempts\nto create an instance cluster once. If the cluster fails to be created, the group\ndoes not try again.\nmaintain: The continuous delivery and maintain capacity type. After the auto provisioning group\nis started, it continuously attempts to create and maintain the instance cluster.\nThe auto provisioning group compares the real-time and target capacity of the cluster.\nIf the cluster does not meet the target capacity, the group will create instances\nuntil the cluster meets the target capacity.\nDefault value: maintain",
      "AllowedValues": [
        "maintain",
        "request"
      ]
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "The version of the instance launch template associated with the auto provisioning\ngroup. You can call the DescribeLaunchTemplateVersions operation to query the versions of available instance launch templates."
    },
    "ValidFrom": {
      "Type": "String",
      "Description": "The time when the auto provisioning group is started. The period of time between this\npoint in time and the point in time specified by the ValidUntil parameter is the effective time period of the auto provisioning group.\nBy default, an auto provisioning group is immediately started after creation."
    },
    "ExcessCapacityTerminationPolicy": {
      "Type": "String",
      "Description": "The shutdown policy for excess preemptible instances followed when the capacity of\nthe auto provisioning group exceeds the target capacity. Valid values:\nno-termination: Excess preemptible instances are not shut down.\ntermination: Excess preemptible instances are to be shut down. The action to be performed on these\nshutdown instances is specified by the SpotInstanceInterruptionBehavior parameter.\nDefault value: no-termination",
      "AllowedValues": [
        "no-termination",
        "termination"
      ]
    },
    "TerminateInstances": {
      "Type": "Boolean",
      "Description": "Specifies whether to release instances of the auto provisioning group. Valid values:\ntrue\nfalse\nDefault: false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "TerminateInstancesWithExpiration": {
      "Type": "Boolean",
      "Description": "The shutdown policy for preemptible instances when the auto provisioning group expires.\nValid values:\ntrue: shuts down preemptible instances. The action to be performed on these shutdown instances\nis specified by the SpotInstanceInterruptionBehavior parameter.\nfalse: does not shut down preemptible instances.\nDefault: false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "LaunchTemplateConfig": {
      "Type": "Json",
      "Description": ""
    }
  },
  "Outputs": {
    "AutoProvisioningGroupId": {
      "Description": "The ID of the auto provisioning group.",
      "Value": {
        "Fn::GetAtt": [
          "AutoProvisioningGroup",
          "AutoProvisioningGroupId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  AutoProvisioningGroup:
    Type: 'ALIYUN::ECS::AutoProvisioningGroup'
    Properties:
      SpotInstancePoolsToUseCount:
        Ref: SpotInstancePoolsToUseCount
      AutoProvisioningGroupName:
        Ref: AutoProvisioningGroupName
      ValidUntil:
        Ref: ValidUntil
      Description:
        Ref: Description
      PayAsYouGoAllocationStrategy:
        Ref: PayAsYouGoAllocationStrategy
      MaxSpotPrice:
        Ref: MaxSpotPrice
      LaunchTemplateId:
        Ref: LaunchTemplateId
      DefaultTargetCapacityType:
        Ref: DefaultTargetCapacityType
      SpotInstanceInterruptionBehavior:
        Ref: SpotInstanceInterruptionBehavior
      SpotTargetCapacity:
        Ref: SpotTargetCapacity
      SpotAllocationStrategy:
        Ref: SpotAllocationStrategy
      PayAsYouGoTargetCapacity:
        Ref: PayAsYouGoTargetCapacity
      TotalTargetCapacity:
        Ref: TotalTargetCapacity
      AutoProvisioningGroupType:
        Ref: AutoProvisioningGroupType
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      ValidFrom:
        Ref: ValidFrom
      ExcessCapacityTerminationPolicy:
        Ref: ExcessCapacityTerminationPolicy
      TerminateInstances:
        Ref: TerminateInstances
      TerminateInstancesWithExpiration:
        Ref: TerminateInstancesWithExpiration
      LaunchTemplateConfig:
        Ref: LaunchTemplateConfig
Parameters:
  SpotInstancePoolsToUseCount:
    Type: Number
    Description: >-
      This parameter takes effect when the SpotAllocationStrategy parameter is
      set to lowest-price. The auto provisioning group selects instance types of
      the lowest cost to create

      instances.
  AutoProvisioningGroupName:
    Type: String
    Description: >-
      The name of the auto provisioning group to be created. It must be 2 to 128
      characters

      in length. It must start with a letter but cannot start with http:// or
      https://.

      It can contain letters, digits, colons (:), underscores (_), and hyphens
      (-).
  ValidUntil:
    Type: String
    Description: >-
      The time when the auto provisioning group expires. The period of time
      between this

      point in time and the point in time specified by the ValidFrom parameter
      is the effective time period of the auto provisioning group.

      By default, an auto provisioning group never expires.
  Description:
    Type: String
    Description: The description of the auto provisioning group.
  PayAsYouGoAllocationStrategy:
    Type: String
    Description: >-
      The scale-out policy for pay-as-you-go instances. Valid values:

      lowest-price: The cost optimization policy the auto provisioning group
      follows to select instance

      types of the lowest cost to create instances.

      prioritized: The priority-based policy the auto provisioning group follows
      to create instances.

      The priority of an instance type is specified by the
      LaunchTemplateConfig.N.Priority parameter.

      Default value: lowest-price
    AllowedValues:
      - lowest-price
      - prioritized
  MaxSpotPrice:
    Type: Number
    Description: >-
      The global maximum price for preemptible instances in the auto
      provisioning group.

      If both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters
      are specified, the maximum price is the lower value of the two.
  LaunchTemplateId:
    Type: String
    Description: >-
      The ID of the instance launch template associated with the auto
      provisioning group.

      You can call the DescribeLaunchTemplates operation to query available
      instance launch templates.

      An auto provisioning group can be associated with only one instance launch
      template.

      But you can configure multiple extended configurations for the launch
      template through

      the LaunchTemplateConfig parameter.
  DefaultTargetCapacityType:
    Type: String
    Description: >-
      The type of supplemental instances. When the total value of
      PayAsYouGoTargetCapacity and SpotTargetCapacity is smaller than the value
      of TotalTargetCapacity, the auto provisioning group will create instances
      of the specified type to meet

      the capacity requirements. Valid values:

      PayAsYouGo: Pay-as-you-go instances.

      Spot: Preemptible instances.

      Default value: Spot
    AllowedValues:
      - PayAsYouGo
      - Spot
  SpotInstanceInterruptionBehavior:
    Type: String
    Description: >-
      The default behavior after preemptible instances are shut down. Value
      values:

      stop: stops preemptible instances.

      terminate: releases preemptible instances.

      Default value: stop
    AllowedValues:
      - stop
      - terminate
  SpotTargetCapacity:
    Type: String
    Description: >-
      The target capacity of preemptible instances in the auto provisioning
      group.
  SpotAllocationStrategy:
    Type: String
    Description: >-
      The scale-out policy for preemptible instances. Valid values:

      lowest-price: The cost optimization policy the auto provisioning group
      follows to select instance

      types of the lowest cost to create instances.

      diversified: The distribution balancing policy the auto provisioning group
      follows to evenly create

      instances across zones specified in multiple extended template
      configurations.

      Default value: lowest-price
    AllowedValues:
      - diversified
      - lowest-price
  PayAsYouGoTargetCapacity:
    Type: String
    Description: >-
      The target capacity of pay-as-you-go instances in the auto provisioning
      group.
  TotalTargetCapacity:
    Type: String
    Description: >-
      The total target capacity of the auto provisioning group. The target
      capacity consists

      of the following three parts:

      The target capacity of pay-as-you-go instances specified by the
      PayAsYouGoTargetCapacity parameter

      The target capacity of preemptible instances specified by the
      SpotTargetCapacity parameter

      The supplemental capacity besides PayAsYouGoTargetCapacity and
      SpotTargetCapacity
  AutoProvisioningGroupType:
    Type: String
    Description: >-
      The type of the auto provisioning group. Valid values:

      request: One-time delivery. After the auto provisioning group is started,
      it only attempts

      to create an instance cluster once. If the cluster fails to be created,
      the group

      does not try again.

      maintain: The continuous delivery and maintain capacity type. After the
      auto provisioning group

      is started, it continuously attempts to create and maintain the instance
      cluster.

      The auto provisioning group compares the real-time and target capacity of
      the cluster.

      If the cluster does not meet the target capacity, the group will create
      instances

      until the cluster meets the target capacity.

      Default value: maintain
    AllowedValues:
      - maintain
      - request
  LaunchTemplateVersion:
    Type: String
    Description: >-
      The version of the instance launch template associated with the auto
      provisioning

      group. You can call the DescribeLaunchTemplateVersions operation to query
      the versions of available instance launch templates.
  ValidFrom:
    Type: String
    Description: >-
      The time when the auto provisioning group is started. The period of time
      between this

      point in time and the point in time specified by the ValidUntil parameter
      is the effective time period of the auto provisioning group.

      By default, an auto provisioning group is immediately started after
      creation.
  ExcessCapacityTerminationPolicy:
    Type: String
    Description: >-
      The shutdown policy for excess preemptible instances followed when the
      capacity of

      the auto provisioning group exceeds the target capacity. Valid values:

      no-termination: Excess preemptible instances are not shut down.

      termination: Excess preemptible instances are to be shut down. The action
      to be performed on these

      shutdown instances is specified by the SpotInstanceInterruptionBehavior
      parameter.

      Default value: no-termination
    AllowedValues:
      - no-termination
      - termination
  TerminateInstances:
    Type: Boolean
    Description: >-
      Specifies whether to release instances of the auto provisioning group.
      Valid values:

      true

      false

      Default: false
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  TerminateInstancesWithExpiration:
    Type: Boolean
    Description: >-
      The shutdown policy for preemptible instances when the auto provisioning
      group expires.

      Valid values:

      true: shuts down preemptible instances. The action to be performed on
      these shutdown instances

      is specified by the SpotInstanceInterruptionBehavior parameter.

      false: does not shut down preemptible instances.

      Default: false
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  LaunchTemplateConfig:
    Type: Json
    Description: ''
Outputs:
  AutoProvisioningGroupId:
    Description: The ID of the auto provisioning group.
    Value:
      'Fn::GetAtt':
        - AutoProvisioningGroup
        - AutoProvisioningGroupId
```


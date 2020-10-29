# ALIYUN::ECS::AutoProvisioningGroup

ALIYUN::ECS::AutoProvisioningGroup is used to create an auto provisioning group.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SpotInstancePoolsToUseCount|Integer|No|No|The number of ECS instances to be created. The auto provisioning group selects instance types of the lowest cost to create instances. This parameter takes effect only when the SpotAllocationStrategy parameter is set to lowest-price.|The value of this parameter must be smaller than the number of extended launch template configurations specified by LaunchTemplateConfig.|
|AutoProvisioningGroupName|String|No|No|The name of the auto provisioning group.|The name must be 2 to 128 characters in length and can contain letters, digits, colons\(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|ValidUntil|String|No|No|The time when the auto provisioning group expires. The period of time between this point in time and the point in time specified by the ValidFrom parameter is the effective time period of the auto provisioning group.|Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC.|
|Description|String|No|No|The description of the auto provisioning group.|None|
|PayAsYouGoAllocationStrategy|String|No|No|The scale-out policy for pay-as-you-go instances.|Default value: lowest-price. Valid values: -   lowest-price: the cost optimization policy that the auto provisioning group follows to select instance types of the lowest cost to create instances.
-   prioritized: the priority-based policy that the auto provisioning group follows to create instances. The priority of an instance type is specified by the LaunchTemplateConfig parameter. |
|MaxSpotPrice|Number|No|Yes|The maximum price of preemptible instances in the auto provisioning group.|If both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are specified, the maximum price is the smaller value of the two.|
|LaunchTemplateId|String|Yes|No|The ID of the launch template that is associated with the auto provisioning group. You can call the [DescribeLaunchTemplates](/intl.en-US/API Reference/Launch templates/DescribeLaunchTemplates.md) operation to query available instance launch templates.|None|
|DefaultTargetCapacityType|String|No|Yes|The type of supplemental instances. When the total value of PayAsYouGoTargetCapacity and SpotTargetCapacity is smaller than the value of TotalTargetCapacity, the auto provisioning group creates instances of the specified type to meet the capacity requirements.|Default value: Spot. Valid values: -   PayAsYouGo: pay-as-you-go instances
-   Spot: preemptible instances |
|SpotInstanceInterruptionBehavior|String|No|No|The action to follow after you stop a preemptible instance.|Default value: stop. Valid values: -   stop: retains the stop status.
-   terminate: releases the excess preemptible instances. |
|SpotTargetCapacity|String|No|Yes|The expected capacity of preemptible instances in the auto provisioning group.|The value of this parameter must be smaller than that of the TotalTargetCapacity parameter.|
|SpotAllocationStrategy|String|No|No|The scale-out policy for preemptible instances.|Default value: lowest-price. Valid values: -   lowest-price: the cost optimization policy that the auto provisioning group follows to select instance types of the lowest cost to create instances.
-   diversified: the distribution balancing policy that the auto provisioning group follows to evenly create instances across zones specified in multiple extended template configurations. |
|PayAsYouGoTargetCapacity|String|No|Yes|The expected capacity of pay-as-you-go instances in the auto provisioning group.|The value of this parameter must be smaller than that of the TotalTargetCapacity parameter.|
|TotalTargetCapacity|String|Yes|Yes|The total expected capacity of the auto provisioning group.|Valid values: any non-zero positive integer. The expected capacity of the auto provisioning group must be at least the sum of the capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity parameter and the capacity of preemptible instances specified by the SpotTargetCapacity parameter.|
|AutoProvisioningGroupType|String|No|No|The delivery type of the auto provisioning group.|Default value: maintain. Valid values: -   request: one-time delivery. After the auto provisioning group is started, it attempts to deliver an instance cluster only once. If the cluster fails to be delivered, the group does not retry the operation.
-   maintain: continuous delivery and capacity maintenance. After the auto provisioning group is started, it continuously attempts to create and deliver an instance cluster. The auto provisioning group monitors the real-time capacity. If a gap exists between the real-time capacity and the expected capacity, the auto provisioning group automatically scales in or out to meet the expected capacity. |
|LaunchTemplateVersion|String|No|No|The version of the instance launch template that is associated with the auto provisioning group. You can call the [DescribeLaunchTemplateVersions](/intl.en-US/API Reference/Launch templates/DescribeLaunchTemplateVersions.md) operation to query available versions of instance launch templates.|None|
|ValidFrom|String|No|No|The time when the auto provisioning group is started. The period of time between this point in time and the point in time specified by the ValidUntil parameter is the effective time period of the auto provisioning group.|Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC.|
|ExcessCapacityTerminationPolicy|String|No|Yes|Specifies whether to stop excess preemptible instances when the total expected capacity of the specified auto provisioning group is reached.|Default value: no-termination. Valid values: -   no-termination: Excess preemptible instances are not stopped.
-   termination: Excess preemptible instances are stopped. The action to be performed on these stopped instances is specified by the SpotInstanceInterruptionBehavior parameter. |
|TerminateInstances|Boolean|No|No|Specifies whether to release instances in the auto provisioning group when the auto provisioning group is deleted.|Default value: false. Valid values: -   true
-   false |
|TerminateInstancesWithExpiration|Boolean|No|Yes|Specifies whether to stop preemptible instances when the auto provisioning group expires.|Default value: false. Valid values: -   true: Preemptible instances are stopped. The action to be performed on these stopped instances is specified by the SpotInstanceInterruptionBehavior parameter.
-   false: The preemptible instances are not shut down. |
|LaunchTemplateConfig|List|No|No|The list of one or more extended configurations of the launch template.|A maximum of 20 extended configurations can be specified.|

## LaunchTemplateConfig syntax

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

## LaunchTemplateConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Priority|Integer|No|No|The priority of the instance type specified in extended configurations.|Valid values: 0 or any positive integer.|
|WeightedCapacity|Integer|No|No|The weight of the instance type specified in extended configurations. A greater weight indicates that the instance has more computing power, and as a result fewer instances are required.|Valid values: any non-zero positive integer. The weight is calculated based on the computing power of the specified instance type and the minimum computing power of a single node of the cluster. For example, if the minimum computing power of a single node is 8 vCPUs and 60 GiB, the weight of the instance type that has 8 vCPUs and 60 GiB can be set to 1. The weight of the instance type that has 16 vCPUs and 120 GiB can be set to 2.|
|VSwitchId|String|Yes|No|The ID of the VSwitch in extended configurations. The zone of the ECS instances that are created from the extended configurations is determined by the VSwitch.|None|
|InstanceType|String|No|No|The instance type that is specified in extended configurations.|None|
|MaxPrice|Integer|Yes|No|The maximum price of preemptible instances in extended configurations.|None|

## Response parameters

Fn::GetAtt

AutoProvisioningGroupId: the ID of the auto provisioning group.

## Examples

`JSON` format

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

`YAML` format

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


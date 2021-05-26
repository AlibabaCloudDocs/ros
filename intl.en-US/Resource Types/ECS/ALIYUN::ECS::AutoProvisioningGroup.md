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
    "CheckExecutionStatus": Boolean,
    "LaunchConfiguration": Map
    "LaunchTemplateConfig": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SpotInstancePoolsToUseCount|Integer|No|No|The number of Elastic Compute Service \(ECS\) instances to be created. The auto provisioning group selects instance types of the lowest cost to create instances.|The value of this parameter must be smaller than the number of extended launch template configurations specified by LaunchTemplateConfig. This parameter takes effect only when the SpotAllocationStrategy parameter is set to lowest-price. |
|AutoProvisioningGroupName|String|No|No|The name of the auto provisioning group.|The name must be 2 to 128 characters in length and can contain letters, digits, colons\(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|ValidUntil|String|No|No|The time when the auto provisioning group expires. The period of time between this point in time and the point in time specified by the ValidFrom parameter is the effective time period of the auto provisioning group.|Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC.|
|Description|String|No|No|The description of the auto provisioning group.|None|
|PayAsYouGoAllocationStrategy|String|No|No|The scale-out policy for pay-as-you-go instances.|Default value: lowest-price. Valid values: -   lowest-price: the cost optimization policy that the auto provisioning group follows to select instance types of the lowest cost to create instances.
-   prioritized: the priority-based policy that the auto provisioning group follows to create instances. The priority of an instance type is specified by the LaunchTemplateConfig parameter. |
|MaxSpotPrice|Number|No|Yes|The maximum price of preemptible instances in the auto provisioning group.|If both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are specified, the maximum price is the smaller value of the two.|
|LaunchTemplateId|String|No|No|The ID of the launch template that is associated with the auto provisioning group. You can call the [DescribeLaunchTemplates](/intl.en-US/API Reference/Launch templates/DescribeLaunchTemplates.md) operation to query available instance launch templates.|When both the LaunchConfiguration and LaunchConfiguration parameters are specified, the launch template is preferentially used.|
|DefaultTargetCapacityType|String|No|Yes|The type of supplemental instances. When the total value of PayAsYouGoTargetCapacity and SpotTargetCapacity is smaller than the value of TotalTargetCapacity, the auto provisioning group creates instances of the specified type to meet the capacity requirements.|Default value: Spot. Valid values: -   PayAsYouGo: pay-as-you-go instances
-   Spot: preemptible instances |
|SpotInstanceInterruptionBehavior|String|No|No|The next action to take after the excess preemptible instances are shut down.|Default value: stop. Valid values: -   stop: retains the stop status.
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
-   false: The preemptible instances are not stopped. |
|CheckExecutionStatus|Boolean|No|No|Specifies whether to check the execution status.|Valid values:-   true
-   false |
|LaunchConfiguration|Map|No|No|The launch configurations.|When both the LaunchConfiguration and LaunchConfiguration parameters are specified, the launch template is preferentially used. For more information, see [LaunchConfiguration properties](#section_0iu_0oo_7i4). |
|LaunchTemplateConfig|List|No|No|The list of one or more extended configurations of the launch template.|A maximum of 20 extended configurations can be specified. For more information, see [LaunchTemplateConfig properties](#section_cf0_16o_lmh). |

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
|Priority|Integer|No|No|The priority of the instance type specified in extended configurations. A value of 0 indicates the highest priority.|Valid values: 0 or any positive integer.|
|WeightedCapacity|Integer|No|No|The weight of the instance type specified in extended configurations. A greater weight indicates that the instance has more computing power, and as a result fewer instances are required.|Valid values: any non-zero positive integer. The weight is calculated based on the computing power of the specified instance type and the minimum computing power of a single node of the cluster. For example, if the minimum computing power of a single node is 8 vCPUs and 60 GiB, the weight of the instance type that has 8 vCPUs and 60 GiB can be set to 1. The weight of the instance type that has 16 vCPUs and 120 GiB can be set to 2.|
|VSwitchId|String|Yes|No|The ID of the vSwitch in extended configurations. The zone of the ECS instances that are created from the extended configurations is determined by the vSwitch.|None|
|InstanceType|String|No|No|The instance type that is specified in extended configurations.|None|
|MaxPrice|Integer|No|No|The maximum price of preemptible instances in extended configurations.|None|

## LaunchConfiguration syntax

```
"LaunchConfiguration": {
  "InstanceDescription": String,
  "SystemDiskName": String,
  "RamRoleName": String,
  "SystemDiskCategory": String,
  "SecurityGroupId": String,
  "CreditSpecification": String,
  "HostName": String,
  "SystemDiskDescription": String,
  "InternetMaxBandwidthIn": Integer,
  "SystemDiskPerformanceLevel": String,
  "DataDisk": List,
  "InternetMaxBandwidthOut": Integer,
  "IoOptimized": String,
  "Tag": List,
  "ImageId": String,
  "ResourceGroupId": String,
  "KeyPairName": String,
  "PasswordInherit": Boolean,
  "UserData": String,
  "InstanceName": String,
  "SystemDiskSize": Integer,
  "InternetChargeType": String,
  "SecurityEnhancementStrategy": String
}
```

## LaunchConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|SystemDiskName|String|No|No|The name of the system disk attached to the instance.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|RamRoleName|String|No|No|The RAM role name of the instance.|None|
|SystemDiskCategory|String|No|No|The category of the system disk.|Valid values:-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud: basic disk

For non-I/O optimized instances of retired instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency.|
|SecurityGroupId|String|Yes|No|The ID of the security group to which the instance belongs.|None|
|CreditSpecification|String|No|No|The running mode of the burstable instance.|Valid values:-   Standard: standard mode
-   Unlimited: unlimited mode |
|HostName|String|No|No|The hostname of the instance.|The hostname cannot start or end with a period \(.\) or hyphen \(-\).It cannot contain consecutive periods \(.\) or hyphens \(-\).

-   For Windows instances, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   For instances that run other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate the hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). |
|SystemDiskDescription|String|No|No|The description of the system disk.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Valid values:-   If the outbound public bandwidth is less than or equal to 10 Mbit/s, the valid values of this parameter are 1 to 10, and the default value of this parameter is 10.
-   If the maximum outbound network bandwidth is greater than 10 Mbit/s, the valid values of this parameter are 1 to the InternetMaxBandwidthOut value, and the default value is the InternetMaxBandwidthOut value.

Unit: Mbit/s. |
|SystemDiskPerformanceLevel|String|No|No|The performance level of the ESSD that is used as the system disk.|Default value: PL0. Valid values:-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS. |
|DataDisk|List|No|No|The data disk attached to the instance.|A maximum of 16 data disks can be specified. For more information, see [DataDisk properties](#section_8er_q0e_qbh). |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound public bandwidth.|Valid values: 0 to 100. Default value: 0

Unit: Mbit/s. |
|IoOptimized|String|No|No|Specifies whether the instance is an I/O optimized instance.|Valid values:-   none: The instance to be created is non-I/O optimized.
-   optimized: The instance to be created is I/O optimized. |
|Tag|List|No|No|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see [Tag properties](#section_c89_1b3_g4w). |
|ImageId|String|Yes|No|The ID of the image.|None|
|ResourceGroupId|String|No|No|The ID of the enterprise resource group to which the instance belongs.|None|
|KeyPairName|String|No|No|The name of the key pair.|For Windows instances, this parameter is ignored. This parameter is empty by default.

For Linux instances, the username and password authentication method is disabled by default. |
|PasswordInherit|Boolean|No|No|Specifies whether to use the preset password in the image.|Valid values:-   true: The preset password is used.
-   false: The preset password is not used. |
|UserData|String|No|No|The user data provided to create the instance.|The user data must be encoded in Base64. The maximum size of the raw data is 16 KB.|
|InstanceName|String|No|No|The name of the instance.|The default value of this parameter is the InstanceId value. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), periods \(.\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. |
|SystemDiskSize|Integer|No|No|The size of the system disk.|Valid values: 20 to 500. The size of the system disk must be greater than or equal to that of the image. Default value: 40 or image size.

Unit: GiB. |
|InternetChargeType|String|No|No|The billing method for network usage.|Valid values:-   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic

**Note:** When the pay-by-traffic billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. When resources are insufficient, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the pay-by-bandwidth billing method. |
|SecurityEnhancementStrategy|String|No|No|Specifies whether to enable security enhancement.|Valid values:-   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: disables security enhancement. This value is applicable to all image types. |

## DataDisk syntax

```
"DataDisk": [
  {
    "DiskName": String,
    "Size": Integer,
    "Category": String,
    "Description": String,
    "DeleteWithInstance": Boolean,
    "SnapshotId": String,
    "Encrypted": Boolean,
    "KmsKeyId": String,
    "InternetChargeType": String,
    "PerformanceLevel": String
  }
]
```

## DataDisk properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DiskName|String|No|No|The name of the data disk.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|Size|Integer|No|No|The size of the data disk.|Valid values:-   Valid values when DiskCategory is set to cloud\_efficiency: 20 to 32768.
-   Valid values when DiskCategory is set to cloud\_ssd: 20 to 32768.
-   Valid values when DiskCategory is set to cloud\_essd: 20 to 32768.
-   Valid values when DiskCategory is set to cloud: 5 to 2000.

Unit: GiB. |
|Category|String|No|No|The category of the data disk.|Valid values:-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   cloud: basic disk

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud.|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|DeleteWithInstance|Boolean|No|No|Specifies whether to release the data disk along with the instance.|Default value: true. Valid values:-   true: The data disk is released along with the instance.
-   false: The data disk is not released along with the instance. |
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|If this parameter is specified, the Size parameter is ignored, and the disk is created with the size of the specified snapshot. Use snapshots created after July 15, 2013. Otherwise, an error is returned, and your request is rejected.|
|Encrypted|Boolean|No|No|Specifies whether data disk N is encrypted.|Default value: false. Valid values:-   true: The data disk is encrypted.
-   false: The data disk is not encrypted. |
|KmsKeyId|String|No|No|The ID of the Key Management Service \(KMS\) key corresponding to the data disk.|None|
|InternetChargeType|String|No|No|The billing method for network usage.|Valid values:-   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic

**Note:** When the pay-by-traffic billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. When resources are insufficient, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the pay-by-bandwidth billing method. |
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the data disk.|Default value: PL0. Valid values:-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS. |

## Tag syntax

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tag properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of a tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of a tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   AutoProvisioningGroupId: the ID of the auto provisioning group.
-   AutoProvisioningGroupName: the name of the auto provisioning group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TotalTargetCapacity": {
      "Type": "String",
      "Description": "The total target capacity of the auto provisioning group. The target capacity consists\nof the following three parts:\nThe target capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity parameter\nThe target capacity of preemptible instances specified by the SpotTargetCapacity parameter\nThe supplemental capacity besides PayAsYouGoTargetCapacity and SpotTargetCapacity"
    },
    "AutoProvisioningGroupName": {
      "Type": "String",
      "Description": "The name of the auto provisioning group to be created. It must be 2 to 128 characters\nin length. It must start with a letter but cannot start with http:// or https://.\nIt can contain letters, digits, colons (:), underscores (_), and hyphens (-)."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the auto provisioning group."
    },
    "ExcessCapacityTerminationPolicy": {
      "Type": "String",
      "Description": "The shutdown policy for excess preemptible instances followed when the capacity of\nthe auto provisioning group exceeds the target capacity. Valid values:\nno-termination: Excess preemptible instances are not shut down.\ntermination: Excess preemptible instances are to be shut down. The action to be performed on these\nshutdown instances is specified by the SpotInstanceInterruptionBehavior parameter.\nDefault value: no-termination",
      "AllowedValues": [
        "no-termination",
        "termination"
      ]
    },
    "LaunchTemplateConfig": {
      "Type": "Json",
      "Description": ""
    },
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "The ID of the instance launch template associated with the auto provisioning group.\nYou can call the DescribeLaunchTemplates operation to query available instance launch templates.\nAn auto provisioning group can be associated with only one instance launch template.\nBut you can configure multiple extended configurations for the launch template through\nthe LaunchTemplateConfig parameter."
    },
    "CheckExecutionStatus": {
      "Type": "Boolean",
      "Description": "Whether check execution status. If set true, ROS will check the state of AutoProvisioningGroup to be fulfilled. Otherwise ROS will regard AutoProvisioningGroup create failed.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PayAsYouGoTargetCapacity": {
      "Type": "String",
      "Description": "The target capacity of pay-as-you-go instances in the auto provisioning group."
    },
    "AutoProvisioningGroupType": {
      "Type": "String",
      "Description": "The type of the auto provisioning group. Valid values:\nrequest: One-time delivery. After the auto provisioning group is started, it only attempts\nto create an instance cluster once. If the cluster fails to be created, the group\ndoes not try again.\nmaintain: The continuous delivery and maintain capacity type. After the auto provisioning group\nis started, it continuously attempts to create and maintain the instance cluster.\nThe auto provisioning group compares the real-time and target capacity of the cluster.\nIf the cluster does not meet the target capacity, the group will create instances\nuntil the cluster meets the target capacity.\nDefault value: maintain",
      "AllowedValues": [
        "maintain",
        "request"
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
    "ValidUntil": {
      "Type": "String",
      "Description": "The time when the auto provisioning group expires. The period of time between this\npoint in time and the point in time specified by the ValidFrom parameter is the effective time period of the auto provisioning group.\nBy default, an auto provisioning group never expires."
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
    "DefaultTargetCapacityType": {
      "Type": "String",
      "Description": "The type of supplemental instances. When the total value of PayAsYouGoTargetCapacity and SpotTargetCapacity is smaller than the value of TotalTargetCapacity, the auto provisioning group will create instances of the specified type to meet\nthe capacity requirements. Valid values:\nPayAsYouGo: Pay-as-you-go instances.\nSpot: Preemptible instances.\nDefault value: Spot",
      "AllowedValues": [
        "PayAsYouGo",
        "Spot"
      ]
    },
    "LaunchConfiguration": {
      "Type": "Json",
      "Description": ""
    },
    "SpotInstancePoolsToUseCount": {
      "Type": "Number",
      "Description": "This parameter takes effect when the SpotAllocationStrategy parameter is set to lowest-price. The auto provisioning group selects instance types of the lowest cost to create\ninstances."
    },
    "SpotTargetCapacity": {
      "Type": "String",
      "Description": "The target capacity of preemptible instances in the auto provisioning group."
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "The version of the instance launch template associated with the auto provisioning\ngroup. You can call the DescribeLaunchTemplateVersions operation to query the versions of available instance launch templates."
    },
    "ValidFrom": {
      "Type": "String",
      "Description": "The time when the auto provisioning group is started. The period of time between this\npoint in time and the point in time specified by the ValidUntil parameter is the effective time period of the auto provisioning group.\nBy default, an auto provisioning group is immediately started after creation."
    },
    "MaxSpotPrice": {
      "Type": "Number",
      "Description": "The global maximum price for preemptible instances in the auto provisioning group.\nIf both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are specified, the maximum price is the lower value of the two."
    },
    "SpotAllocationStrategy": {
      "Type": "String",
      "Description": "The scale-out policy for preemptible instances. Valid values:\nlowest-price: The cost optimization policy the auto provisioning group follows to select instance\ntypes of the lowest cost to create instances.\ndiversified: The distribution balancing policy the auto provisioning group follows to evenly create\ninstances across zones specified in multiple extended template configurations.\nDefault value: lowest-price",
      "AllowedValues": [
        "diversified",
        "lowest-price"
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
    "PayAsYouGoAllocationStrategy": {
      "Type": "String",
      "Description": "The scale-out policy for pay-as-you-go instances. Valid values:\nlowest-price: The cost optimization policy the auto provisioning group follows to select instance\ntypes of the lowest cost to create instances.\nprioritized: The priority-based policy the auto provisioning group follows to create instances.\nThe priority of an instance type is specified by the LaunchTemplateConfig.N.Priority parameter.\nDefault value: lowest-price",
      "AllowedValues": [
        "lowest-price",
        "prioritized"
      ]
    }
  },
  "Resources": {
    "AutoProvisioningGroup": {
      "Type": "ALIYUN::ECS::AutoProvisioningGroup",
      "Properties": {
        "TotalTargetCapacity": {
          "Ref": "TotalTargetCapacity"
        },
        "AutoProvisioningGroupName": {
          "Ref": "AutoProvisioningGroupName"
        },
        "Description": {
          "Ref": "Description"
        },
        "ExcessCapacityTerminationPolicy": {
          "Ref": "ExcessCapacityTerminationPolicy"
        },
        "LaunchTemplateConfig": {
          "Ref": "LaunchTemplateConfig"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "CheckExecutionStatus": {
          "Ref": "CheckExecutionStatus"
        },
        "PayAsYouGoTargetCapacity": {
          "Ref": "PayAsYouGoTargetCapacity"
        },
        "AutoProvisioningGroupType": {
          "Ref": "AutoProvisioningGroupType"
        },
        "SpotInstanceInterruptionBehavior": {
          "Ref": "SpotInstanceInterruptionBehavior"
        },
        "ValidUntil": {
          "Ref": "ValidUntil"
        },
        "TerminateInstancesWithExpiration": {
          "Ref": "TerminateInstancesWithExpiration"
        },
        "DefaultTargetCapacityType": {
          "Ref": "DefaultTargetCapacityType"
        },
        "LaunchConfiguration": {
          "Ref": "LaunchConfiguration"
        },
        "SpotInstancePoolsToUseCount": {
          "Ref": "SpotInstancePoolsToUseCount"
        },
        "SpotTargetCapacity": {
          "Ref": "SpotTargetCapacity"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "ValidFrom": {
          "Ref": "ValidFrom"
        },
        "MaxSpotPrice": {
          "Ref": "MaxSpotPrice"
        },
        "SpotAllocationStrategy": {
          "Ref": "SpotAllocationStrategy"
        },
        "TerminateInstances": {
          "Ref": "TerminateInstances"
        },
        "PayAsYouGoAllocationStrategy": {
          "Ref": "PayAsYouGoAllocationStrategy"
        }
      }
    }
  },
  "Outputs": {
    "AutoProvisioningGroupName": {
      "Description": "The name of the auto provisioning group.",
      "Value": {
        "Fn::GetAtt": [
          "AutoProvisioningGroup",
          "AutoProvisioningGroupName"
        ]
      }
    },
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
Parameters:
  AutoProvisioningGroupName:
    Description: 'The name of the auto provisioning group to be created. It must be
      2 to 128 characters

      in length. It must start with a letter but cannot start with http:// or https://.

      It can contain letters, digits, colons (:), underscores (_), and hyphens (-).'
    Type: String
  AutoProvisioningGroupType:
    AllowedValues:
    - maintain
    - request
    Description: 'The type of the auto provisioning group. Valid values:

      request: One-time delivery. After the auto provisioning group is started, it
      only attempts

      to create an instance cluster once. If the cluster fails to be created, the
      group

      does not try again.

      maintain: The continuous delivery and maintain capacity type. After the auto
      provisioning group

      is started, it continuously attempts to create and maintain the instance cluster.

      The auto provisioning group compares the real-time and target capacity of the
      cluster.

      If the cluster does not meet the target capacity, the group will create instances

      until the cluster meets the target capacity.

      Default value: maintain'
    Type: String
  CheckExecutionStatus:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: Whether check execution status. If set true, ROS will check the state
      of AutoProvisioningGroup to be fulfilled. Otherwise ROS will regard AutoProvisioningGroup
      create failed.
    Type: Boolean
  DefaultTargetCapacityType:
    AllowedValues:
    - PayAsYouGo
    - Spot
    Description: 'The type of supplemental instances. When the total value of PayAsYouGoTargetCapacity
      and SpotTargetCapacity is smaller than the value of TotalTargetCapacity, the
      auto provisioning group will create instances of the specified type to meet

      the capacity requirements. Valid values:

      PayAsYouGo: Pay-as-you-go instances.

      Spot: Preemptible instances.

      Default value: Spot'
    Type: String
  Description:
    Description: The description of the auto provisioning group.
    Type: String
  ExcessCapacityTerminationPolicy:
    AllowedValues:
    - no-termination
    - termination
    Description: 'The shutdown policy for excess preemptible instances followed when
      the capacity of

      the auto provisioning group exceeds the target capacity. Valid values:

      no-termination: Excess preemptible instances are not shut down.

      termination: Excess preemptible instances are to be shut down. The action to
      be performed on these

      shutdown instances is specified by the SpotInstanceInterruptionBehavior parameter.

      Default value: no-termination'
    Type: String
  LaunchConfiguration:
    Description: ''
    Type: Json
  LaunchTemplateConfig:
    Description: ''
    Type: Json
  LaunchTemplateId:
    Description: 'The ID of the instance launch template associated with the auto
      provisioning group.

      You can call the DescribeLaunchTemplates operation to query available instance
      launch templates.

      An auto provisioning group can be associated with only one instance launch template.

      But you can configure multiple extended configurations for the launch template
      through

      the LaunchTemplateConfig parameter.'
    Type: String
  LaunchTemplateVersion:
    Description: 'The version of the instance launch template associated with the
      auto provisioning

      group. You can call the DescribeLaunchTemplateVersions operation to query the
      versions of available instance launch templates.'
    Type: String
  MaxSpotPrice:
    Description: 'The global maximum price for preemptible instances in the auto provisioning
      group.

      If both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are
      specified, the maximum price is the lower value of the two.'
    Type: Number
  PayAsYouGoAllocationStrategy:
    AllowedValues:
    - lowest-price
    - prioritized
    Description: 'The scale-out policy for pay-as-you-go instances. Valid values:

      lowest-price: The cost optimization policy the auto provisioning group follows
      to select instance

      types of the lowest cost to create instances.

      prioritized: The priority-based policy the auto provisioning group follows to
      create instances.

      The priority of an instance type is specified by the LaunchTemplateConfig.N.Priority
      parameter.

      Default value: lowest-price'
    Type: String
  PayAsYouGoTargetCapacity:
    Description: The target capacity of pay-as-you-go instances in the auto provisioning
      group.
    Type: String
  SpotAllocationStrategy:
    AllowedValues:
    - diversified
    - lowest-price
    Description: 'The scale-out policy for preemptible instances. Valid values:

      lowest-price: The cost optimization policy the auto provisioning group follows
      to select instance

      types of the lowest cost to create instances.

      diversified: The distribution balancing policy the auto provisioning group follows
      to evenly create

      instances across zones specified in multiple extended template configurations.

      Default value: lowest-price'
    Type: String
  SpotInstanceInterruptionBehavior:
    AllowedValues:
    - stop
    - terminate
    Description: 'The default behavior after preemptible instances are shut down.
      Value values:

      stop: stops preemptible instances.

      terminate: releases preemptible instances.

      Default value: stop'
    Type: String
  SpotInstancePoolsToUseCount:
    Description: 'This parameter takes effect when the SpotAllocationStrategy parameter
      is set to lowest-price. The auto provisioning group selects instance types of
      the lowest cost to create

      instances.'
    Type: Number
  SpotTargetCapacity:
    Description: The target capacity of preemptible instances in the auto provisioning
      group.
    Type: String
  TerminateInstances:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Specifies whether to release instances of the auto provisioning
      group. Valid values:

      true

      false

      Default: false'
    Type: Boolean
  TerminateInstancesWithExpiration:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'The shutdown policy for preemptible instances when the auto provisioning
      group expires.

      Valid values:

      true: shuts down preemptible instances. The action to be performed on these
      shutdown instances

      is specified by the SpotInstanceInterruptionBehavior parameter.

      false: does not shut down preemptible instances.

      Default: false'
    Type: Boolean
  TotalTargetCapacity:
    Description: 'The total target capacity of the auto provisioning group. The target
      capacity consists

      of the following three parts:

      The target capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity
      parameter

      The target capacity of preemptible instances specified by the SpotTargetCapacity
      parameter

      The supplemental capacity besides PayAsYouGoTargetCapacity and SpotTargetCapacity'
    Type: String
  ValidFrom:
    Description: 'The time when the auto provisioning group is started. The period
      of time between this

      point in time and the point in time specified by the ValidUntil parameter is
      the effective time period of the auto provisioning group.

      By default, an auto provisioning group is immediately started after creation.'
    Type: String
  ValidUntil:
    Description: 'The time when the auto provisioning group expires. The period of
      time between this

      point in time and the point in time specified by the ValidFrom parameter is
      the effective time period of the auto provisioning group.

      By default, an auto provisioning group never expires.'
    Type: String
Resources:
  AutoProvisioningGroup:
    Properties:
      AutoProvisioningGroupName:
        Ref: AutoProvisioningGroupName
      AutoProvisioningGroupType:
        Ref: AutoProvisioningGroupType
      CheckExecutionStatus:
        Ref: CheckExecutionStatus
      DefaultTargetCapacityType:
        Ref: DefaultTargetCapacityType
      Description:
        Ref: Description
      ExcessCapacityTerminationPolicy:
        Ref: ExcessCapacityTerminationPolicy
      LaunchConfiguration:
        Ref: LaunchConfiguration
      LaunchTemplateConfig:
        Ref: LaunchTemplateConfig
      LaunchTemplateId:
        Ref: LaunchTemplateId
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      MaxSpotPrice:
        Ref: MaxSpotPrice
      PayAsYouGoAllocationStrategy:
        Ref: PayAsYouGoAllocationStrategy
      PayAsYouGoTargetCapacity:
        Ref: PayAsYouGoTargetCapacity
      SpotAllocationStrategy:
        Ref: SpotAllocationStrategy
      SpotInstanceInterruptionBehavior:
        Ref: SpotInstanceInterruptionBehavior
      SpotInstancePoolsToUseCount:
        Ref: SpotInstancePoolsToUseCount
      SpotTargetCapacity:
        Ref: SpotTargetCapacity
      TerminateInstances:
        Ref: TerminateInstances
      TerminateInstancesWithExpiration:
        Ref: TerminateInstancesWithExpiration
      TotalTargetCapacity:
        Ref: TotalTargetCapacity
      ValidFrom:
        Ref: ValidFrom
      ValidUntil:
        Ref: ValidUntil
    Type: ALIYUN::ECS::AutoProvisioningGroup
Outputs:
  AutoProvisioningGroupId:
    Description: The ID of the auto provisioning group.
    Value:
      Fn::GetAtt:
      - AutoProvisioningGroup
      - AutoProvisioningGroupId
  AutoProvisioningGroupName:
    Description: The name of the auto provisioning group.
    Value:
      Fn::GetAtt:
      - AutoProvisioningGroup
      - AutoProvisioningGroupName
```

For more examples, visit [LaunchTemplate.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/LaunchTemplate.json) and [LaunchTemplate.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/LaunchTemplate.yml). In the examples, the ALIYUN::ECS::LaunchTemplate and ALIYUN::ECS::AutoProvisioningGroup resource types are involved.


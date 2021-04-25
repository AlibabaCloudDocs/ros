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
    "CheckExecutionStatus": Boolean,
    "LaunchConfiguration": Map
    "LaunchTemplateConfig": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SpotInstancePoolsToUseCount|Integer|否|否|弹性供应组选择价格最低的实例规格创建实例的数量。|取值：小于启动模板的扩展设置数量。当SpotAllocationStrategy取值为lowest-price时该参数生效。 |
|AutoProvisioningGroupName|String|否|否|弹性供应组的名称。|长度为2~128个字符，必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。|
|ValidUntil|String|否|否|弹性供应组的到期时间，和ValidFrom共同确定有效时段。|按照ISO8601标准表示，并使用UTC+0时间，格式为y`yyy-MM-ddTHH:mm:ssZ`。|
|Description|String|否|否|弹性供应组的描述信息。|无|
|PayAsYouGoAllocationStrategy|String|否|否|创建按量付费实例的策略。|取值： -   lowest-price（默认值）：成本优化策略。选择价格最低的实例规格。
-   prioritized：优先级策略。按照LaunchTemplateConfig设定的优先级创建实例。 |
|MaxSpotPrice|Number|否|是|弹性供应组内抢占式实例的最高价格。|同时设置MaxSpotPrice和扩展启动模板MaxPrice时，以最低值为准。|
|LaunchTemplateId|String|否|否|弹性供应组关联的实例启动模板的ID。您可以调用[DescribeLaunchTemplates](/intl.zh-CN/API参考/启动模板/DescribeLaunchTemplates.md)查询可用的实例启动模板。|同时指定LaunchTemplateId和LaunchConfiguration时，优先使用启动模板。|
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
|CheckExecutionStatus|Boolean|否|否|是否检查执行状态。|取值：-   true
-   false |
|LaunchConfiguration|Map|否|否|启动配置信息。|同时指定LaunchTemplateId和LaunchConfiguration时，优先使用启动模板。更多信息，请参见[LaunchConfiguration属性](#section_0iu_0oo_7i4)。 |
|LaunchTemplateConfig|List|否|否|启动模板的扩展设置。|最多支持20个扩展设置。更多信息，请参见[LaunchTemplateConfig 属性](#section_cf0_16o_lmh)。 |

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
|MaxPrice|Integer|否|否|扩展启动模板中，抢占式实例的价格上限。|无|

## LaunchConfiguration语法

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

## LaunchConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceDescription|String|否|否|实例描述。|长度为2~256个字符，不能以`http://`和`https://`开头。|
|SystemDiskName|String|否|否|系统盘名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可以包含英文字母、汉字、数字、半角句号（.）、半角冒号（:）、下划线（\_）和短划线（-）。|
|RamRoleName|String|否|否|实例RAM角色名称。|无|
|SystemDiskCategory|String|否|否|系统盘的云盘种类。|取值：-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。
-   cloud：普通云盘。

已停售的实例规格且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。|
|SecurityGroupId|String|是|否|实例所属的安全组ID。|无|
|CreditSpecification|String|否|否|修改突发性能实例的运行模式。|取值：-   Standard：标准模式。
-   Unlimited：无性能约束模式。 |
|HostName|String|否|否|实例主机名称。|半角句号（.）和短划线（-）不能作为首尾字符，更不能连续使用。取值要求如下：

-   Windows实例：长度为2~15个字符，不支持半角句号（.），不能全是数字。可包含英文字母、数字和短划线（-）。
-   其他类型实例（Linux等）：长度为2~64个字符，支持多个半角句号（.），点之间为一段，每段可包含英文字母、数字和短划线（-）。 |
|SystemDiskDescription|String|否|否|系统盘的描述。|长度为2~256个字符，不能以`http://`和`https://`开头。|
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值。|取值：-   当公网出带宽小于等于10Mbps时：1~10，默认为10。
-   当公网出带宽大于10Mbps时：1～InternetMaxBandwidthOut的值，默认为InternetMaxBandwidthOut的值。

单位：Mbps。 |
|SystemDiskPerformanceLevel|String|否|否|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|取值：-   PL0（默认）：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。 |
|DataDisk|List|否|否|数据盘。|最多支持16块数据盘。更多信息，请参见[DataDisk属性](#section_8er_q0e_qbh)。 |
|InternetMaxBandwidthOut|Integer|否|否|公网出带宽最大值。|取值范围：0~100。默认值：0。

单位为Mbps。 |
|IoOptimized|String|否|否|是否为I/O优化实例。|取值：-   none：不是I/O优化实例。
-   optimized：是I/O优化实例。 |
|Tag|List|否|否|实例的标签。|最多20个标签。更多信息，请参见[Tag属性](#section_c89_1b3_g4w)。 |
|ImageId|String|是|否|镜像ID。|无|
|ResourceGroupId|String|否|否|实例所在的企业资源组ID。|无|
|KeyPairName|String|否|否|密钥对名称。|Windows实例，忽略该参数。默认为空。

Linux实例的密码登录方式会被初始化成禁止。 |
|PasswordInherit|Boolean|否|否|是否使用镜像预设的密码。|取值：-   true：使用。
-   false：不使用。 |
|UserData|String|否|否|实例自定义数据。|需要以Base64方式编码，原始数据最多为16 KB。|
|InstanceName|String|否|否|实例名称。|默认值为实例的InstanceId。长度为2~128个字符，必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）、半角句号（.）和短划线（-）。 |
|SystemDiskSize|Integer|否|否|系统盘大小。|取值范围：20~500。必须大于等于镜像大小。默认值：40或镜像大小。

单位：GiB。 |
|InternetChargeType|String|否|否|网络计费类型。|取值：-   PayByBandwidth：按固定带宽计费。
-   PayByTraffic：按使用流量计费。

**说明：** 按使用流量计费模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用按固定带宽计费模式。 |
|SecurityEnhancementStrategy|String|否|否|是否开启安全加固。|取值：-   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。 |

## DataDisk语法

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

## DataDisk属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DiskName|String|否|否|数据盘名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、半角冒号（:）、下划线（\_）和短划线（-）。|
|Size|Integer|否|否|数据盘的容量大小。|取值范围：-   cloud\_efficiency：20~32,768。
-   cloud\_ssd：20~32,768。
-   cloud\_essd：20~32,768。
-   cloud：5~2000。

单位：GiB。 |
|Category|String|否|否|数据盘的云盘类型。|取值：-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。
-   cloud：普通云盘。

对于I/O优化实例，默认值为cloud\_efficiency。对于非I/O优化实例，默认值为cloud。|
|Description|String|否|否|数据盘的描述。|长度为2~256个字符，不能以`http://`和`https://`开头。|
|DeleteWithInstance|Boolean|否|否|数据盘是否随实例释放。|取值：-   true（默认值）：数据盘随实例释放。
-   false：数据盘不随实例释放。 |
|SnapshotId|String|否|否|创建数据盘使用的快照。|指定该参数后，参数Size会被忽略，实际创建的云盘大小为指定的快照的大小。不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。|
|Encrypted|Boolean|否|否|数据盘N是否加密。|取值：-   true：加密。
-   false（默认值）：不加密。 |
|KmsKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|
|InternetChargeType|String|否|否|网络计费类型。|取值：-   PayByBandwidth：按固定带宽计费。
-   PayByTraffic：按使用流量计费。

**说明：** 按使用流量计费模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用按固定带宽计费模式。 |
|PerformanceLevel|String|否|否|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。|取值：-   PL0（默认）：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。 |

## Tag语法

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tag属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   AutoProvisioningGroupId：弹性供应组的ID。
-   AutoProvisioningGroupName：弹性供应组的名称。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建ECS实例启动模板和创建弹性供应组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/LaunchTemplate.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/LaunchTemplate.yml)。


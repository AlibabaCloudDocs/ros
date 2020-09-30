# ALIYUN::ESS::ScalingGroup

ALIYUN::ESS::ScalingGroup is used to create a scaling group. A scaling group is a group of ECS instances that are dynamically scaled based on the configured scenario. A scaling group does not take effect immediately after it is created. You must use ALIYUN::ESS::ScalingGroupEnable to enable the scaling group to trigger scaling rules and execute scaling activities.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MinSize|Integer|Yes|Yes|The minimum number of ECS instances in the scaling group.|Valid values: 0 to 1000.

When the number of ECS instances in the scaling group is smaller than the value of MinSize, Auto Scaling automatically creates ECS instances till the number of instances is equal to the value of MinSize. |
|MaxSize|Integer|Yes|Yes|The maximum number of ECS instances in the scaling group.|Valid values: 0 to 1000.

When the number of ECS instances in the scaling group is greater than the value of MaxSize, Auto Scaling removes ECS instances from the scaling group till the number of instances is equal to the value of MaxSize. |
|ScalingGroupName|String|No|Yes|The display name of the scaling group.|The name must be 2 to 40 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit. The name must be unique to an Alibaba Cloud account in a region.

The default value is the ID of the scaling group.|
|LaunchTemplateId|String|No|Yes|The ID of the instance launch template from which the scaling group obtains launch configurations.|None|
|LaunchTemplateVersion|String|No|Yes|The version of the instance launch template.|Valid values: -   The fixed template version number.
-   Default: The default template version is always used.
-   Latest: The latest template version is always used. |
|RemovalPolicys|List|No|Yes|The policies that are used to remove ECS instances from the scaling group.|Valid values: -   OldestInstance: removes the ECS instance that is added to the scaling group at the earliest point in time.
-   NewestInstance: removes the ECS instance that is added to the scaling group at the latest point in time.
-   OldestScalingConfiguration: removes the ECS instance that is created based on the earliest scaling configuration. |
|VSwitchId|String|No|No|The ID of the VSwitch.|None|
|LoadBalancerIds|List|No|Yes|The ID of the SLB instance.|This value can be a JSON array that contains up to five SLB instance IDs. Separate multiple IDs with commas \(,\).|
|DefaultCooldown|Integer|No|Yes|The cooldown period after a scaling activity is executed. Scaling activities include addition and remove of ECS instances.|-   Valid values: 0 to 86400.
-   Unit: seconds.
-   Default value: 300.

During the cooldown period, the scaling group executes only scaling activities that are triggered by CloudMonitor event-triggered tasks. |
|DBInstanceIds|List|No|Yes|The IDs of ApsaraDB for RDS instances.|This value can be a JSON array that contains up to eight ApsaraDB for RDS instance IDs. Separate multiple IDs with commas \(,\).|
|VSwitchIds|List|No|No|The IDs of VSwitches.|You can specify a maximum of five VSwitch IDs. If you specify this parameter, the VSwitchId parameter is ignored. VSwitches are sorted in descending order of priority. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system uses the VSwitch with the next highest priority to create the ECS instance.|
|MultiAZPolicy|String|No|No|The ECS instance scaling policy for the multi-zone scaling group.|Valid values: -   PRIORITY: ECS instances are scaled based on the specified VSwitch. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system uses the VSwitch with the next highest priority to create the ECS instance.
-   BALANCE: ECS instances are distributed evenly in multiple zones specified in the scaling group.
-   COST\_OPTIMIZED: ECS instances are created based on the unit price of vCPUs, from low to high. Preemptible instances are created first when preemptible instance types are specified for the scaling configuration. Pay-as-you-go instances are created automatically when no preemptible instances are available due to issues such as insufficient ECS resources. |
|NotificationConfigurations|List|No|Yes|The notification configurations for event and resource changes.|For more information, see [NotificationConfigurations properties](#section_ay8_o4w_pba).|
|ProtectedInstances|List|No|Yes|The number of protected ECS instances in the scaling group.|Maximum value: 1000.|
|StandbyInstances|List|No|Yes|The number of ECS instances that are in the standby state in the scaling group.|Maximum value: 1000.|
|HealthCheckType|String|No|Yes|The health check type.|Valid values: -   ECS
-   NONE |
|GroupDeletionProtection|Boolean|No|Yes|Specifies whether to enable deletion protection for the scaling group.|Default value: false. Valid values: -   true: enables deletion protection for the scaling group. In this case, you cannot delete the scaling group.
-   false: disables deletion protection for the scaling group. |
|DesiredCapacity|Integer|No|Yes|The expected number of ECS instances in the scaling group. The scaling group automatically keeps the number of ECS instances at the expected value.|The number of ECS instances must be greater than the value of MinSize and less than the value of MaxSize.|
|InstanceId|String|No|No|The ID of the ECS instance from which the scaling group obtains configuration information of the specified instance.|None|

## NotificationConfigurations syntax

```
"NotificationConfigurations": [
  {
    "NotificationArn": String,
    "NotificationTypes": List
  }
]  
```

## NotificationConfigurations properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NotificationArn|String|Yes|No|The Alibaba Cloud Resource Name \(ARN\) of the notification receiver that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook. This object can be an MNS queue or an MNS topic.|Format: -   MNS queue: `acs:ess:{region}:{account-id}:queue/{queuename}`
-   MNS topic: `acs:ess:{region}:{account-id}:topic/{topicname}` |
|NotificationTypes|List|Yes|No|The types of the notification configurations for ESS event and resource changes.|None|

## Response parameters

Fn::GetAtt

ScalingGroupId: the ID of the scaling group. This ID is a globally unique identifier \(GUID\) generated by the system.

## Examples

`JSON` format

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
      "Description": "Name shown for the scaling group, which must contain 2-40 characters (English or Chinese). The name must begin with a number, an upper/lower-case letter or a Chinese character and may contain numbers, \"_\", \"-\" or \". \". The account name is unique in the same region.\nIf this parameter is not specified, the default value is ScalingGroupId.",
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

`YAML` format

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


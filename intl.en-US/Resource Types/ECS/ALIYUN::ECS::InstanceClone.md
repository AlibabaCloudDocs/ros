# ALIYUN::ECS::InstanceClone

ALIYUN::ECS::InstanceClone is used to clone an ECS instance.

## Syntax

```
{
  "Type": "ALIYUN::ECS::InstanceClone",
  "Properties": {
    "DeletionProtection": Boolean,
    "DiskMappings": List,
    "LoadBalancerIdToAttach": String,
    "Description": String,
    "BackendServerWeight": Integer,
    "Tags": List,
    "SecurityGroupId": String,
    "RamRoleName": String,
    "ImageId": String,
    "ResourceGroupId": String,
    "SpotPriceLimit": String,
    "InstanceChargeType": String,
    "SourceInstanceId": String,
    "Period": Number,
    "SpotStrategy": String,
    "Password": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "ZoneId": String,
    "KeyPairName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the instance belongs.|None|
|SourceInstanceId|String|Yes|No|The ID of the source ECS instance.|The clone operation clones the source ECS instance, including its instance type, image, bandwidth billing method, bandwidth limit, and network type. If the source ECS instance belongs to multiple security groups, the created instances are added only to the first of these security groups.|
|BackendServerWeight|Integer|No|No|The weight that is assigned to the ECS instance in the SLB instance.|Valid values: 0 to 100. Default value: 100. |
|LoadBalancerIdToAttach|String|No|No|The ID of the SLB instance to which the created ECS instance is to be attached.|None|
|Description|String|No|No|The description of the created ECS instance.|The description can be up to 256 characters in length.|
|ImageId|String|No|Yes|The ID of the image that is used to start the created ECS instance. You can use a public image, a custom image, or an Alibaba Cloud Marketplace image.|You can specify a partial public image ID instead of the complete ID. Examples:

-   If you enter ubuntu, the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd
-   If you enter ubuntu\_14, the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd
-   If you enter ubuntu\*14\*32, the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd
-   If you enter ubuntu\_16\_0402\_32, the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd |
|SecurityGroupId|String|No|No|The ID of the security group to which the created ECS instance belongs.|None|
|InstanceName|String|No|No|The name of the created ECS instance.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|Password|String|No|No|The password that is used to log on to the created ECS instance.|The password must be 8 to 30 characters in length.

It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.

Special characters include

```
( ) ' ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? /
```

If you specify this parameter in the API request, you must use HTTPS to secure the API and protect your password. |
|DiskMappings|List|No|No|The data disks to be attached to the created ECS instance.|A maximum of 16 data disks can be attached. For more information, see [DiskMappings properties](#section_y8y_lnw_k29). |
|Tags|List|No|Yes|The custom tags of the created ECS instance.|A maximum of 20 tags can be specified in the `[{"Key":"tagKey","Value":"tagValue"}, {"Key":"tagKey2","Value":"tagValue2"}]` format. For more information, see [Tags properties](#section_yna_hli_1bd). |
|ZoneId|String|No|No|The zone ID of the created ECS instance.|None|
|InstanceChargeType|String|No|No|The billing method of the created ECS instance.|Default value: Postpaid. Valid values: -   Prepaid

**Note:** If you set this parameter to Prepaid, make sure that you have sufficient balance in your account. Otherwise, the instance fails to be created.

-   Postpaid |
|Period|Number|No|No|The billing cycle of the created ECS instance.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.

This parameter is required when the InstanceChargeType parameter is set to Prepaid. This parameter is optional when the InstanceChargeType parameter is set to Postpaid. |
|KeyPairName|String|No|No|The name of the key pair that is used to connect to the created ECS instance.|For Windows instances, this parameter is empty by default.

For Linux instances, the Password parameter still takes effect if this parameter is specified. However, logon by password is disabled, and the value of this parameter is used. |
|RamRoleName|String|No|No|The RAM role name of the created ECS instance.|For more information, see [CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md) and [ListRoles](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/ListRoles.md).|
|SpotPriceLimit|String|No|No|The maximum hourly price of the created ECS instance.|This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit. Three decimal places are allowed at most.|
|SpotStrategy|String|No|No|The bidding policy for pay-as-you-go instances.|This parameter takes effect only when the InstanceChargeType parameter is set to PostPaid. Default value: NoSpot. Valid values: -   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with a maximum hourly price.
-   SpotAsPriceGo: applies to pay-as-you-go instances priced at the market price at the time of purchase. |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Valid values: 1 to 200. Unit: Mbit/s. |
|DeletionProtection|Boolean|No|No|The deletion protection property of the created ECS instance. It specifies whether the instance can be released by using the ECS console or by calling the [DeleteInstance](/intl.en-US/API Reference/Instances/DeleteInstance.md) operation.|Valid values: -   true
-   false |

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Device": String,
    "SnapshotId": String,
    "PerformanceLevel": String,
    "Size": String
  }
]
```

## DiskMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Size|String|Yes|No|The size of the data disk.|Valid values: 20 to 500. Unit: GB. |
|Category|String|No|No|The type of the data disk.|-   cloud: basic disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud\_efficiency: ultra disk
-   ephemeral\_ssd: local SSD

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud.|
|DiskName|String|No|No|The name of the data disk.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), colons \(:\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the system disk.|-   Default value: PL1. Valid values: PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. This parameter is empty by default. |
|Device|String|No|No|The mount point of the data disk.|**Note:** This parameter is about to be removed. We recommend that you use other parameters to ensure future compatibility. |
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|None|

## Tags syntax

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance. The instance ID is a globally unique identifier \(GUID\) generated by the system for the instance.
-   PrivateIp: the private IP address of the VPC-type instance. This parameter takes effect only when the NetworkType parameter is set to VPC.
-   InnerIp: the private IP address of the classic network-type instance. This parameter takes effect only when the NetworkType parameter is set to Classic.
-   PublicIp: the public IP address of the classic network-type instance. This parameter takes effect only when the NetworkType parameter is set to Classic.
-   ZoneId: the zone ID of the instance.
-   HostName: the hostname of the instance.
-   PrimaryNetworkInterfaceId: the ID of the primary elastic network interface \(ENI\).

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "BackendServerWeight": {
      "Type": "Number",
      "Description": "The weight of backend server of load balancer. From 0 to 100, 0 means offline. Default is 100.",
      "MinValue": 0,
      "MaxValue": 100,
      "Default": 100
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.",
      "MaxLength": 16
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60. Default value is 1.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36,
        48,
        60
      ],
      "Default": 1
    },
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether an instance can be released manually through the console or API, deletion protection only support postPaid instance ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source ecs instance used to copy properties to clone new ecs instance. It will copy the InstanceType, ImageId, InternetChargeType, InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and data disk configurations. If the instance network is VPC, it will also clone the relative properties. If specified instance with more than one security group, it will use the first security group to create instance. you can also specify the SecurityGroupId to override it."
    },
    "LoadBalancerIdToAttach": {
      "Type": "String",
      "Description": "After the instance is created. Automatic attach it to the load balancer."
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SpotPriceLimit": {
      "Type": "String",
      "Description": "The hourly price threshold of a instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Three decimals is allowed at most. "
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "SpotStrategy": {
      "Type": "String",
      "Description": "The spot strategy of a Pay-As-You-Go instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Value range: \"NoSpot: A regular Pay-As-You-Go instance\", \"SpotWithPriceLimit: A price threshold for a spot instance, \"\"SpotAsPriceGo: A price that is based on the highest Pay-As-You-Go instance. \"Default value: NoSpot.",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    }
  },
  "Resources": {
    "InstanceClone": {
      "Type": "ALIYUN::ECS::InstanceClone",
      "Properties": {
        "BackendServerWeight": {
          "Ref": "BackendServerWeight"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "DeletionProtection": {
          "Ref": "DeletionProtection"
        },
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
        },
        "LoadBalancerIdToAttach": {
          "Ref": "LoadBalancerIdToAttach"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  },
  "Outputs": {
    "PrimaryNetworkInterfaceId": {
      "Description": "Primary network interface id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "PrimaryNetworkInterfaceId"
        ]
      }
    },
    "InnerIp": {
      "Description": "Inner IP address of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "InnerIp"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "ZoneId"
        ]
      }
    },
    "InstanceId": {
      "Description": "The instance id of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "InstanceId"
        ]
      }
    },
    "PrivateIp": {
      "Description": "Private IP address of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "PrivateIp"
        ]
      }
    },
    "PublicIp": {
      "Description": "Public IP address of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "PublicIp"
        ]
      }
    },
    "HostName": {
      "Description": "Host name of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceClone",
          "HostName"
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
  BackendServerWeight:
    Type: Number
    Description: >-
      The weight of backend server of load balancer. From 0 to 100, 0 means
      offline. Default is 100.
    MinValue: 0
    MaxValue: 100
    Default: 100
  KeyPairName:
    Type: String
    Description: SSH key pair name.
  Description:
    Type: String
    Description: >-
      Description of the instance, [2, 256] characters. Do not fill or empty,
      the default is empty.
  DiskMappings:
    Type: Json
    Description: >-
      Disk mappings to attach to instance. Max support 16 disks.

      If the image contains a data disk, you can specify other parameters of the
      data disk via the same value of parameter "Device". If parameter
      "Category" is not specified, it will be cloud_efficiency instead of
      "Category" of data disk in the image.
    MaxLength: 16
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  ZoneId:
    Type: String
    Description: current zone to create the instance.
  InstanceChargeType:
    Type: String
    Description: >-
      Instance Charge type, allowed value: Prepaid and Postpaid. If specified
      Prepaid, please ensure you have sufficient balance in your account. Or
      instance creation will be failure. Default value is Postpaid.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  SecurityGroupId:
    Type: String
    Description: >-
      Security group to create ecs instance. For classic instance need the
      security group not belong to VPC, for VPC instance, please make sure the
      security group belong to specified VPC.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36,
      48, 60. Default value is 1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 4
      - 5
      - 6
      - 7
      - 8
      - 9
      - 12
      - 24
      - 36
      - 48
      - 60
    Default: 1
  DeletionProtection:
    Type: Boolean
    Description: >-
      Whether an instance can be released manually through the console or API,
      deletion protection only support postPaid instance
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  SourceInstanceId:
    Type: String
    Description: >-
      Source ecs instance used to copy properties to clone new ecs instance. It
      will copy the InstanceType, ImageId, InternetChargeType,
      InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and
      data disk configurations. If the instance network is VPC, it will also
      clone the relative properties. If specified instance with more than one
      security group, it will use the first security group to create instance.
      you can also specify the SecurityGroupId to override it.
  LoadBalancerIdToAttach:
    Type: String
    Description: After the instance is created. Automatic attach it to the load balancer.
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SpotPriceLimit:
    Type: String
    Description: >-
      The hourly price threshold of a instance, and it takes effect only when
      parameter InstanceChargeType is PostPaid. Three decimals is allowed at
      most.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  SpotStrategy:
    Type: String
    Description: >-
      The spot strategy of a Pay-As-You-Go instance, and it takes effect only
      when parameter InstanceChargeType is PostPaid. Value range: "NoSpot: A
      regular Pay-As-You-Go instance", "SpotWithPriceLimit: A price threshold
      for a spot instance, ""SpotAsPriceGo: A price that is based on the highest
      Pay-As-You-Go instance. "Default value: NoSpot.
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
  Password:
    Type: String
    Description: >-
      Password of created ecs instance. Must contain at least 3 types of special
      character, lower character, upper character, number.
Resources:
  InstanceClone:
    Type: 'ALIYUN::ECS::InstanceClone'
    Properties:
      BackendServerWeight:
        Ref: BackendServerWeight
      KeyPairName:
        Ref: KeyPairName
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      ResourceGroupId:
        Ref: ResourceGroupId
      ZoneId:
        Ref: ZoneId
      InstanceChargeType:
        Ref: InstanceChargeType
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      DeletionProtection:
        Ref: DeletionProtection
      SourceInstanceId:
        Ref: SourceInstanceId
      LoadBalancerIdToAttach:
        Ref: LoadBalancerIdToAttach
      InstanceName:
        Ref: InstanceName
      RamRoleName:
        Ref: RamRoleName
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      ImageId:
        Ref: ImageId
      SpotPriceLimit:
        Ref: SpotPriceLimit
      Tags:
        Ref: Tags
      SpotStrategy:
        Ref: SpotStrategy
      Password:
        Ref: Password
Outputs:
  PrimaryNetworkInterfaceId:
    Description: Primary network interface id of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - PrimaryNetworkInterfaceId
  InnerIp:
    Description: Inner IP address of the specified instance. Only for classical instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - InnerIp
  ZoneId:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - ZoneId
  InstanceId:
    Description: The instance id of created ecs instance
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - InstanceId
  PrivateIp:
    Description: Private IP address of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - PrivateIp
  PublicIp:
    Description: Public IP address of created ecs instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - PublicIp
  HostName:
    Description: Host name of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceClone
        - HostName
```


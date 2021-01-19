# ALIYUN::ECS::PrepayInstanceGroupClone

ALIYUN::ECS::PrepayInstanceGroupClone is used to clone a group of subscription ECS instances.

## Syntax

```
{
  "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
  "Properties": {
    "PeriodType": String,
    "SystemDiskAutoSnapshotPolicyId": String,
    "SystemDiskCategory": String,
    "RamRoleName": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "MinAmount": Integer,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "AutoRenew": String,
    "SourceInstanceId": String,
    "EniMappings": List,
    "Password": String,
    "PasswordInherit": Boolean,
    "MaxAmount": Integer,
    "DiskMappings": List,
    "LaunchTemplateName": String,
    "LaunchTemplateVersion": String,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SecurityGroupIds": String,
    "LaunchTemplateId": String,
    "Period": Number,
    "HpcClusterId": String,
    "SystemDiskDescription": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|HpcClusterId|String|No|Yes|The ID of the E-HPC cluster to which the created ECS instances belong.|None|
|PeriodType|String|Yes|No|The type of billing cycle for the created ECS instances.|Valid values: -   Monthly
-   Yearly |
|SystemDiskCategory|String|No|Yes|The type of the system disk.|Default value: cloud\_efficiency. Valid values: -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD |
|RamRoleName|String|No|No|The RAM role name of the created ECS instances.|You can call the ListRoles operation to query the RAM role name. For more information, see [CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md) and [ListRoles](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/ListRoles.md).|
|KeyPairName|String|No|Yes|The name of the key pair that is used to connect to the created ECS instances.|For Windows instances, this parameter is ignored by default. For Linux instances, logon by password is disabled by default. To enhance instance security, we recommend that you use the SSH key pair for connection.|
|SystemDiskDiskName|String|No|Yes|The name of the system disk.|None|
|PeriodUnit|String|No|Yes|The unit of the billing cycle.|Default value: Month. Valid values: -   Week
-   Month |
|Description|String|No|Yes|The description of the created ECS instances.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Tags|List|No|Yes|The custom tags of the ECS instances.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_xs0_kno_v4a). |
|MinAmount|Integer|Yes|No|The minimum number of ECS instances that can be created.|Valid values: 1 to 100. This parameter must be set to a value less than or equal to the value of the MaxAmount parameter. |
|AutoRenewPeriod|Number|No|Yes|The auto-renewal period for the created ECS instances.|Default value: 1. Valid values:-   1
-   2
-   3
-   6
-   12 |
|ImageId|String|No|Yes|The ID of the image that is used to start the created ECS instances. You can use a public image, a custom image, or an Alibaba Cloud Marketplace image.|None|
|AutoRenew|String|No|Yes|Specifies whether to enable auto-renewal for the created ECS instances.|Default value: false. Valid values: -   true
-   false |
|SourceInstanceId|String|Yes|No|The ID of the source ECS instance to be cloned.|The clone operation clones the specified instance, including its instance type, image, billing method for network usage, bandwidth limit, and network type. If the source ECS instance belongs to multiple security groups, the cloned instance is added only to the first of these security groups.|
|EniMappings|List|No|Yes|The elastic network interfaces \(ENIs\) to be attached to the created ECS instances.|Only one ENI can be attached to an instance. For more information, see [EniMappings properties](#section_dy6_vil_dja). |
|Password|String|No|Yes|The password that is used to log on to the created ECS instances.|The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include ```
( ) ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? / -
```

If you specify this parameter in the API request, use HTTPS to secure the API and protect your password.|
|PasswordInherit|Boolean|No|No|Specifies whether to use the password preset in the image.|Valid values:-   true
-   false

**Note:** To use the PasswordInherit parameter, the Password parameter must be empty and you must make sure that the selected image has a password configured. |
|MaxAmount|Integer|Yes|No|The maximum number of ECS instances that can be created.|Valid values: 1 to 100. This parameter must be set to a value greater than or equal to the value of the MinAmount parameter. |
|DiskMappings|List|No|Yes|The disks to be attached to the created instances.|A maximum of 16 disks can be attached for each instance. For more information, see [DiskMappings properties](#section_5fl_9j5_atz). |
|LaunchTemplateName|String|No|Yes|The name of the launch template.|None|
|LaunchTemplateVersion|String|No|Yes|The version of the launch template.|If you do not specify a version, the default version is used.|
|ZoneId|String|No|No|The ID of the zone.|None|
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound public bandwidth.|Valid values: -   Valid values for the PayByBandwidth mode: 0 to 200.
-   Valid values for the PayByTraffic mode: 1 to 200. This parameter is required if the InternetChargeType parameter is set to PayByTraffic.

Unit: Mbit/s. |
|InstanceName|String|No|No|The names of the created ECS instances.|The names can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Valid values: 1 to 200.

Default value: 200.

Unit: Mbit/s. |
|SecurityGroupId|String|No|No|The ID of the security group to which the created ECS instances belong.|You cannot specify both SecurityGroupId and SecurityGroupIds.|
|SecurityGroupIds|List|No|No|The IDs of multiple security groups to which the created ECS instances belong. For information about the quota for security groups to which an ECS instance can belong, see [Security group limits](/intl.en-US/Product Introduction/Limits.md).|You cannot specify both SecurityGroupId and SecurityGroupIds.|
|LaunchTemplateId|String|No|Yes|The ID of the launch template.|None|
|Period|Number|Yes|No|The subscription period of the created ECS instances.|Valid values:-   Valid values when the PeriodType parameter is set to Monthly: 1 to 9.
-   Valid values when the PeriodType parameter is set to Yearly: 1 to 3. |
|SystemDiskDescription|String|No|Yes|The description of the system disk.|None|
|DeploymentSetId|String|No|Yes|The ID of the deployment set.|None|
|SystemDiskAutoSnapshotPolicyId|String|No|Yes|The ID of the automatic snapshot policy for the system disk.|None|

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## EniMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "AutoSnapshotPolicyId": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "PerformanceLevel": String,
    "Size": String
  }
]
```

## EniMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SecurityGroupId|String|Yes|Yes|The ID of the security group.|The security group and the ENI must belong to the same VPC.|
|VSwitchId|String|Yes|No|The ID of the VSwitch.|None|
|Description|String|No|Yes|The description of the ENI.|None|
|NetworkInterfaceName|String|No|Yes|The name of the ENI.|None|
|PrimaryIpAddress|String|No|No|The primary private IP address of the ENI.|The specified IP address must be available within the CIDR block of the VSwitch. If this parameter is not specified, an available IP address in the VSwitch CIDR block is selected at random.|

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "AutoSnapshotPolicyId": String,
    "Encrypted": String,
    "KMSKeyId": String,
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
|Encrypted|String|No|No|Specifies whether to encrypt the data disk.|Valid values: -   true
-   false |
|KMSKeyId|String|No|No|The ID of the KMS key corresponding to the data disk.|None|
|Category|String|No|No|The type of the data disk.|Default value: cloud\_efficiency. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD |
|DiskName|String|No|No|The name of the data disk.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of the data disk.|None|
|Device|String|No|No|The device name of the data disk that is attached to an ECS instance.|Example: `/dev/xvd[a-z]`.|
|SnapshotId|String|No|No|The ID of the snapshot.|None|
|Size|String|Yes|No|The size of the data disk.|Unit: GB.|
|PerformanceLevel|String|No|No|The performance level of the enhanced SSD that is used as the data disk.|Default value: PL1. Valid values: -   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md). |
|AutoSnapshotPolicyId|String|No|No|The ID of the automatic snapshot policy.|None|

## Response parameters

Fn::GetAtt

-   OrderId: the ID of the order.
-   InnerIps: the list of private IP addresses of instances in the classic network.
-   PrivateIps: the private IP addresses of instances in a VPC.
-   ZoneIds: the IDs of zones.
-   PublicIps: the list of public IP addresses of instances in the classic network.
-   HostNames: the hostnames of the created ECS instances.
-   RelatedOrderIds: the related order IDs.
-   InstanceIds: the IDs of the created ECS instances.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeriodType": {
      "Type": "String",
      "Description": "Charge period for created instances.",
      "AllowedValues": [
        "Monthly",
        "Yearly"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty. Old instances will not be changed."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image. Old instances will not be changed.",
      "MaxLength": 16
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk. Old instances will not be changed."
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False. Old instances will not be changed.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source ecs instance used to copy properties to clone new ecs instance. It will copy the InstanceType, ImageId, InternetChargeType, InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and data disk configurations. If the instance network is VPC, it will also clone the relative properties. If specified instance with more than one security group, it will use the first security group to create instance. you can also specify the SecurityGroupId to override it."
    },
    "MaxAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be smaller than 'MaxAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100
    },
    "SystemDiskAutoSnapshotPolicyId": {
      "Type": "String",
      "Description": "Auto snapshot policy ID."
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "MinAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be bigger than 'MinAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk. Old instances will not be changed."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "PasswordInherit": {
      "Type": "Boolean",
      "Description": "Specifies whether to use the password preset in the image. To use the PasswordInherit parameter, the Password parameter must be empty and you must make sure that the selected image has a password configured.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect. It could be 1, 2, 3, 6, 12. Default value is 1. Old instances will not be changed.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name. Old instances will not be changed."
    },
    "LaunchTemplateName": {
      "Type": "String",
      "Description": "Name of launch template. Launch template id or name must be specified to use launch template"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs.The change of the property does not affect existing instances."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "ID of launch template. Launch template id or name must be specified to use launch template"
    },
    "SecurityGroupIds": {
      "Type": "CommaDelimitedList",
      "Description": "The IDs of security groups N to which the instance belongs. The valid values of N are based on the maximum number of security groups to which an instance can belong. For more information, see Security group limits.Note: You cannot specify both SecurityGroupId and SecurityGroupIds at the same time."
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd. Old instances will not be changed.",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "EniMappings": {
      "Type": "Json",
      "Description": "NetworkInterface to attach to instance. Max support 1 ENI.",
      "MaxLength": 1
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID. The change of the property does not affect existing instances."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1.While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "Version of launch template. Default version is used if version is not specified.",
      "AllowedPattern": "^[1-9]\\d*$"
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month. Old instances will not be changed.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    }
  },
  "Resources": {
    "PrepayInstanceGroupClone": {
      "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
        },
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "SystemDiskAutoSnapshotPolicyId": {
          "Ref": "SystemDiskAutoSnapshotPolicyId"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "MinAmount": {
          "Ref": "MinAmount"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PasswordInherit": {
          "Ref": "PasswordInherit"
        },
        "Password": {
          "Ref": "Password"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "LaunchTemplateName": {
          "Ref": "LaunchTemplateName"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "SecurityGroupIds": {
          "Ref": "SecurityGroupIds"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "EniMappings": {
          "Ref": "EniMappings"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "DeploymentSetId": {
          "Ref": "DeploymentSetId"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "PublicIps": {
      "Description": "Public IP address list of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "PublicIps"
        ]
      }
    },
    "RelatedOrderIds": {
      "Description": "The related order id list of created ecs instances",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "RelatedOrderIds"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "InstanceIds"
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
  PeriodType:
    Type: String
    Description: Charge period for created instances.
    AllowedValues:
      - Monthly
      - Yearly
  Description:
    Type: String
    Description: >-
      Description of the instance, [2, 256] characters. Do not fill or empty,
      the default is empty. Old instances will not be changed.
  DiskMappings:
    Type: Json
    Description: >-
      Disk mappings to attach to instance. Max support 16 disks.

      If the image contains a data disk, you can specify other parameters of the
      data disk via the same value of parameter "Device". If parameter
      "Category" is not specified, it will be cloud_efficiency instead of
      "Category" of data disk in the image. Old instances will not be changed.
    MaxLength: 16
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk. Old instances will not be changed.
  AutoRenew:
    Type: String
    Description: >-
      Whether renew the fee automatically? When the parameter InstanceChargeType
      is PrePaid, it will take effect. Range of value:True: automatic
      renewal.False: no automatic renewal. Default value is False.Old instances
      will not be changed.
    AllowedValues:
      - 'True'
      - 'False'
    Default: 'False'
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
  MaxAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be smaller than 'MaxAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
  SystemDiskAutoSnapshotPolicyId:
    Type: String
    Description: Auto snapshot policy ID.
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  MinAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be bigger than 'MinAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
    Default: 1
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk. Old instances will not be changed.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  PasswordInherit:
    Type: Boolean
    Description: >-
      Specifies whether to use the password preset in the image. To use the
      PasswordInherit parameter, the Password parameter must be empty and you
      must make sure that the selected image has a password configured.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Password:
    Type: String
    Description: >-
      Password of created ecs instance. Must contain at least 3 types of special
      character, lower character, upper character, number.
  AutoRenewPeriod:
    Type: Number
    Description: >-
      The time period of auto renew. When the parameter InstanceChargeType is
      PrePaid, it will take effect. It could be 1, 2, 3, 6, 12. Default value is
      1. Old instances will not be changed.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  KeyPairName:
    Type: String
    Description: SSH key pair name. Old instances will not be changed.
  LaunchTemplateName:
    Type: String
    Description: >-
      Name of launch template. Launch template id or name must be specified to
      use launch template
  ZoneId:
    Type: String
    Description: current zone to create the instance.
  HpcClusterId:
    Type: String
    Description: >-
      The HPC cluster ID to which the instance belongs.The change of the
      property does not affect existing instances.
  SecurityGroupId:
    Type: String
    Description: >-
      Security group to create ecs instance. For classic instance need the
      security group not belong to VPC, for VPC instance, please make sure the
      security group belong to specified VPC.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  LaunchTemplateId:
    Type: String
    Description: >-
      ID of launch template. Launch template id or name must be specified to use
      launch template
  SecurityGroupIds:
    Type: CommaDelimitedList
    Description: >-
      The IDs of security groups N to which the instance belongs. The valid
      values of N are based on the maximum number of security groups to which an
      instance can belong. For more information, see Security group limits.Note:
      You cannot specify both SecurityGroupId and SecurityGroupIds at the same
      time.
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. Default is cloud_efficiency. support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd.Old instances
      will not be changed.
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
    Default: cloud_efficiency
  EniMappings:
    Type: Json
    Description: NetworkInterface to attach to instance. Max support 1 ENI.
    MaxLength: 1
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  DeploymentSetId:
    Type: String
    Description: >-
      Deployment set ID. The change of the property does not affect existing
      instances.
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Set internet output bandwidth of instance. Unit is Mbps(Mega bit per
      second). Range is [0,200]. Default is 1.While the property is not 0,
      public ip will be assigned for instance.
    MinValue: 0
    MaxValue: 200
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  LaunchTemplateVersion:
    Type: String
    Description: >-
      Version of launch template. Default version is used if version is not
      specified.
    AllowedPattern: '^[1-9]\d*$'
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month. Default value is
      Month. Old instances will not be changed.
    AllowedValues:
      - Week
      - Month
    Default: Month
Resources:
  PrepayInstanceGroupClone:
    Type: 'ALIYUN::ECS::PrepayInstanceGroupClone'
    Properties:
      PeriodType:
        Ref: PeriodType
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      SystemDiskDescription:
        Ref: SystemDiskDescription
      AutoRenew:
        Ref: AutoRenew
      SourceInstanceId:
        Ref: SourceInstanceId
      MaxAmount:
        Ref: MaxAmount
      SystemDiskAutoSnapshotPolicyId:
        Ref: SystemDiskAutoSnapshotPolicyId
      RamRoleName:
        Ref: RamRoleName
      MinAmount:
        Ref: MinAmount
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      Tags:
        Ref: Tags
      PasswordInherit:
        Ref: PasswordInherit
      Password:
        Ref: Password
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      KeyPairName:
        Ref: KeyPairName
      LaunchTemplateName:
        Ref: LaunchTemplateName
      ZoneId:
        Ref: ZoneId
      HpcClusterId:
        Ref: HpcClusterId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      LaunchTemplateId:
        Ref: LaunchTemplateId
      SecurityGroupIds:
        Ref: SecurityGroupIds
      SystemDiskCategory:
        Ref: SystemDiskCategory
      EniMappings:
        Ref: EniMappings
      InstanceName:
        Ref: InstanceName
      DeploymentSetId:
        Ref: DeploymentSetId
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  PublicIps:
    Description: Public IP address list of created ecs instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - PublicIps
  RelatedOrderIds:
    Description: The related order id list of created ecs instances
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - RelatedOrderIds
  PrivateIps:
    Description: Private IP address list of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - PrivateIps
  HostNames:
    Description: Host names of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - HostNames
  InnerIps:
    Description: >-
      Inner IP address list of the specified instance. Only for classical
      instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - InnerIps
  ZoneIds:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - ZoneIds
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - OrderId
  InstanceIds:
    Description: The instance id list of created ecs instance
    Value:
      'Fn::GetAtt':
        - PrepayInstanceGroupClone
        - InstanceIds
```


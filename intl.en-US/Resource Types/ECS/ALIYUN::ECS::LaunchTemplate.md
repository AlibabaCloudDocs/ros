# ALIYUN::ECS::LaunchTemplate

ALIYUN::ECS::LaunchTemplate is used to create a launch template for creating ECS instances.

## Syntax

```
{
  "Type": "ALIYUN::ECS::LaunchTemplate",
  "Properties": {
    "LaunchTemplateName": String,
    "VersionDescription": String,
    "ImageId": String,
    "InstanceType": String,
    "SecurityGroupId": String,
    "NetworkType": String,
    "VSwitchId": String,
    "InstanceName": String,
    "Description": String,
    "InternetMaxBandwidthIn": Integer,
    "InternetMaxBandwidthOut": Integer,
    "HostName": String,
    "ZoneId": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Number,
    "SystemDiskDiskName": String,
    "SystemDiskDescription": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "UserData": String,
    "KeyPairName": String,
    "RamRoleName": String,
    "AutoReleaseTime": String,
    "SpotStrategy": String,
    "SpotPriceLimit": String,
    "SecurityEnhancementStrategy": String,
    "DiskMappings": List,
    "NetworkInterfaces": List,
    "Tags": List,
    "TemplateTags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|LaunchTemplateName|String|Yes|No|The name of the launch template.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|VersionDescription|String|No|No|The description of the launch template version.|The description must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|ImageId|String|No|No|The ID of the image.|None|
|InstanceType|String|No|No|The type of the ECS instance.|None|
|SecurityGroupId|String|No|No|The ID of the security group.|None|
|NetworkType|String|No|No|The network type of the instance.|Valid values: -   classic
-   vpc |
|VSwitchId|String|No|No|The ID of the VSwitch. This parameter is required if you want to create an instance in a VPC.|None|
|InstanceName|String|No|No|The name of the instance.|The name must be 2 to 128 characters in length. The name must start with a letter and cannot start with `http://` or `https://`.|
|Description|String|No|No|The description of the instance.|The description must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet.|Valid values: 1 to 200. Unit: Mbit/s. |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth to the Internet.|Valid values: 0 to 100. Unit: Mbit/s. |
|HostName|String|No|No|The hostname of the instance.|The hostname cannot contain consecutive periods \(.\) or hyphens \(-\). It cannot start or end with a period \(.\) or hyphen \(-\).

Valid values: -   For Windows instances:
    -   The hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\).
    -   It cannot contain only digits.
-   For other instances such as Linux instances:
    -   The hostname must be 2 to 64 characters in length and can contain letters, digits, and hyphens \(-\). |
|ZoneId|String|No|No|The ID of the zone to which the instance belongs.|None|
|SystemDiskCategory|String|No|No|The type of the system disk.|Valid values: -   cloud: basic disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: standard SSD.
-   ephemeral\_ssd: local SSD. |
|SystemDiskSize|Number|No|No|The size of the system disk.|Valid values: 20 to 500. Unit: GB. |
|SystemDiskDiskName|String|No|No|The name of the system disk.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|SystemDiskDescription|String|No|No|The description of the system disk.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|IoOptimized|String|No|No|Specifies whether the instance is I/O optimized.|Valid values: -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|InternetChargeType|String|No|No|The billing method for network usage.|Valid values: -   PayByBandwidth
-   PayByTraffic |
|UserData|String|No|No|The user data of the instance.|The user data must be encoded in Base64. The maximum size of the raw data is 16 KB.|
|KeyPairName|String|No|No|The name of the key pair.|Valid values: -   For Windows instances, this parameter is ignored and empty by default. The Password parameter takes effect even if the KeyPairName parameter is specified.
-   For Linux instances, the username and password authentication method is disabled by default. |
|RamRoleName|String|No|No|The RAM role name of the instance.|None|
|AutoReleaseTime|String|No|No|The time scheduled for the instance to be automatically released.|The time follows the ISO 8601 standard in the `YYYY-MM-DDThh:mm:ssZ` format. The time is displayed in UTC.|
|SpotStrategy|String|No|No|The preemption policy for pay-as-you-go instances.|This parameter takes effect only when the InstanceChargeType parameter is set to PostPaid.

Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with a maximum hourly price.
-   SpotAsPriceGo: applies to pay-as-you-go instances priced at the market price at the time of purchase. |
|SpotPriceLimit|String|No|No|The maximum hourly price of the instance.|Three decimal places are allowed at most.|
|SecurityEnhancementStrategy|String|No|No|Specifies whether to enable security hardening.|Valid values: -   Active: enables security hardening.
-   Deactive: disables security hardening. |
|DiskMappings|List|No|No|The list of data disks.|A maximum of 16 data disks can be specified. For more information, see [DiskMappings properties](#section_p35_rmn_4fb). |
|NetworkInterfaces|List|No|No|The list of ENIs.|A maximum of eight ENIs can be specified. For more information, see [NetworkInterfaces properties](#section_bs3_2nn_4fb). |
|Tags|List|No|No|The tags of an instance, a security group, a disk, or an ENI.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_e2f_vnn_4fb). |
|TemplateTags|List|No|No|The tags of the launch template.|A maximum of 20 tags can be specified. For more information, see [TemplateTags properties](#section_fcq_n4n_4fb). |

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "SnapshotId": String,
    "Size": String,
    "Encrypted": String,
    "DeleteWithInstance": String
  }
]
```

## DiskMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Category|String|No|No|The type of the data disk.|Valid values: -   cloud: basic disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: standard SSD.
-   ephemeral\_ssd: local SSD. |
|DiskName|String|No|No|The name of the data disk.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|None|
|Size|String|No|No|The size of the system disk.|Valid values:

-   cloud: 5 to 2000.
-   cloud\_efficiency: 20 to 32768.
-   cloud\_ssd: 20 to 32768.
-   ephemeral\_ssd: 5 to 800.

Unit: GB. |
|Encrypted|Boolean|No|No|Specifies whether to encrypt the data disk.|None|
|DeleteWithInstance|Boolean|No|No|Specifies whether to release the data disk when the instance is released.|None|

## NetworkInterfaces syntax

```
"NetworkInterfaces": [
  {
    "PrimaryIpAddress": String,
    "VSwitchId": String,
    "SecurityGroupId": String,
    "NetworkInterfaceName": String,
    "Description": String
  }
]
```

## NetworkInterfaces properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PrimaryIpAddress|String|No|No|The primary private IP address of the ENI.|None|
|VSwitchId|String|No|No|The ID of the VSwitch to which the ENI belongs.|None|
|SecurityGroupId|String|No|No|The ID of the security group to which the ENI belongs.|None|
|NetworkInterfaceName|String|No|No|The name of the ENI.|None|
|Description|String|No|No|The description of the ENI.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|

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
|Key|String|No|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## TemplateTags syntax

```
"TemplateTags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## TemplateTags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|No|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   LaunchTemplateId: the ID of the instance launch template.
-   LaunchTemplateName: the name of the instance launch template.
-   DefaultVersionNumber: the default version number of the instance launch template.
-   LatestVersionNumber: the latest version number of the instance launch template.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.",
      "MaxLength": 16
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size. ",
      "MinValue": 20
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters."
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk."
    },
    "TemplateTags": {
      "Type": "Json",
      "Description": "Template tags to attach to launch template.",
      "MaxLength": 20
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "Instance network type. Support 'vpc' and 'classic'",
      "AllowedValues": [
        "vpc",
        "classic"
      ]
    },
    "NetworkInterfaces": {
      "Type": "Json",
      "Description": "Elastic network interfaces to be attached to instance.",
      "MaxLength": 8
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk."
    },
    "SpotPriceLimit": {
      "Type": "String",
      "Description": "The hourly price threshold of a instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Three decimals is allowed at most. "
    },
    "InstanceType": {
      "Type": "String",
      "Description": "Ecs instance supported instance type, make sure it should be correct."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance, security group, disk and network interface.",
      "MaxLength": 20
    },
    "HostName": {
      "Type": "String",
      "Description": "Host name of created ecs instance. at least 2 characters, and '.' '-' Is not the first and last characters as hostname, not continuous use. Windows platform can be up to 15 characters, allowing letters (without limiting case), numbers and '-', and does not support the number of points, not all is digital ('.').Other (Linux, etc.) platform up to 30 characters, allowing support number multiple points for the period between the points, each permit letters (without limiting case), numbers and '-' components."
    },
    "SpotStrategy": {
      "Type": "String",
      "Description": "The spot strategy of a Pay-As-You-Go instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Value range: \"NoSpot: A regular Pay-As-You-Go instance\", \"SpotWithPriceLimit: A price threshold for a spot instance, \"\"SpotAsPriceGo: A price that is based on the highest Pay-As-You-Go instance. \"",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "LaunchTemplateName": {
      "Type": "String",
      "Description": "The name of launch template."
    },
    "IoOptimized": {
      "Type": "String",
      "Description": "The 'optimized' instance can provide better IO performance. Support 'none' and 'optimized' only.",
      "AllowedValues": [
        "none",
        "optimized"
      ]
    },
    "VersionDescription": {
      "Type": "String",
      "Description": "Description for version 1 of launch template."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Current zone to create the instance."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ]
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only.",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ]
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Max internet out bandwidth in Mbps(Mega bit per second). Range is [0,200].While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet in bandwidth in Mbps(Mega bit per second). The range is [1,200].",
      "MinValue": 1,
      "MaxValue": 200
    },
    "SecurityEnhancementStrategy": {
      "Type": "String",
      "Description": "Activate or deactivate security enhancement,Value range: \"Active\" and \"Deactive\"",
      "AllowedValues": [
        "Active",
        "Deactive"
      ]
    },
    "AutoReleaseTime": {
      "Type": "String",
      "Description": "Auto release time for created instance, Follow ISO8601 standard using UTC time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this day onwards"
    }
  },
  "Resources": {
    "LaunchTemplate": {
      "Type": "ALIYUN::ECS::LaunchTemplate",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Ref": "UserData"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "TemplateTags": {
          "Ref": "TemplateTags"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "NetworkInterfaces": {
          "Ref": "NetworkInterfaces"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "HostName": {
          "Ref": "HostName"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "LaunchTemplateName": {
          "Ref": "LaunchTemplateName"
        },
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "VersionDescription": {
          "Ref": "VersionDescription"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "SecurityEnhancementStrategy": {
          "Ref": "SecurityEnhancementStrategy"
        },
        "AutoReleaseTime": {
          "Ref": "AutoReleaseTime"
        }
      }
    }
  },
  "Outputs": {
    "LaunchTemplateName": {
      "Description": "The name of launch template.",
      "Value": {
        "Fn::GetAtt": [
          "LaunchTemplate",
          "LaunchTemplateName"
        ]
      }
    },
    "LatestVersionNumber": {
      "Description": "The latest version number of launch template.",
      "Value": {
        "Fn::GetAtt": [
          "LaunchTemplate",
          "LatestVersionNumber"
        ]
      }
    },
    "LaunchTemplateId": {
      "Description": "The id of launch template.",
      "Value": {
        "Fn::GetAtt": [
          "LaunchTemplate",
          "LaunchTemplateId"
        ]
      }
    },
    "DefaultVersionNumber": {
      "Description": "The default version number of launch template.",
      "Value": {
        "Fn::GetAtt": [
          "LaunchTemplate",
          "DefaultVersionNumber"
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
  Description:
    Type: String
    Description: 'Description of the instance, [2, 256] characters.'
  DiskMappings:
    Type: Json
    Description: Disk mappings to attach to instance. Max support 16 disks.
    MaxLength: 16
  SystemDiskSize:
    Type: Number
    Description: >-
      Disk size of the system disk, range from 20 to 500 GB. If you specify with
      your own image, make sure the system disk size bigger than image size.
    MinValue: 20
  UserData:
    Type: String
    Description: 'User data to pass to instance. [1, 16KB] characters.'
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk.
  TemplateTags:
    Type: Json
    Description: Template tags to attach to launch template.
    MaxLength: 20
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  NetworkType:
    Type: String
    Description: Instance network type. Support 'vpc' and 'classic'
    AllowedValues:
      - vpc
      - classic
  NetworkInterfaces:
    Type: Json
    Description: Elastic network interfaces to be attached to instance.
    MaxLength: 8
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk.
  SpotPriceLimit:
    Type: String
    Description: >-
      The hourly price threshold of a instance, and it takes effect only when
      parameter InstanceChargeType is PostPaid. Three decimals is allowed at
      most.
  InstanceType:
    Type: String
    Description: 'Ecs instance supported instance type, make sure it should be correct.'
  Tags:
    Type: Json
    Description: 'Tags to attach to instance, security group, disk and network interface.'
    MaxLength: 20
  HostName:
    Type: String
    Description: >-
      Host name of created ecs instance. at least 2 characters, and '.' '-' Is
      not the first and last characters as hostname, not continuous use. Windows
      platform can be up to 15 characters, allowing letters (without limiting
      case), numbers and '-', and does not support the number of points, not all
      is digital ('.').Other (Linux, etc.) platform up to 30 characters,
      allowing support number multiple points for the period between the points,
      each permit letters (without limiting case), numbers and '-' components.
  SpotStrategy:
    Type: String
    Description: >-
      The spot strategy of a Pay-As-You-Go instance, and it takes effect only
      when parameter InstanceChargeType is PostPaid. Value range: "NoSpot: A
      regular Pay-As-You-Go instance", "SpotWithPriceLimit: A price threshold
      for a spot instance, ""SpotAsPriceGo: A price that is based on the highest
      Pay-As-You-Go instance. "
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
  KeyPairName:
    Type: String
    Description: SSH key pair name.
  LaunchTemplateName:
    Type: String
    Description: The name of launch template.
  IoOptimized:
    Type: String
    Description: >-
      The 'optimized' instance can provide better IO performance. Support 'none'
      and 'optimized' only.
    AllowedValues:
      - none
      - optimized
  VersionDescription:
    Type: String
    Description: Description for version 1 of launch template.
  ZoneId:
    Type: String
    Description: Current zone to create the instance.
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ecs instance.
  SecurityGroupId:
    Type: String
    Description: >-
      Security group to create ecs instance. For classic instance need the
      security group not belong to VPC, for VPC instance, please make sure the
      security group belong to specified VPC.
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only.
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Max internet out bandwidth in Mbps(Mega bit per second). Range is
      [0,200].While the property is not 0, public ip will be assigned for
      instance.
    MinValue: 0
    MaxValue: 200
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet in bandwidth in Mbps(Mega bit per second). The range is
      [1,200].
    MinValue: 1
    MaxValue: 200
  SecurityEnhancementStrategy:
    Type: String
    Description: >-
      Activate or deactivate security enhancement,Value range: "Active" and
      "Deactive"
    AllowedValues:
      - Active
      - Deactive
  AutoReleaseTime:
    Type: String
    Description: >-
      Auto release time for created instance, Follow ISO8601 standard using UTC
      time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this
      day onwards
Resources:
  LaunchTemplate:
    Type: 'ALIYUN::ECS::LaunchTemplate'
    Properties:
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      SystemDiskSize:
        Ref: SystemDiskSize
      UserData:
        Ref: UserData
      SystemDiskDescription:
        Ref: SystemDiskDescription
      TemplateTags:
        Ref: TemplateTags
      RamRoleName:
        Ref: RamRoleName
      NetworkType:
        Ref: NetworkType
      NetworkInterfaces:
        Ref: NetworkInterfaces
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      SpotPriceLimit:
        Ref: SpotPriceLimit
      InstanceType:
        Ref: InstanceType
      Tags:
        Ref: Tags
      HostName:
        Ref: HostName
      SpotStrategy:
        Ref: SpotStrategy
      KeyPairName:
        Ref: KeyPairName
      LaunchTemplateName:
        Ref: LaunchTemplateName
      IoOptimized:
        Ref: IoOptimized
      VersionDescription:
        Ref: VersionDescription
      ZoneId:
        Ref: ZoneId
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      SystemDiskCategory:
        Ref: SystemDiskCategory
      InternetChargeType:
        Ref: InternetChargeType
      InstanceName:
        Ref: InstanceName
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      SecurityEnhancementStrategy:
        Ref: SecurityEnhancementStrategy
      AutoReleaseTime:
        Ref: AutoReleaseTime
Outputs:
  LaunchTemplateName:
    Description: The name of launch template.
    Value:
      'Fn::GetAtt':
        - LaunchTemplate
        - LaunchTemplateName
  LatestVersionNumber:
    Description: The latest version number of launch template.
    Value:
      'Fn::GetAtt':
        - LaunchTemplate
        - LatestVersionNumber
  LaunchTemplateId:
    Description: The id of launch template.
    Value:
      'Fn::GetAtt':
        - LaunchTemplate
        - LaunchTemplateId
  DefaultVersionNumber:
    Description: The default version number of launch template.
    Value:
      'Fn::GetAtt':
        - LaunchTemplate
        - DefaultVersionNumber
```


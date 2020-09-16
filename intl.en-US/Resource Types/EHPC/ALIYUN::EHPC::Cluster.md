# ALIYUN::EHPC::Cluster

ALIYUN::EHPC::Cluster is used to create an Elastic High Performance Computing \(E-HPC\) cluster.

## Syntax

```
{
  "Type": "ALIYUN::EHPC::Cluster",
  "Properties": {
    "EcsOrderComputeCount": Integer,
    "OsTag": String,
    "HaEnable": Boolean,
    "VolumeType": String,
    "VolumeId": String,
    "EcsOrderManagerInstanceType": String,
    "Application": List,
    "EcsOrderComputeInstanceType": String,
    "KeyPairName": String,
    "PeriodUnit": String,
    "Description": String,
    "AutoRenewPeriod": Integer,
    "JobQueue": String,
    "ImageId": String,
    "AutoRenew": Boolean,
    "EhpcVersion": String,
    "VSwitchId": String,
    "Password": String,
    "Name": String,
    "SchedulerType": String,
    "SccClusterId": String,
    "EcsChargeType": String,
    "ZoneId": String,
    "EcsOrderLoginCount": Integer,
    "DeployMode": String,
    "ImageOwnerAlias": String,
    "RemoteDirectory": String,
    "ComputeSpotPriceLimit": String,
    "ComputeSpotStrategy": String,
    "SecurityGroupName": String,
    "KeyPairName": String,
    "VolumeProtocol": String,
    "SecurityGroupId": String,
    "Period": Integer,
    "PostInstallScript": List,
    "AccountType": String,
    "VolumeMountpoint": String,
    "EcsOrderLoginInstanceType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EcsOrderComputeCount|Integer|Yes|No|The number of compute nodes in the cluster.|Valid values: 1 to 99.|
|OsTag|String|Yes|No|The operating system image. Example: CentOS\_7.2\_64.|None|
|HaEnable|Boolean|No|No|Specifies whether high availability is enabled. If high availability is enabled, each management role in the cluster uses a primary instance and a secondary instance.|None|
|VolumeType|String|No|No|The type of the network shared storage.|Set the value to nas.|
|KeyPairName|String|No|No|The name of the key pair.|You can specify one of the KeyPairName and Password parameters, but you cannot specify both of them.|
|VolumeId|String|Yes|No|The ID of the Apsara File Storage NAS file system.|Automatic creation of NAS file systems is not supported.|
|EcsOrderManagerInstanceType|String|Yes|No|The instance type of the cluster management nodes.|None|
|Application|List|No|No|The application tags|For more information, see [Application properties](#section_lo0_l5j_nbs).|
|EcsOrderComputeInstanceType|String|Yes|No|The instance type of the compute nodes.|None|
|PeriodUnit|String|No|No|The unit of the billing cycle.|Valid values: -   Week
-   Month
-   Year |
|Description|String|No|Yes|The description of the cluster.|The description must be 2 to 128 characters in length.|
|AutoRenewPeriod|Integer|No|No|The auto-renewal period.|This parameter takes effect when the AutoRenew parameter is set to true.|
|JobQueue|String|No|No|The queue to which the compute nodes belong.|None|
|ImageId|String|No|No|The ID of the image.|-   If the ImageOwnerAlias parameter is set to system, the ImageId parameter is ignored, and the ID of the base image is specified by the OsTag parameter.
-   If the ImageOwnerAlias parameter is set to self, others, or marketplace, the ImageId parameter is required. |
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal.|Valid values:-   true
-   false |
|EhpcVersion|String|Yes|No|The version number of the E-HPC client.|Set the value to 1.0.0.|
|VSwitchId|String|Yes|No|The ID of the VSwitch in the VPC.|E-HPC can be deployed only in VPCs.|
|Password|String|No|No|The root password of the jump server \(logon node\). You can specify one of the KeyPairName and Password parameters, but you cannot specify both of them.|The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `( ) ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? /`

You must use HTTPS to call the operation to ensure that the password remains confidential.|
|Name|String|Yes|Yes|The name of the cluster.|The name must be 2 to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\). It must start with a letter.|
|SchedulerType|String|No|No|The scheduler type.|Set the value to pbs.|
|SccClusterId|String|No|No|The ID of the super computing cluster \(SCC\).|The ID is used to create an SCC instance. If you do not specify this parameter, an SCC instance is created.|
|EcsChargeType|String|No|No|The billing method for the ECS instance that is used by the cluster.|Valid values: -   PostPaid: the pay-as-you-go billing method.
-   PrePaid: the subscription billing method.

If this parameter is set to PrePaid, auto-renewal is enabled by default. After the nodes are released, auto-renewal is disabled.|
|ZoneId|String|No|No|The ID of the zone where the cluster resides.|None|
|EcsOrderLoginCount|Integer|Yes|No|The number of logon nodes in the cluster.|Valid values: 1 to 99.|
|DeployMode|String|No|No|The deployment mode.|Valid values: -   Standard: An account node, a scheduler node, a logon node, and several compute nodes are deployed.
-   Advanced: Two high availability \(HA\) account nodes, two HA scheduler nodes, one logon node, and several compute nodes are deployed.
-   Simple: A cluster management node, a logon node, and several compute nodes are deployed. The account and scheduler nodes are deployed on the cluster management node.
-   Tiny: The account, scheduler, and logon nodes are deployed on a single node. Compute nodes are deployed seperately.
-   OneBox: The account, scheduler, logon, and compute nodes are all deployed on a single node. |
|ImageOwnerAlias|String|No|No|The type of the image.|Valid values: -   system
-   self
-   others
-   marketplace |
|RemoteDirectory|String|No|No|The remote directory that is mounted on the network shared storage.|The mount point directory consists of the mount target and the remote directory: NasMountpoint:/RemoteDirectory.|
|ComputeSpotPriceLimit|String|No|No|The maximum hourly price of the instance.|The value is a floating-point number within the current price range.|
|ComputeSpotStrategy|String|No|No|The bidding policy for the compute nodes.|Valid values: -   NoSpot
-   SpotWithPriceLimit
-   SpotAsPriceGo |
|SecurityGroupName|String|No|No|The name of the security group.|If you do not specify the SecurityGroupId parameter, a security group is created by using the name specified in this parameter, and the default policy is applied.|
|VolumeProtocol|String|No|No|The protocol of the network shared storage.|Set the value to nfs.|
|SecurityGroupId|String|No|No|The ID of the security group.|None|
|Period|Integer|No|No|The unit of the billing cycle.|This parameter takes effect and is required only when the EcsChargeType parameter is set to PrePaid.|
|PostInstallScript|List|No|No|The download URLs and runtime parameters of the script.|You can specify up to 16 sets of download URLs and runtime parameters. For more information, see [PostInstallScript properties](#section_q1u_63i_gf5).|
|AccountType|String|No|No|The service type of the domain account.|Set the value to nis.|
|VolumeMountpoint|String|Yes|No|The NAS mount target in the VPC. Automatic creation of NAS mount targets is not supported.|None|
|EcsOrderLoginInstanceType|String|Yes|No|The instance type of logon nodes.|None|

## Application syntax

```
"Application": [
  {
    "Tag": String
  }
]
```

## Application properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Tag|String|Yes|No|The tag of the application. Example: OpenMPI\_11.1.|None|

## PostInstallScript syntax

```
"PostInstallScript": [
  {
    "Url": String,
    "Args": String
  }
]
```

## PostInstallScript properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Url|String|No|No|The URL that is used to download the script after installation.|None|
|Args|String|No|No|The parameters that are used to run the script after installation.|None|

## Response parameters

Fn::GetAtt

-   EcsInfo: the quantity and instance types of the ECS instances deployed in different nodes of the cluster. Example: `{"Manager": {"Count": 2, "InstanceType": "ecs.n1.large"}, "Compute": {"Count": 8, "InstanceType": "ecs.n1.large"}, "Login": {"Count": 1, "InstanceType": "ecs.n1.large"}}`。
-   SecurityGroupId: the ID of the security group.
-   ClusterId: the ID of the cluster.
-   Name: the name of the cluster.

## Examples

JSON format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Cluster": {
      "Type": "ALIYUN::EHPC::Cluster",
      "Properties": {
        "EcsOrderComputeCount": {
          "Ref": "EcsOrderComputeCount"
        },
        "OsTag": {
          "Ref": "OsTag"
        },
        "HaEnable": {
          "Ref": "HaEnable"
        },
        "VolumeType": {
          "Ref": "VolumeType"
        },
        "Period": {
          "Ref": "Period"
        },
        "EcsOrderManagerInstanceType": {
          "Ref": "EcsOrderManagerInstanceType"
        },
        "Application": {
          "Ref": "Application"
        },
        "EcsOrderComputeInstanceType": {
          "Ref": "EcsOrderComputeInstanceType"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        },
        "Description": {
          "Ref": "Description"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "JobQueue": {
          "Ref": "JobQueue"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Password": {
          "Ref": "Password"
        },
        "Name": {
          "Ref": "Name"
        },
        "SchedulerType": {
          "Ref": "SchedulerType"
        },
        "ComputeSpotPriceLimit": {
          "Ref": "ComputeSpotPriceLimit"
        },
        "EcsChargeType": {
          "Ref": "EcsChargeType"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "EcsOrderLoginCount": {
          "Ref": "EcsOrderLoginCount"
        },
        "DeployMode": {
          "Ref": "DeployMode"
        },
        "ImageOwnerAlias": {
          "Ref": "ImageOwnerAlias"
        },
        "RemoteDirectory": {
          "Ref": "RemoteDirectory"
        },
        "SccClusterId": {
          "Ref": "SccClusterId"
        },
        "ComputeSpotStrategy": {
          "Ref": "ComputeSpotStrategy"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "VolumeProtocol": {
          "Ref": "VolumeProtocol"
        },
        "PostInstallScript": {
          "Ref": "PostInstallScript"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "VolumeId": {
          "Ref": "VolumeId"
        },
        "EhpcVersion": {
          "Ref": "EhpcVersion"
        },
        "AccountType": {
          "Ref": "AccountType"
        },
        "VolumeMountpoint": {
          "Ref": "VolumeMountpoint"
        },
        "EcsOrderLoginInstanceType": {
          "Ref": "EcsOrderLoginInstanceType"
        }
      }
    }
  },
  "Parameters": {
    "EcsOrderComputeCount": {
      "Type": "Number",
      "Description": "Computing the number of cluster nodes, Range: 1-99.",
      "MaxValue": 99,
      "MinValue": 1
    },
    "OsTag": {
      "Type": "String",
      "Description": "Operating system image tag. You can call ListImages API to query."
    },
    "HaEnable": {
      "Type": "Boolean",
      "Description": "Availability is turned on, when turned on, the role of each control cluster will use two standby instances.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "VolumeType": {
      "Type": "String",
      "Description": "Network shared storage types, currently supports only Ali cloud NAS.",
      "AllowedValues": [
        "nas"
      ]
    },
    "Period": {
      "Type": "Number",
      "Description": "The purchase of long resources, units: week / month / year. When the value of the parameter EcsChargeType when PrePaid take effect and for the selected value will be."
    },
    "EcsOrderManagerInstanceType": {
      "Type": "String",
      "Description": "Cluster control node instance specifications."
    },
    "Application": {
      "Type": "Json",
      "Description": "Application software tag (SoftwareTag) list, You can call ListSoftwares API to query."
    },
    "EcsOrderComputeInstanceType": {
      "Type": "String",
      "Description": "Cluster computing node instance specifications."
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "Key pair name."
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "The purchase of long-resources unit. Alternatively value Week / Month / year.",
      "AllowedValues": [
        "Week",
        "Month",
        "Year"
      ]
    },
    "Description": {
      "MinLength": 2,
      "Type": "String",
      "Description": "Cluster description, 2 to 128 characters.",
      "MaxLength": 128
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "Duration of each automatic renewals, AutoRenew take effect when AutoRenew is True."
    },
    "JobQueue": {
      "Type": "String",
      "Description": "Computing node added queue"
    },
    "ImageId": {
      "Type": "String",
      "Description": "Mirror Id, if ImageType a system, based on the image ID is determined only according OsTag; if self, others, or marketplace, ImageId is mandatory."
    },
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "true: automatic renewals; false: no automatic renewals.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VPC in switch ID. Products currently only supports VPC network."
    },
    "Password": {
      "MinLength": 8,
      "Type": "String",
      "Description": "Root password of jump server (login node). 8 to 30 characters, must contain three (upper and lower case letters, numbers and special symbols). ! Supports the following special characters :() `~ @ # $% ^ & * - + = | {} []:; '<>, / Be sure to use the HTTPS protocol API call to avoid password leaks that may occur.?.",
      "MaxLength": 30
    },
    "Name": {
      "Type": "String",
      "Description": "Cluster name. 2-64 characters in length, allowing only include Chinese, letters, numbers, dashes (-) and underscore (_), must begin with a letter or Chinese."
    },
    "SchedulerType": {
      "Type": "String",
      "Description": "The scheduler type, currently support pbs.",
      "AllowedValues": [
        "pbs"
      ]
    },
    "ComputeSpotPriceLimit": {
      "Type": "String",
      "Description": "Set an example of the highest price per hour, are floating-point values, in the range of the current price range."
    },
    "EcsChargeType": {
      "Type": "String",
      "Description": "ECS instance payment type, PostPaid: Pay-As-You-Go.PrePaid: Subscription.If you choose PrePaid, automatic renewal will be enabled by default, and closed when node is released."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Available area ID."
    },
    "EcsOrderLoginCount": {
      "Type": "Number",
      "Description": "Log cluster node number, which ranges from: 1-99.",
      "MaxValue": 99,
      "MinValue": 1
    },
    "DeployMode": {
      "Type": "String",
      "Description": "Deployment mode:\nStandard: account node + scheduling node + login node + computing node.\nAdvanced: HA mode.\nSimple: (account + schedule) node + login node + compute node.\nTiny: (account + scheduling + login) node + compute node.\nOneBox: (account + scheduling + login + compute) node + more compute nodes.",
      "AllowedValues": [
        "Standard",
        "Advanced",
        "Simple",
        "Tiny",
        "OneBox"
      ]
    },
    "ImageOwnerAlias": {
      "Type": "String",
      "Description": "Mirror type: system, self, others or marketplace",
      "AllowedValues": [
        "system",
        "self",
        "others",
        "marketplace"
      ]
    },
    "RemoteDirectory": {
      "Type": "String",
      "Description": "Mount shared storage remote directory. The final path to the mount point and mount the remote directory composition: NasMountpoint: / RemoteDirectory"
    },
    "SccClusterId": {
      "Type": "String",
      "Description": "When SCC models, if you pass this field, then the specified SccCluster create Scc instance, otherwise it will create an instance for the user."
    },
    "ComputeSpotStrategy": {
      "Type": "String",
      "Description": "Compute nodes bidding strategy, value NoSpot, SpotWithPriceLimit or SpotAsPriceGo",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "If you do not use an existing security group (SecurityGroupId is empty), then use this name to create a new security group, the default policy. Format Requirements Reference ECS security group name."
    },
    "VolumeProtocol": {
      "Type": "String",
      "Description": "Shared storage network protocols, currently only supports nfs.",
      "AllowedValues": [
        "nfs"
      ]
    },
    "PostInstallScript": {
      "Type": "Json",
      "Description": ""
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group ID."
    },
    "VolumeId": {
      "Type": "String",
      "Description": "Ali cloud NAS instance Id. Currently it does not support automatic creation Ali cloud NAS instance."
    },
    "EhpcVersion": {
      "Type": "String",
      "Description": "E-HPC product version numbers, currently supports 1.0.0",
      "AllowedValues": [
        "1.0.0"
      ]
    },
    "AccountType": {
      "Type": "String",
      "Description": "Domain service account types, currently supports nis.",
      "AllowedValues": [
        "nis"
      ]
    },
    "VolumeMountpoint": {
      "Type": "String",
      "Description": "NAS vpc mount point. Currently it does not support automatic creation Ali cloud NAS mount point."
    },
    "EcsOrderLoginInstanceType": {
      "Type": "String",
      "Description": "Log cluster node instance specifications."
    }
  },
  "Outputs": {
    "EcsInfo": {
      "Description": "A data structure describing the number and specifications of ECS for various components of the cluster.\nYou will get results similar to the following: EcsInfo: {\"Manager\": {\"Count\": 2, \"InstanceType\": \"ecs.n1.large\"}, \"Compute\": {\"Count\": 8, \"InstanceType\": \"ecs.n1.large\"}, \"Login\": {\"Count\": 1, \"InstanceType\": \"ecs.n1.large\"}}",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "EcsInfo"
        ]
      }
    },
    "SecurityGroupId": {
      "Description": "Security group ID.",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "SecurityGroupId"
        ]
      }
    },
    "ClusterId": {
      "Description": "Cluster Id.",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "ClusterId"
        ]
      }
    },
    "Name": {
      "Description": "Cluster name.",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "Name"
        ]
      }
    }
  }
}
```

YAML format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Cluster:
    Type: 'ALIYUN::EHPC::Cluster'
    Properties:
      EcsOrderComputeCount:
        Ref: EcsOrderComputeCount
      OsTag:
        Ref: OsTag
      HaEnable:
        Ref: HaEnable
      VolumeType:
        Ref: VolumeType
      Period:
        Ref: Period
      EcsOrderManagerInstanceType:
        Ref: EcsOrderManagerInstanceType
      Application:
        Ref: Application
      EcsOrderComputeInstanceType:
        Ref: EcsOrderComputeInstanceType
      KeyPairName:
        Ref: KeyPairName
      PeriodUnit:
        Ref: PeriodUnit
      Description:
        Ref: Description
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      JobQueue:
        Ref: JobQueue
      ImageId:
        Ref: ImageId
      AutoRenew:
        Ref: AutoRenew
      VSwitchId:
        Ref: VSwitchId
      Password:
        Ref: Password
      Name:
        Ref: Name
      SchedulerType:
        Ref: SchedulerType
      ComputeSpotPriceLimit:
        Ref: ComputeSpotPriceLimit
      EcsChargeType:
        Ref: EcsChargeType
      ZoneId:
        Ref: ZoneId
      EcsOrderLoginCount:
        Ref: EcsOrderLoginCount
      DeployMode:
        Ref: DeployMode
      ImageOwnerAlias:
        Ref: ImageOwnerAlias
      RemoteDirectory:
        Ref: RemoteDirectory
      SccClusterId:
        Ref: SccClusterId
      ComputeSpotStrategy:
        Ref: ComputeSpotStrategy
      SecurityGroupName:
        Ref: SecurityGroupName
      VolumeProtocol:
        Ref: VolumeProtocol
      PostInstallScript:
        Ref: PostInstallScript
      SecurityGroupId:
        Ref: SecurityGroupId
      VolumeId:
        Ref: VolumeId
      EhpcVersion:
        Ref: EhpcVersion
      AccountType:
        Ref: AccountType
      VolumeMountpoint:
        Ref: VolumeMountpoint
      EcsOrderLoginInstanceType:
        Ref: EcsOrderLoginInstanceType
Parameters:
  EcsOrderComputeCount:
    Type: Number
    Description: 'Computing the number of cluster nodes, Range: 1-99.'
    MaxValue: 99
    MinValue: 1
  OsTag:
    Type: String
    Description: Operating system image tag. You can call ListImages API to query.
  HaEnable:
    Type: Boolean
    Description: >-
      Availability is turned on, when turned on, the role of each control
      cluster will use two standby instances.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  VolumeType:
    Type: String
    Description: 'Network shared storage types, currently supports only Ali cloud NAS.'
    AllowedValues:
      - nas
  Period:
    Type: Number
    Description: >-
      The purchase of long resources, units: week / month / year. When the value
      of the parameter EcsChargeType when PrePaid take effect and for the
      selected value will be.
  EcsOrderManagerInstanceType:
    Type: String
    Description: Cluster control node instance specifications.
  Application:
    Type: Json
    Description: >-
      Application software tag (SoftwareTag) list, You can call ListSoftwares
      API to query.
  EcsOrderComputeInstanceType:
    Type: String
    Description: Cluster computing node instance specifications.
  KeyPairName:
    Type: String
    Description: Key pair name.
  PeriodUnit:
    Type: String
    Description: >-
      The purchase of long-resources unit. Alternatively value Week / Month /
      year.
    AllowedValues:
      - Week
      - Month
      - Year
  Description:
    MinLength: 2
    Type: String
    Description: 'Cluster description, 2 to 128 characters.'
    MaxLength: 128
  AutoRenewPeriod:
    Type: Number
    Description: >-
      Duration of each automatic renewals, AutoRenew take effect when AutoRenew
      is True.
  JobQueue:
    Type: String
    Description: Computing node added queue
  ImageId:
    Type: String
    Description: >-
      Mirror Id, if ImageType a system, based on the image ID is determined only
      according OsTag; if self, others, or marketplace, ImageId is mandatory.
  AutoRenew:
    Type: Boolean
    Description: 'true: automatic renewals; false: no automatic renewals.'
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  VSwitchId:
    Type: String
    Description: VPC in switch ID. Products currently only supports VPC network.
  Password:
    MinLength: 8
    Type: String
    Description: >-
      Root password of jump server (login node). 8 to 30 characters, must
      contain three (upper and lower case letters, numbers and special symbols).
      ! Supports the following special characters :() `~ @ # $% ^ & * - + = | {}
      []:; '<>, / Be sure to use the HTTPS protocol API call to avoid password
      leaks that may occur.?.
    MaxLength: 30
  Name:
    Type: String
    Description: >-
      Cluster name. 2-64 characters in length, allowing only include Chinese,
      letters, numbers, dashes (-) and underscore (_), must begin with a letter
      or Chinese.
  SchedulerType:
    Type: String
    Description: 'The scheduler type, currently support pbs.'
    AllowedValues:
      - pbs
  ComputeSpotPriceLimit:
    Type: String
    Description: >-
      Set an example of the highest price per hour, are floating-point values,
      in the range of the current price range.
  EcsChargeType:
    Type: String
    Description: >-
      ECS instance payment type, PostPaid: Pay-As-You-Go.PrePaid:
      Subscription.If you choose PrePaid, automatic renewal will be enabled by
      default, and closed when node is released.
  ZoneId:
    Type: String
    Description: Available area ID.
  EcsOrderLoginCount:
    Type: Number
    Description: 'Log cluster node number, which ranges from: 1-99.'
    MaxValue: 99
    MinValue: 1
  DeployMode:
    Type: String
    Description: >-
      Deployment mode:

      Standard: account node + scheduling node + login node + computing node.

      Advanced: HA mode.

      Simple: (account + schedule) node + login node + compute node.

      Tiny: (account + scheduling + login) node + compute node.

      OneBox: (account + scheduling + login + compute) node + more compute
      nodes.
    AllowedValues:
      - Standard
      - Advanced
      - Simple
      - Tiny
      - OneBox
  ImageOwnerAlias:
    Type: String
    Description: 'Mirror type: system, self, others or marketplace'
    AllowedValues:
      - system
      - self
      - others
      - marketplace
  RemoteDirectory:
    Type: String
    Description: >-
      Mount shared storage remote directory. The final path to the mount point
      and mount the remote directory composition: NasMountpoint: /
      RemoteDirectory
  SccClusterId:
    Type: String
    Description: >-
      When SCC models, if you pass this field, then the specified SccCluster
      create Scc instance, otherwise it will create an instance for the user.
  ComputeSpotStrategy:
    Type: String
    Description: >-
      Compute nodes bidding strategy, value NoSpot, SpotWithPriceLimit or
      SpotAsPriceGo
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
  SecurityGroupName:
    Type: String
    Description: >-
      If you do not use an existing security group (SecurityGroupId is empty),
      then use this name to create a new security group, the default policy.
      Format Requirements Reference ECS security group name.
  VolumeProtocol:
    Type: String
    Description: 'Shared storage network protocols, currently only supports nfs.'
    AllowedValues:
      - nfs
  PostInstallScript:
    Type: Json
    Description: ''
  SecurityGroupId:
    Type: String
    Description: Security group ID.
  VolumeId:
    Type: String
    Description: >-
      Ali cloud NAS instance Id. Currently it does not support automatic
      creation Ali cloud NAS instance.
  EhpcVersion:
    Type: String
    Description: 'E-HPC product version numbers, currently supports 1.0.0'
    AllowedValues:
      - 1.0.0
  AccountType:
    Type: String
    Description: 'Domain service account types, currently supports nis.'
    AllowedValues:
      - nis
  VolumeMountpoint:
    Type: String
    Description: >-
      NAS vpc mount point. Currently it does not support automatic creation Ali
      cloud NAS mount point.
  EcsOrderLoginInstanceType:
    Type: String
    Description: Log cluster node instance specifications.
Outputs:
  EcsInfo:
    Description: >-
      A data structure describing the number and specifications of ECS for
      various components of the cluster.

      You will get results similar to the following: EcsInfo: {"Manager":
      {"Count": 2, "InstanceType": "ecs.n1.large"}, "Compute": {"Count": 8,
      "InstanceType": "ecs.n1.large"}, "Login": {"Count": 1, "InstanceType":
      "ecs.n1.large"}}
    Value:
      'Fn::GetAtt':
        - Cluster
        - EcsInfo
  SecurityGroupId:
    Description: Security group ID.
    Value:
      'Fn::GetAtt':
        - Cluster
        - SecurityGroupId
  ClusterId:
    Description: Cluster Id.
    Value:
      'Fn::GetAtt':
        - Cluster
        - ClusterId
  Name:
    Description: Cluster name.
    Value:
      'Fn::GetAtt':
        - Cluster
        - Name
```


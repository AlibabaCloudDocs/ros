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
    "EcsOrderManagerCount": Integer,
    "EcsOrderManagerInstanceType": String,
    "EcsOrderComputeInstanceType": String,
    "Application": List,
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
|OsTag|String|Yes|No|The operating system image.|Example: CentOS\_7.2\_64.|
|HaEnable|Boolean|No|No|Specifies whether high availability is enabled.|Valid values:-   true

**Note:** If high availability is enabled, each management role in the cluster uses a primary instance and a secondary instance.

-   false |
|VolumeType|String|No|No|The type of the network shared storage.|Set the value to nas.|
|KeyPairName|String|No|No|The name of the key pair.|You can specify one of the KeyPairName and Password parameters, but you cannot specify both of them.|
|VolumeId|String|Yes|No|The ID of the Apsara File Storage NAS file system.|Automatic creation of NAS file systems is not supported.|
|EcsOrderManagerCount|Integer|No|No|The instance type of the cluster management nodes.|Valid values:-   1
-   2
-   4 |
|EcsOrderManagerInstanceType|String|Yes|No|The instance type of the cluster management node.|None|
|Application|List|No|No|The list of applications.|For more information, see [Application properties](#section_lo0_l5j_nbs).|
|EcsOrderComputeInstanceType|String|Yes|No|The instance type of the compute nodes.|None|
|PeriodUnit|String|No|No|The unit of the billing cycle.|Valid values: -   Week
-   Month
-   Year |
|Description|String|No|Yes|The description of the cluster.|The description must be 2 to 128 characters in length.|
|AutoRenewPeriod|Integer|No|No|The auto-renewal period.|This parameter takes effect when the AutoRenew parameter is set to true.|
|JobQueue|String|No|No|The queue to which the compute nodes belong.|None|
|ImageId|String|No|No|The ID of the image.|If the ImageOwnerAlias parameter is set to system, the ImageId parameter is ignored, and the ID of the base image is specified by the OsTag parameter.

If the ImageOwnerAlias parameter is set to self, others, or marketplace, the ImageId parameter is required.|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal.|Valid values:-   true
-   false |
|EhpcVersion|String|Yes|No|The version number of the E-HPC client.|Set the value to 1.0.0.|
|VSwitchId|String|Yes|No|The ID of the VSwitch in the VPC.|E-HPC can be deployed only in VPCs.|
|Password|String|No|No|The root password of the jump server \(logon node\). You can specify one of the KeyPairName and Password parameters, but you cannot specify both of them.|The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include ```
( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? / 
```

You must use HTTPS to call the operation to ensure that the password remains confidential.|
|Name|String|Yes|Yes|The name of the cluster.|The name must be 2 to 64 characters in length and can contain letters, digits, hyphens \(-\), and underscores \(\_\). It must start with a letter.|
|SchedulerType|String|No|No|The scheduler type.|Set the value to pbs.|
|SccClusterId|String|No|No|The ID of the super computing cluster \(SCC\).|The ID is used to create an SCC instance. If you do not specify this parameter, an SCC instance is created.|
|EcsChargeType|String|No|No|The billing method for the ECS instance that is used by the cluster.|Valid values: -   PostPaid: the pay-as-you-go billing method
-   PrePaid: the subscription billing method

**Note:** If this parameter is set to PrePaid, auto-renewal is enabled by default. After the nodes are released, auto-renewal is disabled. |
|ZoneId|String|No|No|The ID of the zone.|None|
|EcsOrderLoginCount|Integer|Yes|No|The number of logon nodes in the cluster.|Valid values: 1 to 99.|
|DeployMode|String|No|No|The deployment mode.|Valid values: -   Standard: An account node, a scheduler node, a logon node, and several compute nodes are deployed.
-   Advanced: Two high availability \(HA\) account nodes, two HA scheduler nodes, one logon node, and several compute nodes are deployed.
-   Simple: A cluster management node, a logon node, and several compute nodes are deployed. The account and scheduler nodes are deployed on the cluster management node.
-   Tiny: The account, scheduler, and logon nodes are deployed on a single node. Compute nodes are deployed separately.
-   OneBox: The account, scheduler, logon, and compute nodes are all deployed on a single node. |
|ImageOwnerAlias|String|No|No|The type of the image.|Valid values: -   system
-   self
-   others
-   marketplace |
|RemoteDirectory|String|No|No|The remote directory mounted on the network shared storage.|The mount point directory consists of the mount target and the remote directory: `NasMountpoint:/RemoteDirectory`.|
|ComputeSpotPriceLimit|String|No|No|The maximum hourly price of the instance.|The value is a floating-point number within the current price range.|
|ComputeSpotStrategy|String|No|No|The bidding policy for the compute nodes.|Valid values: -   NoSpot
-   SpotWithPriceLimit
-   SpotAsPriceGo |
|SecurityGroupName|String|No|No|The name of the security group.|If you do not specify the SecurityGroupId parameter, a security group is created by using the name specified in this parameter, and the default policy is applied.|
|VolumeProtocol|String|No|No|The protocol of the network shared storage.|Set the value to nfs.|
|SecurityGroupId|String|No|No|The ID of the security group.|None|
|Period|Integer|No|No|The subscription period.|This parameter takes effect and is required only when the EcsChargeType parameter is set to PrePaid.|
|PostInstallScript|List|No|No|The download URLs and runtime parameters of the script.|You can specify up to 16 sets of download URLs and runtime parameters. For more information, see [PostInstallScript properties](#section_q1u_63i_gf5).|
|AccountType|String|No|No|The service type of the domain account.|Set the value to nis.|
|VolumeMountpoint|String|Yes|No|The NAS mount target in the VPC.|Automatic creation of NAS mount targets is not supported.|
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
|Tag|String|Yes|No|The tag of the application.|Example: OpenMPI\_11.1.|

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
|Args|String|No|No|The parameters that are used to run the script after installation.|None.|

## Response parameters

Fn::GetAtt

-   EcsInfo: the quantity and instance types of the ECS instances deployed in different nodes of the cluster. Example: `{"Manager": {"Count": 2, "InstanceType": "ecs.n1.large"}, "Compute": {"Count": 8, "InstanceType": "ecs.n1.large"}, "Login": {"Count": 1, "InstanceType": "ecs.n1.large"}}`.
-   SecurityGroupId: the ID of the security group.
-   ClusterId: the ID of the cluster.
-   Name: the name of the cluster.

## Examples

JSON format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
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
    "VolumeProtocol": {
      "Type": "String",
      "Description": "Shared storage network protocols, currently only supports nfs.",
      "AllowedValues": [
        "nfs"
      ]
    },
    "EcsOrderComputeCount": {
      "Type": "Number",
      "Description": "Computing node number, which ranges from: 1-99.",
      "MinValue": 1,
      "MaxValue": 99
    },
    "Description": {
      "Type": "String",
      "Description": "Cluster description, 2 to 128 characters.",
      "MinLength": 2,
      "MaxLength": 128
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "If you do not use an existing security group (SecurityGroupId is empty), then use this name to create a new security group, the default policy. Format Requirements Reference ECS security group name."
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
    "ComputeSpotPriceLimit": {
      "Type": "String",
      "Description": "Set an example of the highest price per hour, are floating-point values, in the range of the current price range."
    },
    "Name": {
      "Type": "String",
      "Description": "Cluster name. 2-64 characters in length, allowing only include Chinese, letters, numbers, dashes (-) and underscore (_), must begin with a letter or Chinese."
    },
    "VolumeId": {
      "Type": "String",
      "Description": "Ali cloud NAS instance Id. Currently it does not support automatic creation Ali cloud NAS instance."
    },
    "VolumeType": {
      "Type": "String",
      "Description": "Network shared storage types, currently supports only Ali cloud NAS.",
      "AllowedValues": [
        "nas"
      ]
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
    "PostInstallScript": {
      "Type": "Json",
      "Description": ""
    },
    "ImageId": {
      "Type": "String",
      "Description": "Mirror Id, if ImageType a system, based on the image ID is determined only according OsTag; if self, others, or marketplace, ImageId is mandatory."
    },
    "Password": {
      "Type": "String",
      "Description": "Root password of jump server (login node). 8 to 30 characters, must contain three (upper and lower case letters, numbers and special symbols). ! Supports the following special characters :() `~ @ # $% ^ & * - + = | {} []:; '<>, / Be sure to use the HTTPS protocol API call to avoid password leaks that may occur.?.",
      "MinLength": 8,
      "MaxLength": 30
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "Duration of each automatic renewals, AutoRenew take effect when AutoRenew is True."
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "Key pair name."
    },
    "RemoteDirectory": {
      "Type": "String",
      "Description": "Mount shared storage remote directory. The final path to the mount point and mount the remote directory composition: NasMountpoint: / RemoteDirectory"
    },
    "SccClusterId": {
      "Type": "String",
      "Description": "When SCC models, if you pass this field, then the specified SccCluster create Scc instance, otherwise it will create an instance for the user."
    },
    "EcsOrderLoginInstanceType": {
      "Type": "String",
      "Description": "Log cluster node instance specifications."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Available area ID."
    },
    "JobQueue": {
      "Type": "String",
      "Description": "Computing node added queue"
    },
    "EcsOrderLoginCount": {
      "Type": "Number",
      "Description": "Log node number, which ranges from: 1-99.",
      "MinValue": 1,
      "MaxValue": 99
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VPC in switch ID. Products currently only supports VPC network."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group ID."
    },
    "Period": {
      "Type": "Number",
      "Description": "The purchase of long resources, units: week / month / year. When the value of the parameter EcsChargeType when PrePaid take effect and for the selected value will be."
    },
    "SchedulerType": {
      "Type": "String",
      "Description": "The scheduler type, currently support pbs.",
      "AllowedValues": [
        "pbs"
      ]
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
    "AccountType": {
      "Type": "String",
      "Description": "Domain service account types, currently supports nis.",
      "AllowedValues": [
        "nis"
      ]
    },
    "EcsOrderManagerInstanceType": {
      "Type": "String",
      "Description": "Cluster control node instance specifications."
    },
    "EhpcVersion": {
      "Type": "String",
      "Description": "E-HPC product version numbers, currently supports 1.0.0",
      "AllowedValues": [
        "1.0.0"
      ]
    },
    "VolumeMountpoint": {
      "Type": "String",
      "Description": "NAS vpc mount point. Currently it does not support automatic creation Ali cloud NAS mount point."
    },
    "EcsOrderManagerCount": {
      "Type": "Number",
      "Description": "Control node number, which ranges from: 1-99.",
      "MinValue": 1,
      "MaxValue": 99
    },
    "EcsOrderComputeInstanceType": {
      "Type": "String",
      "Description": "Cluster computing node instance specifications."
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
    "OsTag": {
      "Type": "String",
      "Description": "Operating system image tag. You can call ListImages API to query."
    },
    "EcsChargeType": {
      "Type": "String",
      "Description": "ECS instance payment type, PostPaid: Pay-As-You-Go.PrePaid: Subscription.If you choose PrePaid, automatic renewal will be enabled by default, and closed when node is released."
    },
    "Application": {
      "Type": "Json",
      "Description": "Application software tag (SoftwareTag) list, You can call ListSoftwares API to query."
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "The purchase of long-resources unit. Alternatively value Week / Month / year.",
      "AllowedValues": [
        "Week",
        "Month",
        "Year"
      ]
    }
  },
  "Resources": {
    "Cluster": {
      "Type": "ALIYUN::EHPC::Cluster",
      "Properties": {
        "ImageOwnerAlias": {
          "Ref": "ImageOwnerAlias"
        },
        "VolumeProtocol": {
          "Ref": "VolumeProtocol"
        },
        "EcsOrderComputeCount": {
          "Ref": "EcsOrderComputeCount"
        },
        "Description": {
          "Ref": "Description"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "ComputeSpotPriceLimit": {
          "Ref": "ComputeSpotPriceLimit"
        },
        "Name": {
          "Ref": "Name"
        },
        "VolumeId": {
          "Ref": "VolumeId"
        },
        "VolumeType": {
          "Ref": "VolumeType"
        },
        "DeployMode": {
          "Ref": "DeployMode"
        },
        "PostInstallScript": {
          "Ref": "PostInstallScript"
        },
        "ImageId": {
          "Ref": "ImageId"
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
        "RemoteDirectory": {
          "Ref": "RemoteDirectory"
        },
        "SccClusterId": {
          "Ref": "SccClusterId"
        },
        "EcsOrderLoginInstanceType": {
          "Ref": "EcsOrderLoginInstanceType"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "JobQueue": {
          "Ref": "JobQueue"
        },
        "EcsOrderLoginCount": {
          "Ref": "EcsOrderLoginCount"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "SchedulerType": {
          "Ref": "SchedulerType"
        },
        "ComputeSpotStrategy": {
          "Ref": "ComputeSpotStrategy"
        },
        "AccountType": {
          "Ref": "AccountType"
        },
        "EcsOrderManagerInstanceType": {
          "Ref": "EcsOrderManagerInstanceType"
        },
        "EhpcVersion": {
          "Ref": "EhpcVersion"
        },
        "VolumeMountpoint": {
          "Ref": "VolumeMountpoint"
        },
        "EcsOrderManagerCount": {
          "Ref": "EcsOrderManagerCount"
        },
        "EcsOrderComputeInstanceType": {
          "Ref": "EcsOrderComputeInstanceType"
        },
        "HaEnable": {
          "Ref": "HaEnable"
        },
        "OsTag": {
          "Ref": "OsTag"
        },
        "EcsChargeType": {
          "Ref": "EcsChargeType"
        },
        "Application": {
          "Ref": "Application"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "ClusterId": {
      "Description": "Cluster Id.",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "ClusterId"
        ]
      }
    },
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
Parameters:
  ImageOwnerAlias:
    Type: String
    Description: 'Mirror type: system, self, others or marketplace'
    AllowedValues:
      - system
      - self
      - others
      - marketplace
  VolumeProtocol:
    Type: String
    Description: 'Shared storage network protocols, currently only supports nfs.'
    AllowedValues:
      - nfs
  EcsOrderComputeCount:
    Type: Number
    Description: 'Computing node number, which ranges from: 1-99.'
    MinValue: 1
    MaxValue: 99
  Description:
    Type: String
    Description: 'Cluster description, 2 to 128 characters.'
    MinLength: 2
    MaxLength: 128
  SecurityGroupName:
    Type: String
    Description: >-
      If you do not use an existing security group (SecurityGroupId is empty),
      then use this name to create a new security group, the default policy.
      Format Requirements Reference ECS security group name.
  AutoRenew:
    Type: Boolean
    Description: 'true: automatic renewals; false: no automatic renewals.'
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  ComputeSpotPriceLimit:
    Type: String
    Description: >-
      Set an example of the highest price per hour, are floating-point values,
      in the range of the current price range.
  Name:
    Type: String
    Description: >-
      Cluster name. 2-64 characters in length, allowing only include Chinese,
      letters, numbers, dashes (-) and underscore (_), must begin with a letter
      or Chinese.
  VolumeId:
    Type: String
    Description: >-
      Ali cloud NAS instance Id. Currently it does not support automatic
      creation Ali cloud NAS instance.
  VolumeType:
    Type: String
    Description: 'Network shared storage types, currently supports only Ali cloud NAS.'
    AllowedValues:
      - nas
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
  PostInstallScript:
    Type: Json
    Description: ''
  ImageId:
    Type: String
    Description: >-
      Mirror Id, if ImageType a system, based on the image ID is determined only
      according OsTag; if self, others, or marketplace, ImageId is mandatory.
  Password:
    Type: String
    Description: >-
      Root password of jump server (login node). 8 to 30 characters, must
      contain three (upper and lower case letters, numbers and special symbols).
      ! Supports the following special characters :() `~ @ # $% ^ & * - + = | {}
      []:; '<>, / Be sure to use the HTTPS protocol API call to avoid password
      leaks that may occur.?.
    MinLength: 8
    MaxLength: 30
  AutoRenewPeriod:
    Type: Number
    Description: >-
      Duration of each automatic renewals, AutoRenew take effect when AutoRenew
      is True.
  KeyPairName:
    Type: String
    Description: Key pair name.
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
  EcsOrderLoginInstanceType:
    Type: String
    Description: Log cluster node instance specifications.
  ZoneId:
    Type: String
    Description: Available area ID.
  JobQueue:
    Type: String
    Description: Computing node added queue
  EcsOrderLoginCount:
    Type: Number
    Description: 'Log node number, which ranges from: 1-99.'
    MinValue: 1
    MaxValue: 99
  VSwitchId:
    Type: String
    Description: VPC in switch ID. Products currently only supports VPC network.
  SecurityGroupId:
    Type: String
    Description: Security group ID.
  Period:
    Type: Number
    Description: >-
      The purchase of long resources, units: week / month / year. When the value
      of the parameter EcsChargeType when PrePaid take effect and for the
      selected value will be.
  SchedulerType:
    Type: String
    Description: 'The scheduler type, currently support pbs.'
    AllowedValues:
      - pbs
  ComputeSpotStrategy:
    Type: String
    Description: >-
      Compute nodes bidding strategy, value NoSpot, SpotWithPriceLimit or
      SpotAsPriceGo
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
  AccountType:
    Type: String
    Description: 'Domain service account types, currently supports nis.'
    AllowedValues:
      - nis
  EcsOrderManagerInstanceType:
    Type: String
    Description: Cluster control node instance specifications.
  EhpcVersion:
    Type: String
    Description: 'E-HPC product version numbers, currently supports 1.0.0'
    AllowedValues:
      - 1.0.0
  VolumeMountpoint:
    Type: String
    Description: >-
      NAS vpc mount point. Currently it does not support automatic creation Ali
      cloud NAS mount point.
  EcsOrderManagerCount:
    Type: Number
    Description: 'Control node number, which ranges from: 1-99.'
    MinValue: 1
    MaxValue: 99
  EcsOrderComputeInstanceType:
    Type: String
    Description: Cluster computing node instance specifications.
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
  OsTag:
    Type: String
    Description: Operating system image tag. You can call ListImages API to query.
  EcsChargeType:
    Type: String
    Description: >-
      ECS instance payment type, PostPaid: Pay-As-You-Go.PrePaid:
      Subscription.If you choose PrePaid, automatic renewal will be enabled by
      default, and closed when node is released.
  Application:
    Type: Json
    Description: >-
      Application software tag (SoftwareTag) list, You can call ListSoftwares
      API to query.
  PeriodUnit:
    Type: String
    Description: >-
      The purchase of long-resources unit. Alternatively value Week / Month /
      year.
    AllowedValues:
      - Week
      - Month
      - Year
Resources:
  Cluster:
    Type: 'ALIYUN::EHPC::Cluster'
    Properties:
      ImageOwnerAlias:
        Ref: ImageOwnerAlias
      VolumeProtocol:
        Ref: VolumeProtocol
      EcsOrderComputeCount:
        Ref: EcsOrderComputeCount
      Description:
        Ref: Description
      SecurityGroupName:
        Ref: SecurityGroupName
      AutoRenew:
        Ref: AutoRenew
      ComputeSpotPriceLimit:
        Ref: ComputeSpotPriceLimit
      Name:
        Ref: Name
      VolumeId:
        Ref: VolumeId
      VolumeType:
        Ref: VolumeType
      DeployMode:
        Ref: DeployMode
      PostInstallScript:
        Ref: PostInstallScript
      ImageId:
        Ref: ImageId
      Password:
        Ref: Password
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      KeyPairName:
        Ref: KeyPairName
      RemoteDirectory:
        Ref: RemoteDirectory
      SccClusterId:
        Ref: SccClusterId
      EcsOrderLoginInstanceType:
        Ref: EcsOrderLoginInstanceType
      ZoneId:
        Ref: ZoneId
      JobQueue:
        Ref: JobQueue
      EcsOrderLoginCount:
        Ref: EcsOrderLoginCount
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      SchedulerType:
        Ref: SchedulerType
      ComputeSpotStrategy:
        Ref: ComputeSpotStrategy
      AccountType:
        Ref: AccountType
      EcsOrderManagerInstanceType:
        Ref: EcsOrderManagerInstanceType
      EhpcVersion:
        Ref: EhpcVersion
      VolumeMountpoint:
        Ref: VolumeMountpoint
      EcsOrderManagerCount:
        Ref: EcsOrderManagerCount
      EcsOrderComputeInstanceType:
        Ref: EcsOrderComputeInstanceType
      HaEnable:
        Ref: HaEnable
      OsTag:
        Ref: OsTag
      EcsChargeType:
        Ref: EcsChargeType
      Application:
        Ref: Application
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  ClusterId:
    Description: Cluster Id.
    Value:
      'Fn::GetAtt':
        - Cluster
        - ClusterId
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
  Name:
    Description: Cluster name.
    Value:
      'Fn::GetAtt':
        - Cluster
        - Name
```


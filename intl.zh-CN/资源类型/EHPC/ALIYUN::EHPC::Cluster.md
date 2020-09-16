# ALIYUN::EHPC::Cluster

ALIYUN::EHPC::Cluster类型用于创建一个弹性高性能计算集群。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EcsOrderComputeCount|Integer|是|否|集群计算节点数量|取值：1~99|
|OsTag|String|是|否|操作系统镜像，例如：CentOS\_7.2\_64。|无|
|HaEnable|Boolean|否|否|是否开启高可用。如果开启，集群中的每种管控角色将会使用主备2台实例。|无|
|VolumeType|String|否|否|网络共享存储类型|取值：nas|
|KeyPairName|String|否|否|密钥对|与Password二选一。|
|VolumeId|String|是|否|阿里云NAS实例ID|目前不支持自动创建阿里云NAS实例。|
|EcsOrderManagerInstanceType|String|是|否|集群管控节点实例规格|无|
|Application|List|否|否|应用软件的标签|详情请参见[Application属性](#section_lo0_l5j_nbs)。|
|EcsOrderComputeInstanceType|String|是|否|集群计算节点实例规格|无|
|PeriodUnit|String|否|否|购买资源的时长单位|取值： -   Week
-   Month
-   Year |
|Description|String|否|是|集群描述|长度为2~128个字符|
|AutoRenewPeriod|Integer|否|否|每次自动续费的时长|当AutoRenew取值为true时生效|
|JobQueue|String|否|否|计算节点加入的队列|无|
|ImageId|String|否|否|镜像ID|-   如果ImageOwnerAlias取值为system， 则只根据OsTag来决定基础镜像ID。
-   如果ImageOwnerAlias取值为self、others或marketplace， 则ImageId必填。 |
|AutoRenew|Boolean|否|否|是否自动续费|取值： -   true
-   false |
|EhpcVersion|String|是|否|E-HPC产品版本号|取值：1.0.0|
|VSwitchId|String|是|否|VPC中交换机ID|产品目前只支持VPC网络。|
|Password|String|否|否|跳板机（Login 节点）的root密码，与KeyPairName二选一。|长度为8~30个字符，必须同时包含三项（大写字母、小写字母、数字和特殊符号）。支持特殊字符： `( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? /`。

 请务必使用HTTPS协议调用API，避免可能发生的密码泄露。|
|Name|String|是|是|集群名字|长度2~64字符，只允许包含汉字、字母、数字、短划线（-）和下划线（\_），必须以字母或汉字开头。|
|SchedulerType|String|否|否|调度器类型|取值：pbs|
|SccClusterId|String|否|否|SCC集群ID|当使用SCC机型时，如果传入此字段，则使用指定的SccCluster创建Scc实例，否则将自动创建一个实例。|
|EcsChargeType|String|否|否|集群使用ECS实例的付费类型|取值： -   PostPaid：按量付费。
-   PrePaid：包年包月。

 若选择包年包月类型，默认开启自动续费，节点释放后将关闭自动续费。|
|ZoneId|String|否|否|可用区ID|无|
|EcsOrderLoginCount|Integer|是|否|集群登录节点数量|取值：1~99|
|DeployMode|String|否|否|部署模式|取值： -   Standard：账号节点+调度节点+登录节点+计算节点
-   Advanced：HA模式
-   Simple：（账号+调度）节点+登录节点+计算节点
-   Tiny：（账号+调度+登录）节点+计算节点
-   OneBox：（账号+调度+登录+计算）节点+更多计算节点 |
|ImageOwnerAlias|String|否|否|镜像类型|取值： -   system
-   self
-   others
-   marketplace |
|RemoteDirectory|String|否|否|挂载共享存储的远程目录|最终挂载路径为挂载点与远程目录组合：NasMountpoint:/RemoteDirectory。|
|ComputeSpotPriceLimit|String|否|否|设置实例的每小时最高价格|取值是浮点数，为当前的价格区间。|
|ComputeSpotStrategy|String|否|否|计算节点竞价策略|取值： -   NoSpot
-   SpotWithPriceLimit
-   SpotAsPriceGo |
|SecurityGroupName|String|否|否|安全组名称|如果没有传SecurityGroupId，则使用这个名字创建新安全组，应用默认策略。|
|VolumeProtocol|String|否|否|网络共享存储协议|取值：nfs|
|SecurityGroupId|String|否|否|安全组ID|无|
|Period|Integer|否|否|购买资源的时长|当参数EcsChargeType取值为PrePaid时才生效，且为必选值。|
|PostInstallScript|List|否|否|脚本的下载地址和执行参数|最多指定16组下载地址和执行参数。详情请参见[PostInstallScript属性](#section_q1u_63i_gf5)。|
|AccountType|String|否|否|域账号服务类型|取值：nis|
|VolumeMountpoint|String|是|否|NAS VPC挂载点。目前不支持自动创建阿里云NAS挂载点。|无|
|EcsOrderLoginInstanceType|String|是|否|集群登录节点实例规格|无|

## Application语法

```
"Application": [
  {
    "Tag": String
  }
]
```

## Application属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Tag|String|是|否|应用软件的标签，例如：OpenMPI\_11.1。|无|

## PostInstallScript语法

```
"PostInstallScript": [
  {
    "Url": String,
    "Args": String
  }
]
```

## PostInstallScript属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Url|String|否|否|安装后脚本的下载地址|无|
|Args|String|否|否|安装后脚本的执行参数|无|

## 返回值

Fn::GetAtt

-   EcsInfo：集群中各组件的ECS数量和规格，例如： `{"Manager": {"Count": 2, "InstanceType": "ecs.n1.large"}, "Compute": {"Count": 8, "InstanceType": "ecs.n1.large"}, "Login": {"Count": 1, "InstanceType": "ecs.n1.large"}}`。
-   SecurityGroupId：安全组ID。
-   ClusterId：集群ID。
-   Name：集群名称。

## 示例

JSON格式

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

YAML格式

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


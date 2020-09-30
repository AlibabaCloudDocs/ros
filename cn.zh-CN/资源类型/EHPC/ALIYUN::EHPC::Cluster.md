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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EcsOrderComputeCount|Integer|是|否|集群计算节点数量。|取值：1~99|
|OsTag|String|是|否|操作系统镜像。|例如：CentOS\_7.2\_64。|
|HaEnable|Boolean|否|否|是否开启高可用。|取值：-   true：开启。

**说明：** 如果开启，集群中的每种管控角色将会使用主备2台实例。

-   false：不开启。 |
|VolumeType|String|否|否|网络共享存储类型。|取值：nas。|
|KeyPairName|String|否|否|密钥对。|与Password二选一。|
|VolumeId|String|是|否|阿里云NAS实例ID。|目前不支持自动创建阿里云NAS实例。|
|EcsOrderManagerCount|Integer|否|否|集群管控节点实例数量。|取值：-   1
-   2
-   4 |
|EcsOrderManagerInstanceType|String|是|否|集群管控节点实例规格。|无|
|Application|List|否|否|应用软件。|详情请参见[Application属性](#section_lo0_l5j_nbs)。|
|EcsOrderComputeInstanceType|String|是|否|集群计算节点实例规格。|无|
|PeriodUnit|String|否|否|购买资源的时长单位。|取值： -   Week
-   Month
-   Year |
|Description|String|否|是|集群描述。|2~128个字符。|
|AutoRenewPeriod|Integer|否|否|每次自动续费的时长。|当AutoRenew取值为true时生效。|
|JobQueue|String|否|否|计算节点加入的队列。|无|
|ImageId|String|否|否|镜像ID。|如果ImageOwnerAlias取值为system， 则只根据OsTag来决定基础镜像ID。

如果ImageOwnerAlias取值为self、others或marketplace， 则ImageId必填。|
|AutoRenew|Boolean|否|否|是否自动续费。|取值：-   true
-   false |
|EhpcVersion|String|是|否|E-HPC产品版本号。|取值：1.0.0。|
|VSwitchId|String|是|否|专有网络中交换机ID。|产品目前仅支持专有网络。|
|Password|String|否|否|跳板机（Login 节点）的root密码，与KeyPairName二选一。|长度为8~30个字符，必须同时包含三项大写英文字母、小写英文字母、数字和特殊字符其中三项。支持的特殊字符如下： ```
( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? / 
```

请务必使用HTTPS协议调用API，避免可能发生的密码泄露。|
|Name|String|是|是|集群名称。|长度为2~64个字符，必须以英文字母或汉字开头。可包含英文字母、汉字、数字、短划线（-）和下划线（\_）。|
|SchedulerType|String|否|否|调度器类型。|取值：pbs。|
|SccClusterId|String|否|否|SCC集群ID。|使用SCC机型时，如果传入此字段，则使用指定的SccCluster创建Scc实例，否则将自动创建一个实例。|
|EcsChargeType|String|否|否|集群使用ECS实例的付费类型。|取值： -   PostPaid：按量付费。
-   PrePaid：包年包月。

**说明：** 如果选择包年包月类型，默认开启自动续费，节点释放后将关闭自动续费。 |
|ZoneId|String|否|否|可用区ID。|无|
|EcsOrderLoginCount|Integer|是|否|集群登录节点数量。|取值范围：1~99。|
|DeployMode|String|否|否|部署模式。|取值： -   Standard：账号节点+调度节点+登录节点+计算节点。
-   Advanced：HA模式。
-   Simple：（账号+调度）节点+登录节点+计算节点。
-   Tiny：（账号+调度+登录）节点+计算节点。
-   OneBox：（账号+调度+登录+计算）节点+更多计算节点。 |
|ImageOwnerAlias|String|否|否|镜像类型。|取值： -   system
-   self
-   others
-   marketplace |
|RemoteDirectory|String|否|否|挂载共享存储的远程目录。|最终挂载路径为挂载点与远程目录组合：`NasMountpoint:/RemoteDirectory`。|
|ComputeSpotPriceLimit|String|否|否|设置实例的每小时最高价格。|取值是浮点数，为当前的价格区间。|
|ComputeSpotStrategy|String|否|否|计算节点竞价策略。|取值： -   NoSpot
-   SpotWithPriceLimit
-   SpotAsPriceGo |
|SecurityGroupName|String|否|否|安全组名称。|如果没有传SecurityGroupId，则使用这个名字创建新安全组，应用默认策略。|
|VolumeProtocol|String|否|否|网络共享存储协议。|取值：nfs|
|SecurityGroupId|String|否|否|安全组ID。|无|
|Period|Integer|否|否|购买资源的时长。|EcsChargeType取值为PrePaid时该参数生效，且为必选值。|
|PostInstallScript|List|否|否|脚本的下载地址和执行参数。|最多指定16组下载地址和执行参数。详情请参见[PostInstallScript属性](#section_q1u_63i_gf5)。|
|AccountType|String|否|否|域账号服务类型。|取值：nis。|
|VolumeMountpoint|String|是|否|NAS VPC挂载点。|目前不支持自动创建阿里云NAS挂载点。|
|EcsOrderLoginInstanceType|String|是|否|集群登录节点实例规格。|无|

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
|Tag|String|是|否|应用软件的标签。|例如：OpenMPI\_11.1。|

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
|Url|String|否|否|安装后脚本的下载地址。|无|
|Args|String|否|否|安装后脚本的执行参数。|无|

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

YAML格式

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


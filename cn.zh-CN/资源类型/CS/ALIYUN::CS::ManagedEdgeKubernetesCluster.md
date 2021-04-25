# ALIYUN::CS::ManagedEdgeKubernetesCluster

ALIYUN::CS::ManagedEdgeKubernetesCluster类型用于创建Kubernetes边缘托管版集群实例。

## 语法

```
{
  "Type": "ALIYUN::CS::ManagedEdgeKubernetesCluster",
  "Properties": {
    "NumOfNodes": Number,
    "Profile": String,
    "VpcId": String,
    "ServiceCidr": String,
    "Name": String,
    "Tags": List,
    "ProxyMode": String,
    "DisableRollback": Boolean,
    "SnatEntry": Boolean,
    "VSwitchIds": List,
    "LoginPassword": String,
    "WorkerSystemDiskSize": Number,
    "KeyPair": String,
    "Addons": List,
    "WorkerDataDiskCategory": String,
    "EndpointPublicAccess": Boolean,
    "WorkerDataDisk": Boolean,
    "WorkerSystemDiskCategory": String,
    "WorkerDataDiskSize": Integer,
    "TimeoutMins": Number,
    "ClusterSpec": String,
    "ContainerCidr": String,
    "CloudMonitorFlags": Boolean,
    "WorkerInstanceTypes": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NumOfNodes|Number|是|否|Worker节点数。|取值范围：0~300。|
|Profile|String|否|否|边缘集群标识。|默认值：Edge。|
|VpcId|String|否|否|专有网络ID。|如果不设置，系统会自动创建专有网络，系统创建的专有网络网段为192.168.0.0/16。VpcId和VSwitchIds只能同时为空或者同时都设置对应的值。 |
|ServiceCidr|String|否|否|服务网段。|不能与专有网络网段以及容器网段冲突。当选择系统自动创建专有网络时，默认使用172.19.0.0/20网段。|
|Name|String|是|否|集群名称。|以英文字母或数字开头，可包含英文字母、汉字、数字和短划线（-）。|
|Tags|List|否|否|标签。|最多可以设置20个标签。更多信息，请参见[Tags属性](/cn.zh-CN/资源类型/CS/ALIYUN::CS::ManagedKubernetesCluster.md)。 |
|Addons|List|否|否|集群安装的组件列表。|取值：-   网络组件

支持Flannel和Terway两种网络类型，创建集群时需二选一：

    -   Flannel网络：`[{"Name":"flannel","Config":""}]`。
    -   Terway网络：`[{"Name": "terway-eniip","Config": ""}]`。
-   存储组件

支持csi和flexvolume两种类型：

    -   csi：`[{"Name":"csi-plugin","Config": ""},{"Name": "csi-provisioner","Config": ""}]`。
    -   flexvolume：`[{"Name": "flexvolume","Config": ""}]`。
-   日志组件（可选）

**说明：** 如果不开启日志服务，将无法使用集群审计功能。

    -   使用已有SLS Project：`[{"Name": "logtail-ds","Config": "{\"IngressDashboardEnabled\":\"true\",\"sls_project_name\":\"your_sls_project_name\"}"}]`。
    -   创建新的SLS Project：`[{"Name": "logtail-ds","Config": "{\"IngressDashboardEnabled\":\"true\"}"}]`。
-   Ingress组件（可选）

ACK专有版集群默认安装Ingress组件nginx-ingress-controller。

    -   安装Ingress并且开启公网：`[{"Name":"nginx-ingress-controller","Config":"{\"IngressSlbNetworkType\":\"internet\"}"}]`。
    -   不安装Ingress：`[{"Name": "nginx-ingress-controller","Config": "","Disabled": true}]`。
-   事件中心（可选，默认开启）

事件中心提供对Kubernetes事件的存储、查询、告警等能力。Kubernetes事件中心关联的Logstore在90天内免费。更多信息，请参见[创建并使用Kubernetes事件中心](/cn.zh-CN/应用中心（App）/K8S事件中心/创建并使用Kubernetes事件中心.md)。

开启事件中心：`[{"Name":"ack-node-problem-detector","Config":"{\"sls_project_name\":\"your_sls_project_name\"}"}]`。


更多信息，请参见[Addons属性](#section_0xt_i2a_ga9)。|
|ProxyMode|String|否|否|kube-proxy代理模式。|取值：-   iptables（默认值）
-   ipvs |
|DisableRollback|Boolean|否|否|失败时是否回滚。|取值：-   true（默认值）：失败时不回滚。
-   false：失败时回滚。如果选择失败时回滚，则会释放创建过程中所生产的资源，因此不推荐使用false。 |
|SnatEntry|Boolean|否|否|是否为网络配置SNAT。|如果使用自动创建的专有网络则必须设置为true。如果使用已有专有网络则根据是否具备出网能力来设置。 |
|VSwitchIds|List|否|否|交换机ID列表。|取值范围：1~3。VpcId和VSwitchIds只能同时为空或者同时都设置对应的值。 |
|LoginPassword|String|否|否|登录密码。|长度为8~30个字符。必须同时包含大写英文字母、小写英文字母，数字和特殊符号中至少三项，支持的特殊字符为：`( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? /`。LoginPassword和KeyPair二者只能指定一个参数。 |
|KeyPair|String|否|否|密钥对名称。|LoginPassword和KeyPair二者只能指定一个参数。|
|EndpointPublicAccess|Boolean|否|否|是否开启公网API Server。|取值： -   true（默认值）：开启公网API Server。
-   false：仅开启私网API Server。 |
|WorkerSystemDiskSize|Number|否|否|Worker节点系统盘大小。|默认值：120。单位：GiB。 |
|WorkerSystemDiskCategory|String|否|否|Worker节点系统盘类型。|默认值：cloud\_efficiency。|
|WorkerDataDisk|Boolean|否|否|Worker节点是否挂载数据盘。|取值：-   true
-   false（默认值） |
|WorkerDataDiskSize|Integer|否|否|Worker节点数据盘大小。|无|
|WorkerDataDiskCategory|String|否|否|数据盘类型。|无|
|TimeoutMins|Number|否|否|集群资源栈创建超时时间。|默认值：60。单位：分钟。 |
|ClusterSpec|String|否|否|托管版集群类型。|取值：-   ack.pro.small：专业托管集群，即：ACK@Edge Pro版集群。
-   ack.standard（默认值）：标准托管集群，即ACK@Edge标准版集群。 |
|ContainerCidr|String|否|否|容器网段。|不能和专有网段冲突。当选择系统自动创建专有网络时，默认使用172.16.0.0/16网段。|
|CloudMonitorFlags|Boolean|否|否|是否安装云监控插件。|取值：-   true
-   false（默认值） |
|WorkerInstanceTypes|List|否|否|Worker节点实例规格。|无|

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~64个字符，不能以`aliyun`、`acs:`、`https://`或`http://`开头。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`、`acs:`、`https://`或`http://`开头。|

## Addons语法

```
"Addons": [
  {
    "Disabled": Boolean,
    "Config": String,
    "Name": String
  }
]
```

## Addons属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Disabled|Boolean|否|否|是否禁止默认安装组件。|取值：-   true：禁止默认安装组件。
-   false：允许默认安装组件。 |
|Config|String|否|否|组件的配置。|取值为空时表示无需配置。|
|Name|String|是|否|组件的名称。|无|

## 返回值

Fn::GetAtt

-   ClusterId：集群ID。
-   TaskId：任务ID。系统自动分配，用于查询任务状态。
-   WorkerRamRoleName：Worker节点RAM角色名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EndpointPublicAccess": {
      "Type": "Boolean",
      "Description": "Whether to enable the public network API Server:\ntrue: which means that the public network API Server is open.\nfalse: If set to false, the API server on the public network will not be created, only the API server on the private network will be created.Default to true.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "ContainerCidr": {
      "Type": "String",
      "Description": "The container network segment cannot conflict with the VPC network segment. When the system is selected to automatically create a VPC, the network segment 172.16.0.0/16 is used by default.",
      "Default": "172.16.0.0/16"
    },
    "KeyPair": {
      "Type": "String",
      "Description": "Key pair name. Specify one of KeyPair or LoginPassword."
    },
    "VSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "The virtual switch ID of the worker node.",
      "MinLength": 1,
      "MaxLength": 5
    },
    "TimeoutMins": {
      "Type": "Number",
      "Description": "Cluster resource stack creation timeout, in minutes. The default value is 60.",
      "Default": 60
    },
    "Addons": {
      "Type": "Json",
      "Description": "The add-ons to be installed for the cluster."
    },
    "ClusterSpec": {
      "Type": "String",
      "Description": "The edge managed cluster spec. Value:\nack.pro.small: Professional hosting cluster, namely: \"ACK Pro version cluster\".\nack.standard: Standard hosting cluster.\nDefault value: ack.standard. The value can be empty. When it is empty, a standard managed cluster will be created."
    },
    "WorkerSystemDiskCategory": {
      "Type": "String",
      "Description": "Worker node system disk type. \nDefault to cloud_efficiency.",
      "Default": "cloud_efficiency"
    },
    "WorkerSystemDiskSize": {
      "Type": "Number",
      "Description": "Worker disk system disk size, the unit is GiB.\nDefault to 120.",
      "MinValue": 1,
      "Default": 120
    },
    "Profile": {
      "Type": "String",
      "Description": "Edge cluster ID. The default value is Edge.",
      "Default": "Edge"
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the cluster. The cluster name can use uppercase and lowercase letters, Chinese characters, numbers, and dashes."
    },
    "WorkerDataDisk": {
      "Type": "Boolean",
      "Description": "Whether to mount the data disk. The options are as follows:\ntrue: indicates that the worker node mounts data disks.\nfalse: indicates that the worker node does not mount data disks.\nDefault to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "VpcId": {
      "Type": "String",
      "Description": "VPC ID. If not set, the system will automatically create a VPC, and the VPC network segment created by the system is 192.168.0.0/16. \nVpcId and VSwitchId can only be empty at the same time or set the corresponding values at the same time."
    },
    "WorkerDataDiskSize": {
      "Type": "Number",
      "Description": "Data disk size in GiB.",
      "MinValue": 1
    },
    "CloudMonitorFlags": {
      "Type": "Boolean",
      "Description": "Whether to install the cloud monitoring plugin:\ntrue: indicates installation\nfalse: Do not install\nDefault to false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "NumOfNodes": {
      "Type": "Number",
      "Description": "Number of worker nodes. The range is [0,300]",
      "MinValue": 0,
      "MaxValue": 300
    },
    "ServiceCidr": {
      "Type": "String",
      "Description": "The service network segment cannot conflict with the VPC network segment and the container network segment. When the system is selected to automatically create a VPC, the network segment 172.19.0.0/20 is used by default.",
      "Default": "172.19.0.0/20"
    },
    "WorkerDataDiskCategory": {
      "Type": "String",
      "Description": "Data disk type."
    },
    "SnatEntry": {
      "Type": "Boolean",
      "Description": "Whether to configure SNAT for the network.\nWhen a VPC can access the public network environment, set it to false.\nWhen an existing VPC cannot access the public network environment:\nWhen set to True, SNAT is configured and the public network environment can be accessed at this time.\nIf set to false, it means that SNAT is not configured and the public network environment cannot be accessed at this time.\nDefault to true.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "ProxyMode": {
      "Type": "String",
      "Description": "kube-proxy proxy mode, supports both iptables and ipvs modes. The default is iptables.",
      "Default": "iptables"
    },
    "DisableRollback": {
      "Type": "Boolean",
      "Description": "Whether the failure was rolled back:\ntrue: indicates that it fails to roll back\nfalse: rollback failed\nThe default is true. If rollback fails, resources produced during the creation process will be released. False is not recommended.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tag the cluster."
    },
    "WorkerInstanceTypes": {
      "Type": "Json",
      "Description": "Worker node ECS specification type code. For more details, see Instance Specification Family.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "LoginPassword": {
      "Type": "String",
      "Description": "SSH login password. Password rules are 8-30 characters and contain three items (upper and lower case letters, numbers, and special symbols). Specify one of KeyPair or LoginPassword."
    }
  },
  "Resources": {
    "ManagedEdgeKubernetesCluster": {
      "Type": "ALIYUN::CS::ManagedEdgeKubernetesCluster",
      "Properties": {
        "EndpointPublicAccess": {
          "Ref": "EndpointPublicAccess"
        },
        "ContainerCidr": {
          "Ref": "ContainerCidr"
        },
        "KeyPair": {
          "Ref": "KeyPair"
        },
        "VSwitchIds": {
          "Ref": "VSwitchIds"
        },
        "TimeoutMins": {
          "Ref": "TimeoutMins"
        },
        "Addons": {
          "Ref": "Addons"
        },
        "ClusterSpec": {
          "Ref": "ClusterSpec"
        },
        "WorkerSystemDiskCategory": {
          "Ref": "WorkerSystemDiskCategory"
        },
        "WorkerSystemDiskSize": {
          "Ref": "WorkerSystemDiskSize"
        },
        "Profile": {
          "Ref": "Profile"
        },
        "Name": {
          "Ref": "Name"
        },
        "WorkerDataDisk": {
          "Ref": "WorkerDataDisk"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "WorkerDataDiskSize": {
          "Ref": "WorkerDataDiskSize"
        },
        "CloudMonitorFlags": {
          "Ref": "CloudMonitorFlags"
        },
        "NumOfNodes": {
          "Ref": "NumOfNodes"
        },
        "ServiceCidr": {
          "Ref": "ServiceCidr"
        },
        "WorkerDataDiskCategory": {
          "Ref": "WorkerDataDiskCategory"
        },
        "SnatEntry": {
          "Ref": "SnatEntry"
        },
        "ProxyMode": {
          "Ref": "ProxyMode"
        },
        "DisableRollback": {
          "Ref": "DisableRollback"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "WorkerInstanceTypes": {
          "Ref": "WorkerInstanceTypes"
        },
        "LoginPassword": {
          "Ref": "LoginPassword"
        }
      }
    }
  },
  "Outputs": {
    "TaskId": {
      "Description": "Task ID. Automatically assigned by the system, the user queries the task status.",
      "Value": {
        "Fn::GetAtt": [
          "ManagedEdgeKubernetesCluster",
          "TaskId"
        ]
      }
    },
    "ClusterId": {
      "Description": "Cluster instance ID.",
      "Value": {
        "Fn::GetAtt": [
          "ManagedEdgeKubernetesCluster",
          "ClusterId"
        ]
      }
    },
    "WorkerRamRoleName": {
      "Description": "Worker ram role name.",
      "Value": {
        "Fn::GetAtt": [
          "ManagedEdgeKubernetesCluster",
          "WorkerRamRoleName"
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
  EndpointPublicAccess:
    Type: Boolean
    Description: >-
      Whether to enable the public network API Server:

      true: which means that the public network API Server is open.

      false: If set to false, the API server on the public network will not be
      created, only the API server on the private network will be
      created.Default to true.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  ContainerCidr:
    Type: String
    Description: >-
      The container network segment cannot conflict with the VPC network
      segment. When the system is selected to automatically create a VPC, the
      network segment 172.16.0.0/16 is used by default.
    Default: 172.16.0.0/16
  KeyPair:
    Type: String
    Description: Key pair name. Specify one of KeyPair or LoginPassword.
  VSwitchIds:
    Type: CommaDelimitedList
    Description: The virtual switch ID of the worker node.
    MinLength: 1
    MaxLength: 5
  TimeoutMins:
    Type: Number
    Description: >-
      Cluster resource stack creation timeout, in minutes. The default value is
      60.
    Default: 60
  Addons:
    Type: Json
    Description: The add-ons to be installed for the cluster.
  ClusterSpec:
    Type: String
    Description: >-
      The edge managed cluster spec. Value:

      ack.pro.small: Professional hosting cluster, namely: "ACK Pro version
      cluster".

      ack.standard: Standard hosting cluster.

      Default value: ack.standard. The value can be empty. When it is empty, a
      standard managed cluster will be created.
  WorkerSystemDiskCategory:
    Type: String
    Description: |-
      Worker node system disk type. 
      Default to cloud_efficiency.
    Default: cloud_efficiency
  WorkerSystemDiskSize:
    Type: Number
    Description: |-
      Worker disk system disk size, the unit is GiB.
      Default to 120.
    MinValue: 1
    Default: 120
  Profile:
    Type: String
    Description: Edge cluster ID. The default value is Edge.
    Default: Edge
  Name:
    Type: String
    Description: >-
      The name of the cluster. The cluster name can use uppercase and lowercase
      letters, Chinese characters, numbers, and dashes.
  WorkerDataDisk:
    Type: Boolean
    Description: |-
      Whether to mount the data disk. The options are as follows:
      true: indicates that the worker node mounts data disks.
      false: indicates that the worker node does not mount data disks.
      Default to false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  VpcId:
    Type: String
    Description: >-
      VPC ID. If not set, the system will automatically create a VPC, and the
      VPC network segment created by the system is 192.168.0.0/16. 

      VpcId and VSwitchId can only be empty at the same time or set the
      corresponding values at the same time.
  WorkerDataDiskSize:
    Type: Number
    Description: Data disk size in GiB.
    MinValue: 1
  CloudMonitorFlags:
    Type: Boolean
    Description: |-
      Whether to install the cloud monitoring plugin:
      true: indicates installation
      false: Do not install
      Default to false
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  NumOfNodes:
    Type: Number
    Description: 'Number of worker nodes. The range is [0,300]'
    MinValue: 0
    MaxValue: 300
  ServiceCidr:
    Type: String
    Description: >-
      The service network segment cannot conflict with the VPC network segment
      and the container network segment. When the system is selected to
      automatically create a VPC, the network segment 172.19.0.0/20 is used by
      default.
    Default: 172.19.0.0/20
  WorkerDataDiskCategory:
    Type: String
    Description: Data disk type.
  SnatEntry:
    Type: Boolean
    Description: >-
      Whether to configure SNAT for the network.

      When a VPC can access the public network environment, set it to false.

      When an existing VPC cannot access the public network environment:

      When set to True, SNAT is configured and the public network environment
      can be accessed at this time.

      If set to false, it means that SNAT is not configured and the public
      network environment cannot be accessed at this time.

      Default to true.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  ProxyMode:
    Type: String
    Description: >-
      kube-proxy proxy mode, supports both iptables and ipvs modes. The default
      is iptables.
    Default: iptables
  DisableRollback:
    Type: Boolean
    Description: >-
      Whether the failure was rolled back:

      true: indicates that it fails to roll back

      false: rollback failed

      The default is true. If rollback fails, resources produced during the
      creation process will be released. False is not recommended.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  Tags:
    Type: Json
    Description: Tag the cluster.
  WorkerInstanceTypes:
    Type: Json
    Description: >-
      Worker node ECS specification type code. For more details, see Instance
      Specification Family.
    MinLength: 1
    MaxLength: 10
  LoginPassword:
    Type: String
    Description: >-
      SSH login password. Password rules are 8-30 characters and contain three
      items (upper and lower case letters, numbers, and special symbols).
      Specify one of KeyPair or LoginPassword.
Resources:
  ManagedEdgeKubernetesCluster:
    Type: 'ALIYUN::CS::ManagedEdgeKubernetesCluster'
    Properties:
      EndpointPublicAccess:
        Ref: EndpointPublicAccess
      ContainerCidr:
        Ref: ContainerCidr
      KeyPair:
        Ref: KeyPair
      VSwitchIds:
        Ref: VSwitchIds
      TimeoutMins:
        Ref: TimeoutMins
      Addons:
        Ref: Addons
      ClusterSpec:
        Ref: ClusterSpec
      WorkerSystemDiskCategory:
        Ref: WorkerSystemDiskCategory
      WorkerSystemDiskSize:
        Ref: WorkerSystemDiskSize
      Profile:
        Ref: Profile
      Name:
        Ref: Name
      WorkerDataDisk:
        Ref: WorkerDataDisk
      VpcId:
        Ref: VpcId
      WorkerDataDiskSize:
        Ref: WorkerDataDiskSize
      CloudMonitorFlags:
        Ref: CloudMonitorFlags
      NumOfNodes:
        Ref: NumOfNodes
      ServiceCidr:
        Ref: ServiceCidr
      WorkerDataDiskCategory:
        Ref: WorkerDataDiskCategory
      SnatEntry:
        Ref: SnatEntry
      ProxyMode:
        Ref: ProxyMode
      DisableRollback:
        Ref: DisableRollback
      Tags:
        Ref: Tags
      WorkerInstanceTypes:
        Ref: WorkerInstanceTypes
      LoginPassword:
        Ref: LoginPassword
Outputs:
  TaskId:
    Description: >-
      Task ID. Automatically assigned by the system, the user queries the task
      status.
    Value:
      'Fn::GetAtt':
        - ManagedEdgeKubernetesCluster
        - TaskId
  ClusterId:
    Description: Cluster instance ID.
    Value:
      'Fn::GetAtt':
        - ManagedEdgeKubernetesCluster
        - ClusterId
  WorkerRamRoleName:
    Description: Worker ram role name.
    Value:
      'Fn::GetAtt':
        - ManagedEdgeKubernetesCluster
        - WorkerRamRoleName
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CS/JSON/ManagedEdgeKubernetesCluster.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CS/YAML/ManagedEdgeKubernetesCluster.yml)。


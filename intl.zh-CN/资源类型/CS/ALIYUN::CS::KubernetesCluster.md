# ALIYUN::CS::KubernetesCluster

ALIYUN::CS::KubernetesCluster类型用于创建Kubernetes专有版集群。

## 语法

```
{
  "Type": "ALIYUN::CS::KubernetesCluster",
  "Properties": {
    "MasterAutoRenew": Boolean,
    "CloudMonitorFlags": Boolean,
    "ProxyMode": String,
    "MasterInstanceTypes": List,
    "WorkerInstanceChargeType": String,
    "SnatEntry": Boolean,
    "WorkerPeriod": Number,
    "WorkerPeriodUnit": String,
    "WorkerSystemDiskCategory": String,
    "WorkerVSwitchIds": List,
    "MasterInstanceChargeType": String,
    "VpcId": String,
    "Tags": List,
    "MasterAutoRenewPeriod": Number,
    "CpuPolicy": String,
    "WorkerInstanceTypes": List,
    "WorkerDataDisks": List,
    "LoginPassword": String,
    "ContainerCidr": String,
    "NumOfNodes": Number,
    "Name": String,
    "WorkerSystemDiskSize": Number,
    "NodePortRange": String,
    "SshFlags": Boolean,
    "Taint": List,
    "MasterDataDisk": Boolean,
    "MasterSystemDiskCategory": String,
    "WorkerAutoRenewPeriod": Number,
    "WorkerDataDisk": Boolean,
    "WorkerAutoRenew": Boolean,
    "Addons": List,
    "DisableRollback": Boolean,
    "ServiceCidr": String,
    "KubernetesVersion": String,
    "MasterPeriod": Number,
    "SecurityGroupId": String,
    "KeyPair": String,
    "MasterVSwitchIds": List,
    "EndpointPublicAccess": Boolean,
    "MasterSystemDiskSize": Number,
    "MasterDataDisks": List,
    "MasterCount": Number,
    "TimeoutMins": Number,
    "MasterPeriodUnit": String,
    "PodVswitchIds": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MasterAutoRenew|Boolean|否|否|Master节点是否自动续费。|当MasterInstanceChargeType为PrePaid时，该参数生效。 取值：

-   true（默认值）
-   false |
|CloudMonitorFlags|Boolean|否|否|是否安装云监控插件。|取值： -   true
-   false（默认值） |
|ProxyMode|String|否|否|kube-proxy代理模式。|取值： -   iptables（默认值）
-   ipvs |
|MasterInstanceTypes|List|是|否|Master节点ECS实例规格。|必须填写3个ECS实例规格，ECS实例规格可以重复。更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。 |
|WorkerInstanceChargeType|String|否|否|Worker节点付费类型。|取值： -   PrePaid：包年包月。
-   PostPaid（默认值）：按量付费。 |
|SnatEntry|Boolean|否|否|是否为网络配置SNAT。|取值：-   当已有专有网络可以访问公网环境时：false。
-   当已有专有网络不能访问公网环境时：
    -   true：配置SNAT，此时可以访问公网环境。
    -   false：不配置SNAT，此时不能访问公网环境。 |
|WorkerPeriod|Number|否|否|包年包月时长。|当WorkerInstanceChargeType取值为PrePaid时该参数生效且为必选参数。取值：

-   当WorkerPeriodUnit取值为Week时：1、2、3、4。
-   当WorkerPeriodUnit取值为Month时： 1、2、3、4、5、6、7、8、9、12、24、36、48、60。 |
|WorkerPeriodUnit|String|否|否|包年包月周期类型。|当WorkerInstanceChargeType取值为PrePaid时，需要指定周期类型。取值： -   Week
-   Month（默认值） |
|WorkerSystemDiskCategory|String|否|否|Worker节点系统盘类型。|取值： -   cloud\_efficiency（默认值）：高效云盘。
-   cloud\_ssd：SSD云盘。 |
|WorkerVSwitchIds|List|是|否|Worker节点的交换机ID。|最多支持设置5个VSwitchId。|
|MasterInstanceChargeType|String|否|否|Master节点付费类型。|取值： -   PrePaid：包年包月。
-   PostPaid（默认值）：按量付费。 |
|VpcId|String|是|否|专有网络ID。|如果不设置，系统会自动创建专有网络，系统创建的专有网络网段为192.168.0.0/16。 VpcId和MasterVSwitchIds只能同时为空或者同时指定。 |
|Tags|List|否|否|集群标签。|最多可以设置20组标签。更多信息，请参见[Tags属性](#section_sao_4g8_748)。 |
|MasterAutoRenewPeriod|Number|否|否|Master节点自动续费周期。|当选择预付费和自动续费时该参数生效，且为必选值。取值： -   当MasterPeriodUnit取值为Week时：1、2、3。
-   当MasterPeriodUnit取值为Month时：1、2、3、6、12。

默认值：1。 |
|PodVswitchIds|List|否|否|Pod交换机列表。|您需要为每一个节点交换机指定至少一个相同可用区的Pod交换机，该Pod交换机不能跟节点交换机重复。建议您选择网段掩码不大于19的交换机。

**说明：** 当集群列表（Addons）取值为网络组件，且采用Terway网络类型时，必须为集群指定PodVswitchIds。 |
|CpuPolicy|String|否|否|CPU策略。|当集群版本为1.12.6及以上版本时，取值：-   static
-   none（默认值） |
|WorkerInstanceTypes|List|是|否|Worker节点ECS实例规格。|更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。|
|WorkerDataDisks|List|否|否|Worker数据盘类型、大小等配置。|只有在挂载Worker节点数据盘时有效。更多信息，请参见[WorkerDataDisks属性](#section_cka_mac_ug7)。 |
|LoginPassword|String|否|否|SSH登录密码。|长度为8~30个字符，必须同时包含大写英文字母、小写英文字母、数字和特殊字符其中三项。 该参数和KeyPair二选一。 |
|ContainerCidr|String|否|否|容器网段。|会与专有网络网段冲突。当选择系统自动创建专有网络时，默认使用172.16.0.0/16网段。|
|NumOfNodes|Number|否|否|Worker节点数。|取值范围：0~300。 默认值：3。 |
|Name|String|是|否|集群名称。|长度为1~63个字符。可包含写英文字母、汉字、数字和短划线（-）。|
|WorkerSystemDiskSize|Number|否|否|Worker节点系统盘大小。|默认值：120。 单位：GiB。 |
|NodePortRange|String|否|否|节点服务端口。|取值范围：30,000~65,535中的两个值，以短划线（-）分隔。 默认值：30,000-65,535。 |
|SshFlags|Boolean|否|否|是否开放公网SSH登录。|取值： -   true
-   false |
|Taint|List|否|否|给节点做污点标记，通常用于Pods的调度策略。|若Pods上有相对应的容忍（tolerance）标记，则可以将容忍节点上的污点调度到该节点。|
|MasterDataDisk|Boolean|否|否|Master节点是否挂载数据盘。|取值： -   true
-   false（默认值） |
|MasterSystemDiskCategory|String|否|否|Master节点系统盘类型。|取值： -   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。 |
|WorkerAutoRenewPeriod|Number|否|否|自动续费周期。|当选择预付费和自动续费时该参数生效且为必选参数。取值： -   当WorkerPeriodUnit取值为Week时：1、2、3。
-   当WorkerPeriodUnit取值为Month时：1、2、3、6、12。 |
|WorkerDataDisk|Boolean|否|否|Worker节点是否挂载数据盘。|取值： -   true
-   false（默认值） |
|WorkerAutoRenew|Boolean|否|否|是否开启Worker节点自动续费。|取值： -   true（默认值）
-   false |
|Addons|List|否|否|Kubernetes集群安装的组件列表。|取值：-   网络组件

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

事件中心提供对Kubernetes事件的存储、查询、告警等能力。Kubernetes事件中心关联的Logstore在90天内免费。更多信息，请参见[创建并使用Kubernetes事件中心](/intl.zh-CN/应用中心（App）/K8S事件中心/创建并使用Kubernetes事件中心.md)。

开启事件中心：`[{"Name":"ack-node-problem-detector","Config":"{\"sls_project_name\":\"your_sls_project_name\"}"}]`。


更多信息，请参见[Addons属性](#section_3nl_fca_4be)。|
|DisableRollback|Boolean|否|否|失败是否回滚。|取值： -   true（默认值）：失败不回滚。
-   false：失败回滚。

**说明：** 如果选择失败回滚，则会释放创建过程中所生产的资源，不推荐使用。 |
|ServiceCidr|String|否|否|服务网段。|不能和专有网络网段以及容器网段冲突。 当选择系统自动创建专有网络时，默认使用172.19.0.0/20网段。 |
|KubernetesVersion|String|否|否|集群版本，与Kubernetes社区基线版本保持一致。建议选择最新版本。|目前您可以创建两种最新版本的集群。关于ACK支持的Kubernetes版本，请参见[Kubernetes版本发布概览](/intl.zh-CN/产品发布记录/Kubernetes版本发布说明/Kubernetes版本发布概览.md)。|
|MasterPeriod|Number|否|否|包年包月时长。|当MasterInstanceChargeType取值为PrePaid时该参数生效且为必选参数。 取值：

-   当MasterPeriodUnit取值为Week时：1，2，3，4。
-   当MasterPeriodUnit取值为Month时：1，2，3，4，5，6，7，8，9，12，24，36，48，60。

 默认值：1。|
|SecurityGroupId|String|否|否|集群ECS实例所属于的安全组ID。|无|
|KeyPair|String|否|否|密钥对名称。|和LoginPassword二选一。|
|MasterVSwitchIds|List|是|否|Master节点交换机ID。|必须指定3个交换机ID，交换机ID可以重复。为确保集群的高可用性，推荐您选择3个交换机。|
|EndpointPublicAccess|Boolean|否|否|是否开启公网APIServer。|取值： -   true：开启公网APIServer。
-   false（默认值）：仅创建私网APIServer。 |
|MasterSystemDiskSize|Number|否|否|Master节点系统盘大小。|默认值：120。 单位：GiB。 |
|MasterDataDisks|List|否|否|Master数据盘类型、大小等配置。|只有在挂载Master节点数据盘时有效。更多信息，请参见[MasterDataDisks属性](#section_sqy_mx3_wf0)。 |
|MasterCount|Number|否|否|Master实例个数。|取值： -   3（默认值）
-   5 |
|TimeoutMins|Number|否|否|集群资源栈创建超时时间。|默认值：60。 单位：分钟。 |
|MasterPeriodUnit|String|否|否|Master节点付费周期。|当MasterInstanceChargeType指定为PrePaid时，需要指定周期。 取值：

-   Week
-   Month（默认值） |

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

## MasterDataDisks语法

```
"MasterDataDisks": [
  {
    "Category": String,
    "Size": Number
  }
]
```

## MasterDataDisks属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Category|String|是|否|Master节点数据盘类型。|取值： -   cloud：普通云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_efficiency：高效云盘。 |
|Size|Number|是|否|Master节点数据盘大小。|取值范围：40~32,768。 单位：GiB。 |

## WorkerDataDisks语法

```
"WorkerDataDisks": [
  {
    "Category": String,
    "Size": Number
  }
]
```

## WorkerDataDisks属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Category|String|是|否|Worker节点数据盘类型。|取值： -   cloud：普通云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_efficiency：高效云盘。 |
|Size|Number|是|否|数据盘大小。|取值范围：40~32,768。 单位：GiB。 |

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
|Disabled|Boolean|否|否|是否禁止默认安装。|取值：-   true：禁止默认安装。
-   false：允许默认安装。 |
|Config|String|否|否|插件的配置。|取值为空时表示无需配置。|
|Name|String|是|否|插件的名称。|无|

## 返回值

Fn::GetAtt

-   ClusterId：集群ID。
-   TaskId：任务ID。系统自动分配，用户查询任务状态。
-   WorkerRamRoleName：Worker节点RAM角色名称。

## 示例

JSON示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EndpointPublicAccess": {
      "Type": "Boolean",
      "Description": "Whether to enable the public network API Server:\ntrue: which means that the public network API Server is open.\nfalse: If set to false, the API server on the public network will not be created, only the API server on the private network will be created.Default to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "WorkerPeriod": {
      "Type": "Number",
      "Description": "The duration of the annual and monthly subscription. It takes effect when the worker_instance_charge_type value is PrePaid and is required. The value range is:\nWhen PeriodUnit = Week, Period values are: {\"1\", \"2\", \"3\", \"4\"}\nWhen PeriodUnit = Month, Period values are: {\"1\", \"2\", \"3\", \"4\", \"5\", \"6\", \"7\", \"8\", \"9\", \"12\", \"24\", \"36\", \"48\", \"60\"}\nDefault to 1.",
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
    "WorkerPeriodUnit": {
      "Type": "String",
      "Description": "When you specify PrePaid, you need to specify the period. The options are:\nWeek: Time is measured in weeks\nMonth: time in months\nDefault to Month.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    },
    "MasterSystemDiskCategory": {
      "Type": "String",
      "Description": "Master disk system disk type. The value includes:\ncloud_efficiency: efficient cloud disk\ncloud_ssd: SSD cloud disk\ncloud_essd: ESSD cloud diskDefault to cloud_ssd.",
      "Default": "cloud_ssd"
    },
    "Addons": {
      "Type": "Json",
      "Description": "A combination of addon plugins for Kubernetes clusters.\nNetwork plug-in: including Flannel and Terway network plug-ins\nLog service: Optional. If the log service is not enabled, the cluster audit function cannot be used.\nIngress: The installation of the Ingress component is enabled by default."
    },
    "MasterSystemDiskSize": {
      "Type": "Number",
      "Description": "Master disk system disk size in GiB.\nDefault to 120.",
      "MinValue": 1,
      "Default": 120
    },
    "WorkerSystemDiskCategory": {
      "Type": "String",
      "Description": "Worker node system disk type. The value includes:\ncloud_efficiency: efficient cloud disk\ncloud_ssd: SSD cloud disk\nDefault to cloud_efficiency.",
      "Default": "cloud_efficiency"
    },
    "WorkerSystemDiskSize": {
      "Type": "Number",
      "Description": "Worker disk system disk size, the unit is GiB.\nDefault to 120.",
      "MinValue": 1,
      "Default": 120
    },
    "NodePortRange": {
      "Type": "String",
      "Description": "Node service port. The value range is [30000, 65535].\nDefault to 30000-65535.",
      "Default": "30000-65535"
    },
    "MasterCount": {
      "Type": "Number",
      "Description": "Number of master instances. The value can be 3 or 5. The default value is 3.",
      "AllowedValues": [
        3,
        5
      ],
      "Default": 3
    },
    "SshFlags": {
      "Type": "Boolean",
      "Description": "Whether to enable public network SSH login:\ntrue: open\nfalse: not open",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "MasterVSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "Master node switch ID. To ensure high availability of the cluster, it is recommended that you select 3 switches and distribute them in different Availability Zones.",
      "MinLength": 1,
      "MaxLength": 3
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the cluster. The cluster name can use uppercase and lowercase letters, Chinese characters, numbers, and dashes."
    },
    "Taint": {
      "Type": "Json",
      "Description": "It is used to mark nodes with taints. It is usually used for the scheduling strategy of Pods. The corresponding concept is: tolerance. If there is a corresponding tolerance mark on the Pods, the stain on the node can be tolerated and scheduled to the node."
    },
    "MasterDataDisks": {
      "Type": "Json",
      "Description": "Master data disk type, size and other configuration combinations. This parameter is valid only when the master node data disk is mounted."
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
    "ServiceCidr": {
      "Type": "String",
      "Description": "The service network segment cannot conflict with the VPC network segment and the container network segment. When the system is selected to automatically create a VPC, the network segment 172.19.0.0/20 is used by default.",
      "Default": "172.19.0.0/20"
    },
    "PodVswitchIds": {
      "Type": "Json",
      "Description": "The list of pod vSwitches. For each vSwitch that is allocated to nodes, \n you must specify at least one pod vSwitch in the same zone. \n The pod vSwitches cannot be the same as the node vSwitches. \n We recommend that you set the mask length of the CIDR block to a value no \ngreater than 19 for the pod vSwitches.\nThe pod_vswitch_ids parameter is required when the Terway network \nplug-in is selected for the cluster."
    },
    "WorkerAutoRenew": {
      "Type": "Boolean",
      "Description": "Whether to enable automatic renewal of Worker nodes. The optional values are:\ntrue: automatic renewal\nfalse: do not renew automatically\nDefault to true.",
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
    "Tags": {
      "Type": "Json",
      "Description": "Tag the cluster."
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
    "WorkerInstanceTypes": {
      "Type": "Json",
      "Description": "Worker node ECS specification type code. For more details, see Instance Specification Family.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "LoginPassword": {
      "Type": "String",
      "Description": "SSH login password. Password rules are 8-30 characters and contain three items (upper and lower case letters, numbers, and special symbols). Specify one of KeyPair or LoginPassword."
    },
    "MasterPeriod": {
      "Type": "Number",
      "Description": "The duration of the annual subscription and monthly subscription. It takes effect when the master_instance_charge_type value is PrePaid and is a required value. The value range is:\nWhen PeriodUnit = Week, Period values are: {\"1\", \"2\", \"3\", \"4\"}\nWhen PeriodUnit = Month, Period values are: {\"1\", \"2\", \"3\", \"4\", \"5\", \"6\", \"7\", \"8\", \"9\", \"12\", \"24\", \"36\", \"48\", \"60\"}\nDefault to 1.",
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
    "KubernetesVersion": {
      "Type": "String",
      "Description": "The version of the Kubernetes cluster."
    },
    "MasterInstanceChargeType": {
      "Type": "String",
      "Description": "Master node payment type. The optional values are:\nPrePaid: prepaid\nPostPaid: Pay as you go\nDefault to PostPaid.",
      "AllowedValues": [
        "Subscription",
        "PrePaid",
        "PrePay",
        "Prepaid",
        "PayAsYouGo",
        "PostPaid",
        "PayOnDemand",
        "Postpaid"
      ],
      "Default": "PostPaid"
    },
    "ContainerCidr": {
      "Type": "String",
      "Description": "The container network segment cannot conflict with the VPC network segment. When the sytem is selected to automatically create a VPC, the network segment 172.16.0.0/16 is used by default.",
      "Default": "172.16.0.0/16"
    },
    "CpuPolicy": {
      "Type": "String",
      "Description": "CPU policy. The cluster version is 1.12.6 and above supports both static and none strategies."
    },
    "WorkerInstanceChargeType": {
      "Type": "String",
      "Description": "Worker node payment type. The optional values are:\nPrePaid: prepaid\nPostPaid: Pay as you go\nDefault to PostPaid.",
      "AllowedValues": [
        "Subscription",
        "PrePaid",
        "PrePay",
        "Prepaid",
        "PayAsYouGo",
        "PostPaid",
        "PayOnDemand",
        "Postpaid"
      ],
      "Default": "PostPaid"
    },
    "KeyPair": {
      "Type": "String",
      "Description": "Key pair name. Specify one of KeyPair or LoginPassword."
    },
    "MasterInstanceTypes": {
      "Type": "CommaDelimitedList",
      "Description": "Master node ECS specification type code. For more details, see Instance Type Family. Each item correspond to MasterVSwitchIds.\nList size must be 3, Instance Type can be repeated.",
      "MinLength": 3,
      "MaxLength": 3
    },
    "WorkerDataDisks": {
      "Type": "Json",
      "Description": "A combination of configurations such as worker data disk type and size. This parameter is valid only when the worker node data disk is mounted."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Specifies the ID of the security group to which the cluster ECS instance belongs."
    },
    "TimeoutMins": {
      "Type": "Number",
      "Description": "Cluster resource stack creation timeout, in minutes. The default value is 60.",
      "Default": 60
    },
    "MasterPeriodUnit": {
      "Type": "String",
      "Description": "When you specify PrePaid, you need to specify the period. The options are:\nWeek: Time is measured in weeks\nMonth: time in months\nDefault to Month",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    },
    "MasterAutoRenewPeriod": {
      "Type": "Number",
      "Description": "Automatic renewal cycle, which takes effect when prepaid and automatic renewal are selected, and is required:\nWhen PeriodUnit = Week, the values are: {\"1\", \"2\", \"3\"}\nWhen PeriodUnit = Month, the value is {\"1\", \"2\", \"3\", \"6\", \"12\"}\nDefault to 1.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
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
      "Description": "VPC ID."
    },
    "NumOfNodes": {
      "Type": "Number",
      "Description": "Number of worker nodes. The range is [0,300].\nDefault to 3.",
      "MinValue": 0,
      "MaxValue": 300,
      "Default": 3
    },
    "MasterAutoRenew": {
      "Type": "Boolean",
      "Description": "Whether the master node automatically renews. It takes effect when the value of MasterInstanceChargeType is PrePaid. The optional values are:\ntrue: automatic renewal\nfalse: do not renew automatically\nDefault to true.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "WorkerAutoRenewPeriod": {
      "Type": "Number",
      "Description": "Automatic renewal cycle, which takes effect when prepaid and automatic renewal are selected, and is required:\nWhen PeriodUnit = Week, the values are: {\"1\", \"2\", \"3\"}\nWhen PeriodUnit = Month, the value is {\"1\", \"2\", \"3\", \"6\", \"12\"}\nDefault to 1.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "WorkerVSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "The virtual switch ID of the worker node.",
      "MinLength": 1
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
    "MasterDataDisk": {
      "Type": "Boolean",
      "Description": "Whether the master node mounts data disks can be selected as:\ntrue: mount the data disk\nfalse: no data disk is mounted, default is false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    }
  },
  "Resources": {
    "KubernetesCluster": {
      "Type": "ALIYUN::CS::KubernetesCluster",
      "Properties": {
        "EndpointPublicAccess": {
          "Ref": "EndpointPublicAccess"
        },
        "WorkerPeriod": {
          "Ref": "WorkerPeriod"
        },
        "WorkerPeriodUnit": {
          "Ref": "WorkerPeriodUnit"
        },
        "MasterSystemDiskCategory": {
          "Ref": "MasterSystemDiskCategory"
        },
        "Addons": {
          "Ref": "Addons"
        },
        "MasterSystemDiskSize": {
          "Ref": "MasterSystemDiskSize"
        },
        "WorkerSystemDiskCategory": {
          "Ref": "WorkerSystemDiskCategory"
        },
        "WorkerSystemDiskSize": {
          "Ref": "WorkerSystemDiskSize"
        },
        "NodePortRange": {
          "Ref": "NodePortRange"
        },
        "MasterCount": {
          "Ref": "MasterCount"
        },
        "SshFlags": {
          "Ref": "SshFlags"
        },
        "MasterVSwitchIds": {
          "Ref": "MasterVSwitchIds"
        },
        "Name": {
          "Ref": "Name"
        },
        "Taint": {
          "Ref": "Taint"
        },
        "MasterDataDisks": {
          "Ref": "MasterDataDisks"
        },
        "CloudMonitorFlags": {
          "Ref": "CloudMonitorFlags"
        },
        "ServiceCidr": {
          "Ref": "ServiceCidr"
        },
        "PodVswitchIds": {
          "Ref": "PodVswitchIds"
        },
        "WorkerAutoRenew": {
          "Ref": "WorkerAutoRenew"
        },
        "ProxyMode": {
          "Ref": "ProxyMode"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "DisableRollback": {
          "Ref": "DisableRollback"
        },
        "WorkerInstanceTypes": {
          "Ref": "WorkerInstanceTypes"
        },
        "LoginPassword": {
          "Ref": "LoginPassword"
        },
        "MasterPeriod": {
          "Ref": "MasterPeriod"
        },
        "KubernetesVersion": {
          "Ref": "KubernetesVersion"
        },
        "MasterInstanceChargeType": {
          "Ref": "MasterInstanceChargeType"
        },
        "ContainerCidr": {
          "Ref": "ContainerCidr"
        },
        "CpuPolicy": {
          "Ref": "CpuPolicy"
        },
        "WorkerInstanceChargeType": {
          "Ref": "WorkerInstanceChargeType"
        },
        "KeyPair": {
          "Ref": "KeyPair"
        },
        "MasterInstanceTypes": {
          "Ref": "MasterInstanceTypes"
        },
        "WorkerDataDisks": {
          "Ref": "WorkerDataDisks"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "TimeoutMins": {
          "Ref": "TimeoutMins"
        },
        "MasterPeriodUnit": {
          "Ref": "MasterPeriodUnit"
        },
        "MasterAutoRenewPeriod": {
          "Ref": "MasterAutoRenewPeriod"
        },
        "WorkerDataDisk": {
          "Ref": "WorkerDataDisk"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "NumOfNodes": {
          "Ref": "NumOfNodes"
        },
        "MasterAutoRenew": {
          "Ref": "MasterAutoRenew"
        },
        "WorkerAutoRenewPeriod": {
          "Ref": "WorkerAutoRenewPeriod"
        },
        "WorkerVSwitchIds": {
          "Ref": "WorkerVSwitchIds"
        },
        "SnatEntry": {
          "Ref": "SnatEntry"
        },
        "MasterDataDisk": {
          "Ref": "MasterDataDisk"
        }
      }
    }
  },
  "Outputs": {
    "TaskId": {
      "Description": "Task ID. Automatically assigned by the system, the user queries the task status.",
      "Value": {
        "Fn::GetAtt": [
          "KubernetesCluster",
          "TaskId"
        ]
      }
    },
    "ClusterId": {
      "Description": "Cluster instance ID.",
      "Value": {
        "Fn::GetAtt": [
          "KubernetesCluster",
          "ClusterId"
        ]
      }
    },
    "WorkerRamRoleName": {
      "Description": "Worker ram role name.",
      "Value": {
        "Fn::GetAtt": [
          "KubernetesCluster",
          "WorkerRamRoleName"
        ]
      }
    }
  }
}
```

YAML示例

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  Addons:
    Description: 'A combination of addon plugins for Kubernetes clusters.

      Network plug-in: including Flannel and Terway network plug-ins

      Log service: Optional. If the log service is not enabled, the cluster audit
      function cannot be used.

      Ingress: The installation of the Ingress component is enabled by default.'
    Type: Json
  CloudMonitorFlags:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Whether to install the cloud monitoring plugin:

      true: indicates installation

      false: Do not install

      Default to false'
    Type: Boolean
  ContainerCidr:
    Default: 172.16.0.0/16
    Description: The container network segment cannot conflict with the VPC network
      segment. When the sytem is selected to automatically create a VPC, the network
      segment 172.16.0.0/16 is used by default.
    Type: String
  CpuPolicy:
    Description: CPU policy. The cluster version is 1.12.6 and above supports both
      static and none strategies.
    Type: String
  DisableRollback:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: true
    Description: 'Whether the failure was rolled back:

      true: indicates that it fails to roll back

      false: rollback failed

      The default is true. If rollback fails, resources produced during the creation
      process will be released. False is not recommended.'
    Type: Boolean
  EndpointPublicAccess:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Whether to enable the public network API Server:

      true: which means that the public network API Server is open.

      false: If set to false, the API server on the public network will not be created,
      only the API server on the private network will be created.Default to false.'
    Type: Boolean
  KeyPair:
    Description: Key pair name. Specify one of KeyPair or LoginPassword.
    Type: String
  KubernetesVersion:
    Description: The version of the Kubernetes cluster.
    Type: String
  LoginPassword:
    Description: SSH login password. Password rules are 8-30 characters and contain
      three items (upper and lower case letters, numbers, and special symbols). Specify
      one of KeyPair or LoginPassword.
    Type: String
  MasterAutoRenew:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: true
    Description: 'Whether the master node automatically renews. It takes effect when
      the value of MasterInstanceChargeType is PrePaid. The optional values are:

      true: automatic renewal

      false: do not renew automatically

      Default to true.'
    Type: Boolean
  MasterAutoRenewPeriod:
    AllowedValues:
    - 1
    - 2
    - 3
    - 6
    - 12
    Default: 1
    Description: 'Automatic renewal cycle, which takes effect when prepaid and automatic
      renewal are selected, and is required:

      When PeriodUnit = Week, the values are: {"1", "2", "3"}

      When PeriodUnit = Month, the value is {"1", "2", "3", "6", "12"}

      Default to 1.'
    Type: Number
  MasterCount:
    AllowedValues:
    - 3
    - 5
    Default: 3
    Description: Number of master instances. The value can be 3 or 5. The default
      value is 3.
    Type: Number
  MasterDataDisk:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Whether the master node mounts data disks can be selected as:

      true: mount the data disk

      false: no data disk is mounted, default is false'
    Type: Boolean
  MasterDataDisks:
    Description: Master data disk type, size and other configuration combinations.
      This parameter is valid only when the master node data disk is mounted.
    Type: Json
  MasterInstanceChargeType:
    AllowedValues:
    - Subscription
    - PrePaid
    - PrePay
    - Prepaid
    - PayAsYouGo
    - PostPaid
    - PayOnDemand
    - Postpaid
    Default: PostPaid
    Description: 'Master node payment type. The optional values are:

      PrePaid: prepaid

      PostPaid: Pay as you go

      Default to PostPaid.'
    Type: String
  MasterInstanceTypes:
    Description: 'Master node ECS specification type code. For more details, see Instance
      Type Family. Each item correspond to MasterVSwitchIds.

      List size must be 3, Instance Type can be repeated.'
    MaxLength: 3
    MinLength: 3
    Type: CommaDelimitedList
  MasterPeriod:
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
    Description: 'The duration of the annual subscription and monthly subscription.
      It takes effect when the master_instance_charge_type value is PrePaid and is
      a required value. The value range is:

      When PeriodUnit = Week, Period values are: {"1", "2", "3", "4"}

      When PeriodUnit = Month, Period values are: {"1", "2", "3", "4", "5", "6", "7",
      "8", "9", "12", "24", "36", "48", "60"}

      Default to 1.'
    Type: Number
  MasterPeriodUnit:
    AllowedValues:
    - Week
    - Month
    Default: Month
    Description: 'When you specify PrePaid, you need to specify the period. The options
      are:

      Week: Time is measured in weeks

      Month: time in months

      Default to Month'
    Type: String
  MasterSystemDiskCategory:
    Default: cloud_ssd
    Description: 'Master disk system disk type. The value includes:

      cloud_efficiency: efficient cloud disk

      cloud_ssd: SSD cloud disk

      cloud_essd: ESSD cloud diskDefault to cloud_ssd.'
    Type: String
  MasterSystemDiskSize:
    Default: 120
    Description: 'Master disk system disk size in GiB.

      Default to 120.'
    MinValue: 1
    Type: Number
  MasterVSwitchIds:
    Description: Master node switch ID. To ensure high availability of the cluster,
      it is recommended that you select 3 switches and distribute them in different
      Availability Zones.
    MaxLength: 3
    MinLength: 1
    Type: CommaDelimitedList
  Name:
    Description: The name of the cluster. The cluster name can use uppercase and lowercase
      letters, Chinese characters, numbers, and dashes.
    Type: String
  NodePortRange:
    Default: 30000-65535
    Description: 'Node service port. The value range is [30000, 65535].

      Default to 30000-65535.'
    Type: String
  NumOfNodes:
    Default: 3
    Description: 'Number of worker nodes. The range is [0,300].

      Default to 3.'
    MaxValue: 300
    MinValue: 0
    Type: Number
  PodVswitchIds:
    Description: "The list of pod vSwitches. For each vSwitch that is allocated to\
      \ nodes, \n you must specify at least one pod vSwitch in the same zone. \n The\
      \ pod vSwitches cannot be the same as the node vSwitches. \n We recommend that\
      \ you set the mask length of the CIDR block to a value no \ngreater than 19\
      \ for the pod vSwitches.\nThe pod_vswitch_ids parameter is required when the\
      \ Terway network \nplug-in is selected for the cluster."
    Type: Json
  ProxyMode:
    Default: iptables
    Description: kube-proxy proxy mode, supports both iptables and ipvs modes. The
      default is iptables.
    Type: String
  SecurityGroupId:
    Description: Specifies the ID of the security group to which the cluster ECS instance
      belongs.
    Type: String
  ServiceCidr:
    Default: 172.19.0.0/20
    Description: The service network segment cannot conflict with the VPC network
      segment and the container network segment. When the system is selected to automatically
      create a VPC, the network segment 172.19.0.0/20 is used by default.
    Type: String
  SnatEntry:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: true
    Description: 'Whether to configure SNAT for the network.

      When a VPC can access the public network environment, set it to false.

      When an existing VPC cannot access the public network environment:

      When set to True, SNAT is configured and the public network environment can
      be accessed at this time.

      If set to false, it means that SNAT is not configured and the public network
      environment cannot be accessed at this time.

      Default to true.'
    Type: Boolean
  SshFlags:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Whether to enable public network SSH login:

      true: open

      false: not open'
    Type: Boolean
  Tags:
    Description: Tag the cluster.
    Type: Json
  Taint:
    Description: 'It is used to mark nodes with taints. It is usually used for the
      scheduling strategy of Pods. The corresponding concept is: tolerance. If there
      is a corresponding tolerance mark on the Pods, the stain on the node can be
      tolerated and scheduled to the node.'
    Type: Json
  TimeoutMins:
    Default: 60
    Description: Cluster resource stack creation timeout, in minutes. The default
      value is 60.
    Type: Number
  VpcId:
    Description: VPC ID.
    Type: String
  WorkerAutoRenew:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: true
    Description: 'Whether to enable automatic renewal of Worker nodes. The optional
      values are:

      true: automatic renewal

      false: do not renew automatically

      Default to true.'
    Type: Boolean
  WorkerAutoRenewPeriod:
    AllowedValues:
    - 1
    - 2
    - 3
    - 6
    - 12
    Default: 1
    Description: 'Automatic renewal cycle, which takes effect when prepaid and automatic
      renewal are selected, and is required:

      When PeriodUnit = Week, the values are: {"1", "2", "3"}

      When PeriodUnit = Month, the value is {"1", "2", "3", "6", "12"}

      Default to 1.'
    Type: Number
  WorkerDataDisk:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: 'Whether to mount the data disk. The options are as follows:

      true: indicates that the worker node mounts data disks.

      false: indicates that the worker node does not mount data disks.

      Default to false.'
    Type: Boolean
  WorkerDataDisks:
    Description: A combination of configurations such as worker data disk type and
      size. This parameter is valid only when the worker node data disk is mounted.
    Type: Json
  WorkerInstanceChargeType:
    AllowedValues:
    - Subscription
    - PrePaid
    - PrePay
    - Prepaid
    - PayAsYouGo
    - PostPaid
    - PayOnDemand
    - Postpaid
    Default: PostPaid
    Description: 'Worker node payment type. The optional values are:

      PrePaid: prepaid

      PostPaid: Pay as you go

      Default to PostPaid.'
    Type: String
  WorkerInstanceTypes:
    Description: Worker node ECS specification type code. For more details, see Instance
      Specification Family.
    MaxLength: 10
    MinLength: 1
    Type: Json
  WorkerPeriod:
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
    Description: 'The duration of the annual and monthly subscription. It takes effect
      when the worker_instance_charge_type value is PrePaid and is required. The value
      range is:

      When PeriodUnit = Week, Period values are: {"1", "2", "3", "4"}

      When PeriodUnit = Month, Period values are: {"1", "2", "3", "4", "5", "6", "7",
      "8", "9", "12", "24", "36", "48", "60"}

      Default to 1.'
    Type: Number
  WorkerPeriodUnit:
    AllowedValues:
    - Week
    - Month
    Default: Month
    Description: 'When you specify PrePaid, you need to specify the period. The options
      are:

      Week: Time is measured in weeks

      Month: time in months

      Default to Month.'
    Type: String
  WorkerSystemDiskCategory:
    Default: cloud_efficiency
    Description: 'Worker node system disk type. The value includes:

      cloud_efficiency: efficient cloud disk

      cloud_ssd: SSD cloud disk

      Default to cloud_efficiency.'
    Type: String
  WorkerSystemDiskSize:
    Default: 120
    Description: 'Worker disk system disk size, the unit is GiB.

      Default to 120.'
    MinValue: 1
    Type: Number
  WorkerVSwitchIds:
    Description: The virtual switch ID of the worker node.
    MinLength: 1
    Type: CommaDelimitedList
Resources:
  KubernetesCluster:
    Properties:
      Addons:
        Ref: Addons
      CloudMonitorFlags:
        Ref: CloudMonitorFlags
      ContainerCidr:
        Ref: ContainerCidr
      CpuPolicy:
        Ref: CpuPolicy
      DisableRollback:
        Ref: DisableRollback
      EndpointPublicAccess:
        Ref: EndpointPublicAccess
      KeyPair:
        Ref: KeyPair
      KubernetesVersion:
        Ref: KubernetesVersion
      LoginPassword:
        Ref: LoginPassword
      MasterAutoRenew:
        Ref: MasterAutoRenew
      MasterAutoRenewPeriod:
        Ref: MasterAutoRenewPeriod
      MasterCount:
        Ref: MasterCount
      MasterDataDisk:
        Ref: MasterDataDisk
      MasterDataDisks:
        Ref: MasterDataDisks
      MasterInstanceChargeType:
        Ref: MasterInstanceChargeType
      MasterInstanceTypes:
        Ref: MasterInstanceTypes
      MasterPeriod:
        Ref: MasterPeriod
      MasterPeriodUnit:
        Ref: MasterPeriodUnit
      MasterSystemDiskCategory:
        Ref: MasterSystemDiskCategory
      MasterSystemDiskSize:
        Ref: MasterSystemDiskSize
      MasterVSwitchIds:
        Ref: MasterVSwitchIds
      Name:
        Ref: Name
      NodePortRange:
        Ref: NodePortRange
      NumOfNodes:
        Ref: NumOfNodes
      PodVswitchIds:
        Ref: PodVswitchIds
      ProxyMode:
        Ref: ProxyMode
      SecurityGroupId:
        Ref: SecurityGroupId
      ServiceCidr:
        Ref: ServiceCidr
      SnatEntry:
        Ref: SnatEntry
      SshFlags:
        Ref: SshFlags
      Tags:
        Ref: Tags
      Taint:
        Ref: Taint
      TimeoutMins:
        Ref: TimeoutMins
      VpcId:
        Ref: VpcId
      WorkerAutoRenew:
        Ref: WorkerAutoRenew
      WorkerAutoRenewPeriod:
        Ref: WorkerAutoRenewPeriod
      WorkerDataDisk:
        Ref: WorkerDataDisk
      WorkerDataDisks:
        Ref: WorkerDataDisks
      WorkerInstanceChargeType:
        Ref: WorkerInstanceChargeType
      WorkerInstanceTypes:
        Ref: WorkerInstanceTypes
      WorkerPeriod:
        Ref: WorkerPeriod
      WorkerPeriodUnit:
        Ref: WorkerPeriodUnit
      WorkerSystemDiskCategory:
        Ref: WorkerSystemDiskCategory
      WorkerSystemDiskSize:
        Ref: WorkerSystemDiskSize
      WorkerVSwitchIds:
        Ref: WorkerVSwitchIds
    Type: ALIYUN::CS::KubernetesCluster
Outputs:
  ClusterId:
    Description: Cluster instance ID.
    Value:
      Fn::GetAtt:
      - KubernetesCluster
      - ClusterId
  TaskId:
    Description: Task ID. Automatically assigned by the system, the user queries the
      task status.
    Value:
      Fn::GetAtt:
      - KubernetesCluster
      - TaskId
  WorkerRamRoleName:
    Description: Worker ram role name.
    Value:
      Fn::GetAtt:
      - KubernetesCluster
      - WorkerRamRoleName
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CS/JSON/KubernetesCluster.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CS/YAML/KubernetesCluster.yml)。


# ALIYUN::CS::KubernetesCluster

ALIYUN::CS::KubernetesCluster is used to create a dedicated Kubernetes cluster.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MasterAutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for master nodes.|This parameter takes effect only when the MasterInstanceChargeType parameter is set to PrePaid. Default value: true. Valid values:

-   true
-   false |
|CloudMonitorFlags|Boolean|No|No|Specifies whether to install the CloudMonitor agent.|Default value: false. Valid values: -   true
-   false |
|ProxyMode|String|No|No|The kube-proxy mode.|Default value: iptables. Valid values: -   iptables
-   ipvs |
|MasterInstanceTypes|List|Yes|No|The instance types of Elastic Compute Service \(ECS\) instances that are used as master nodes.|You must specify three ECS instances types. The instance types can be the same. For more information, see [Instance family](/intl.en-US/Instance/Instance family.md). |
|WorkerInstanceChargeType|String|No|No|The billing method of worker nodes.|Default value: PostPaid. Valid values: -   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|SnatEntry|Boolean|No|No|Specifies whether to configure Source Network Address Translation \(SNAT\) rules for the network.|Valid values:-   Set the value to false when the virtual private cloud \(VPC\) that you select for the cluster can access the Internet.
-   Valid values when the VPC that you select for the cluster cannot access the Internet:
    -   true: configures SNAT rules for the VPC to access the Internet.
    -   false: does not configure SNAT rules. In this case, the VPC cannot access the Internet. |
|WorkerPeriod|Number|No|No|The subscription period.|This parameter is valid and required only when the WorkerInstanceChargeType parameter is set to PrePaid. Valid values:

-   Valid values when the WorkerPeriodUnit parameter is set to Week: 1, 2, 3, and 4.
-   Valid values when the WorkerPeriodUnit parameter is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|WorkerPeriodUnit|String|No|No|The unit of the subscription period.|This parameter is required only when the WorkerInstanceChargeType parameter is set to PrePaid. Default value: Month. Valid values: -   Week
-   Month |
|WorkerSystemDiskCategory|String|No|No|The system disk category of worker nodes.|Default value: cloud\_efficiency. Valid values: -   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD |
|WorkerVSwitchIds|List|Yes|No|The vSwitch IDs of worker nodes.|You can specify up to five vSwitch IDs.|
|MasterInstanceChargeType|String|No|No|The billing method of master nodes.|Default value: PostPaid. Valid values: -   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|VpcId|String|Yes|No|The ID of the VPC.|If you do not specify this parameter, the system creates a VPC whose CIDR block is 192.168.0.0/16. You must specify both the VpcId and MasterVSwitchIds parameters or leave both parameters empty. |
|Tags|List|No|No|The tags of the cluster.|You can specify up to 20 tags. For more information, see [Tags properties](#section_sao_4g8_748). |
|MasterAutoRenewPeriod|Number|No|No|The auto-renewal period of master nodes.|This parameter is valid and required when the MasterInstanceChargeType parameter is set to PrePaid and the MasterAutoRenew parameter is set to true. Valid values: -   Valid values when the MasterPeriodUnit parameter is set to Week: 1, 2, and 3.
-   Valid values when the MasterPeriodUnit parameter is set to Month: 1, 2, 3, 6, and 12.

Default value: 1. |
|PodVswitchIds|List|No|No|The list of pod vSwitches.|For each vSwitch that is allocated to nodes, you must specify at least one pod vSwitch in the same zone. The pod vSwitches cannot be the same as the node vSwitches. We recommend that you set the mask length of the CIDR block to a value no greater than 19 for the pod vSwitches.

**Note:** The PodVswitchIds parameter is required when the Terway network plug-in is specified for the cluster by using the Addons parameter. |
|CpuPolicy|String|No|No|The CPU policy.|For Kubernetes v1.12.6 or later, the default value is none and the following valid values are available:-   static
-   none |
|WorkerInstanceTypes|List|Yes|No|The instance types of ECS instances that are used as worker nodes.|For more information, see [Instance family](/intl.en-US/Instance/Instance family.md).|
|WorkerDataDisks|List|No|No|The data disk configurations of worker nodes, such as the disk category and disk size.|This parameter takes effect only when data disks are attached to worker nodes. For more information, see [WorkerDataDisks properties](#section_cka_mac_ug7). |
|LoginPassword|String|No|No|The password for SSH logon.|The password must be 8 to 30 characters in length. It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. You must specify one of the LoginPassword and KeyPair parameters. |
|ContainerCidr|String|No|No|The container CIDR block.|The CIDR block may overlap with that of the VPC. If the VPC is created by the system, the container CIDR block is set to 172.16.0.0/16 by default.|
|NumOfNodes|Number|No|No|The number of worker nodes.|Valid values: 0 to 300. Default value: 3. |
|Name|String|Yes|No|The name of the cluster.|The name must be 1 to 63 characters in length and can contain letters, digits, and hyphens \(-\).|
|WorkerSystemDiskSize|Number|No|No|The system disk size of worker nodes.|Default value: 120. Unit: GiB. |
|NodePortRange|String|No|No|The service port range of nodes.|Valid values: two values within the range of 30000 to 65535. Separate the two values with a hyphen \(-\). Default value: 30000-65535. |
|SshFlags|Boolean|No|No|Specifies whether to allow Internet access over SSH.|Valid values: -   true
-   false |
|Taint|List|No|No|The taints to be added to nodes to ensure appropriate scheduling of pods.|However, toleration rules allow pods to be scheduled to nodes that have matching taints.|
|MasterDataDisk|Boolean|No|No|Specifies whether to attach data disks to master nodes.|Default value: false. Valid values: -   true
-   false |
|MasterSystemDiskCategory|String|No|No|The system disk category of master nodes.|Valid values: -   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD |
|WorkerAutoRenewPeriod|Number|No|No|The auto-renewal period of worker nodes.|This parameter is valid and required when the WorkerInstanceChargeType parameter is set to PrePaid and the WorkerAutoRenew parameter is set to true. Valid values: -   Valid values when the WorkerPeriodUnit parameter is set to Week: 1, 2, and 3.
-   Valid values when the WorkerPeriodUnit parameter is set to Month: 1, 2, 3, 6, and 12. |
|WorkerDataDisk|Boolean|No|No|Specifies whether to attach data disks to worker nodes.|Default value: false. Valid values: -   true
-   false |
|WorkerAutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for worker nodes.|Default value: true. Valid values: -   true
-   false |
|Addons|List|No|No|The add-ons to be installed for the Kubernetes cluster.|The following types of add-ons are supported:-   Network plug-in

Supported network plug-ins are Flannel and Terway. You must select one of the plug-ins when you create a cluster:

    -   Specify the Flannel plug-in in the `[{"Name":"flannel","Config":""}]` format.
    -   Specify the Terway plug-in in the `[{"Name": "terway-eniip","Config": ""}]` format.
-   Volume plug-in

Supported volume plug-ins are Container Storage Interface \(CSI\) and FlexVolume:

    -   Specify the CSI plug-in in the `[{"Name":"csi-plugin","Config": ""},{"Name": "csi-provisioner","Config": ""}]` format.
    -   Specify the FlexVolume plug-in in the `[{"Name": "flexvolume","Config": ""}]` format.
-   \(Optional\) Log Service component

**Note:** If Log Service is disabled, the cluster audit feature is unavailable.

    -   To use an existing Log Service project, specify the component in the `[{"Name": "logtail-ds","Config": "{\"IngressDashboardEnabled\":\"true\",\"sls_project_name\":\"your_sls_project_name\"}"}]` format.
    -   To create a Log Service project, specify the component in the `[{"Name": "logtail-ds","Config": "{\"IngressDashboardEnabled\":\"true\"}"}]` format.
-   \(Optional\) Ingress controller

By default, nginx-ingress-controller is installed for dedicated Kubernetes clusters.

    -   To install nginx-ingress-controller and enable access over the Internet, specify the Ingress controller in the `[{"Name":"nginx-ingress-controller","Config":"{\"IngressSlbNetworkType\":\"internet\"}"}]` format.
    -   If you do not want to install nginx-ingress-controller, specify the Ingress controller in the `[{"Name": "nginx-ingress-controller","Config": "","Disabled": true}]` format.
-   \(Optional\) Event center

By default, the event center feature is enabled. The event center feature allows you to log and query Kubernetes events. It also allows you to configure alerts for the events. The Logstores that are associated with Kubernetes event centers are free of charge within 90 days. For more information, see [Create and use a Kubernetes event center](/intl.en-US/Application/K8s Event Center/Create and use a Kubernetes event center.md).

Enable the ack-node-problem-detector component in the `[{"Name":"ack-node-problem-detector","Config":"{\"sls_project_name\":\"your_sls_project_name\"}"}]` format.


For more information, see [Addons properties](#section_3nl_fca_4be).|
|DisableRollback|Boolean|No|No|Specifies whether to perform a rollback if the cluster fails to be created.|Default value: true. Valid values: -   true: performs a rollback if the cluster fails to be created.
-   false: does not perform a rollback if the cluster fails to be created.

**Note:** If rollback is enabled when the Kubernetes cluster fails to be created, resources that were generated during the creation of the Kubernetes cluster are released. We recommend that you set this parameter to true. |
|ServiceCidr|String|No|No|The CIDR block of the service.|The CIDR block cannot overlap with that of the VPC or container. If the VPC is created by the system, the service CIDR block is set to 172.19.0.0/20 by default. |
|KubernetesVersion|String|No|No|The cluster versions provided by Container Service for Kubernetes \(ACK\) are consistent with the open source versions. We recommend that you select the latest version.|You can create clusters of the latest two versions. For more information about the Kubernetes versions supported by ACK, see [Overview of Kubernetes versions supported by ACK](/intl.en-US/Release notes/Kubernetes release notes/Overview of Kubernetes versions supported by ACK.md).|
|MasterPeriod|Number|No|No|The subscription period.|This parameter is valid and required when the MasterInstanceChargeType parameter is set to PrePaid. Valid values:

-   Valid values when the MasterPeriodUnit parameter is set to Week: 1, 2, 3, and 4.
-   Valid values when the MasterPeriodUnit parameter is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60.

 Default value: 1.|
|SecurityGroupId|String|No|No|The ID of the security group to which the ECS instances in the cluster belong.|None|
|KeyPair|String|No|No|The name of the key pair.|You must specify one of the LoginPassword and KeyPair parameters.|
|MasterVSwitchIds|List|Yes|No|The vSwitch IDs of master nodes.|You must specify three vSwitch IDs. The specified IDs can be the same. We recommend that you specify three different vSwitches to ensure high availability of the cluster.|
|EndpointPublicAccess|Boolean|No|No|Specifies whether to enable access to the API server over the Internet.|Default value: false. Valid values: -   true: enables access to the API server over the Internet.
-   false: disables access to the API server over the Internet. The API server allows access only over the internal network. |
|MasterSystemDiskSize|Number|No|No|The system disk size of master nodes.|Default value: 120. Unit: GiB. |
|MasterDataDisks|List|No|No|The data disk configurations of master nodes, such as the disk category and disk size.|This parameter takes effect only when data disks are attached to master nodes. For more information, see [MasterDataDisks properties](#section_sqy_mx3_wf0). |
|MasterCount|Number|No|No|The number of master nodes.|Default value: 3. Valid values: -   3
-   5 |
|TimeoutMins|Number|No|No|The timeout period for the system to create a cluster stack.|Default value: 60. Unit: minutes. |
|MasterPeriodUnit|String|No|No|The unit of the billing cycle for master nodes.|This parameter is required when the MasterInstanceChargeType parameter is set to PrePaid. Default value: Month. Valid values:

-   Week
-   Month |

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
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 64 characters in length and cannot start with `aliyun`, `acs:`, `https://`, or `http://`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot start with `aliyun`, `acs:`, `https://`, or `http://`.|

## MasterDataDisks syntax

```
"MasterDataDisks": [
  {
    "Category": String,
    "Size": Number
  }
]
```

## MasterDataDisks properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Category|String|Yes|No|The data disk category of the master node.|Valid values: -   cloud: basic disk
-   cloud\_ssd: standard SSD
-   cloud\_efficiency: ultra disk |
|Size|Number|Yes|No|The data disk size of the master node.|Valid values: 40 to 32768. Unit: GiB. |

## WorkerDataDisks syntax

```
"WorkerDataDisks": [
  {
    "Category": String,
    "Size": Number
  }
]
```

## WorkerDataDisks properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Category|String|Yes|No|The data disk category of the worker node.|Valid values: -   cloud: basic disk
-   cloud\_ssd: standard SSD
-   cloud\_efficiency: ultra disk |
|Size|Number|Yes|No|The data disk size of the worker node.|Valid values: 40 to 32768. Unit: GiB. |

## Addons syntax

```
"Addons": [
  {
    "Disabled": Boolean,
    "Config": String,
    "Name": String
  }
]
```

## Addons properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Disabled|Boolean|No|No|Specifies whether to disable automatic installation of the add-on.|Valid values:-   true: disables automatic installation of the add-on.
-   false: enables automatic installation of the add-on. |
|Config|String|No|No|The configurations of the add-on.|If this parameter is empty, no configuration is required.|
|Name|String|Yes|No|The name of the add-on.|None|

## Response parameters

Fn::GetAtt

-   ClusterId: the ID of the cluster.
-   TaskId: the ID of the task. The task ID is assigned by the system and can be used to query the task status.
-   WorkerRamRoleName: the Resource Access Management \(RAM\) role name of worker nodes.

## Examples

JSON format

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

YAML format

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

To view more examples, visit [KubernetesCluster.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CS/JSON/KubernetesCluster.json) and [KubernetesCluster.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CS/YAML/KubernetesCluster.yml).


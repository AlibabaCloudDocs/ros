# ALIYUN::CS::ManagedEdgeKubernetesCluster

ALIYUN::CS::ManagedEdgeKubernetesCluster is used to create edge Managed Kubernetes clusters.

## Syntax

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
    "ContainerCidr": String,
    "CloudMonitorFlags": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|NumOfNodes|Number|Yes|No|The number of worker nodes.|Valid values: 0 to 300.|
|Profile|String|No|No|The ID of the edge cluster.|None.|
|VpcId|String|No|No|The ID of the VPC. If you do not specify this parameter, the system creates a VPC whose CIDR block is 192.168.0.0/16.|You must specify both the VpcId and VSwitchIds parameters or leave both parameters empty.|
|ServiceCidr|String|No|No|The CIDR block of the service.|The CIDR block cannot overlap with that of the VPC or container. If the VPC is created by the system, the service CIDR block is set to 172.19.0.0/20 by default.|
|Name|String|Yes|No|The name of the cluster.|The name must start with a letter or digit. It can contain letters, digits, and hyphens \(-\).|
|Tags|List|No|No|The tags of the cluster.|You can specify up to 20 tags for a cluster.For more information, see [Tags properties](/intl.en-US/Resource Types/CS/ALIYUN::CS::ManagedKubernetesCluster.md). |
|Addons|List|No|No|The list of add-ons to be installed.|Valid values:-   Network add-ons

The Flannel and Terway network add-on types are supported. You must specify one of the two network types when you create a Kubernetes cluster:

    -   Specify a Flannel add-on in the `[{"Name":"flannel","Config":""}]` format.
    -   Specify a Terway add-on in the `[{"Name": "terway-eniip","Config": ""}]` format.
-   Storage add-ons

The CSI and FlexVolume add-ons are supported:

    -   Specify a CSI add-on in the `[{"Name":"csi-plugin","Config": ""},{"Name": "csi-provisioner","Config": ""}]` format.
    -   Specify a FlexVolume add-on in the `[{"Name": "flexvolume","Config": ""}]` format.
-   \(Optional\) Log add-ons

**Note:** If Log Service is disabled, the cluster audit feature is unavailable.

    -   If you select an existing Log Service project, specify the add-on in the `[{"Name": "logtail-ds","Config": "{\"IngressDashboardEnabled\":\"true\",\"sls_project_name\":\"your_sls_project_name\"}"}]` format.
    -   If you create a Log Service project, specify the add-on in the `[{"Name": "logtail-ds","Config": "{\"IngressDashboardEnabled\":\"true\"}"}]` format.
-   \(Optional\) Ingress add-ons

By default, the nginx-ingress-controller ingress add-on is installed in the dedicated Kubernetes cluster.

    -   If you install nginx-ingress-controller and enable access over the Internet, specify the add-on in the `[{"Name":"nginx-ingress-controller","Config":"{\"IngressSlbNetworkType\":\"internet\"}"}]` format.
    -   If you do not install nginx-ingress-controller, specify the add-on in the `[{"Name": "nginx-ingress-controller","Config": "","Disabled": true}]` format.
-   \(Optional\) Event center. By default, the event center feature is enabled.

The event center feature allows you to store and query Kubernetes events. It also allows you to configure alerts for the events. The Logstore feature associated with Kubernetes event centers are free of charge within 90 days. For more information, see [Create and use a Kubernetes event center](/intl.en-US/Application/K8s Event Center/Create and use a Kubernetes event center.md).

If you enable the event center feature, specify the add-on in the `[{"Name":"ack-node-problem-detector","Config":"{\"sls_project_name\":\"your_sls_project_name\"}"}]` format.


For more information, see [Addons properties](#section_0xt_i2a_ga9).|
|ProxyMode|String|No|No|The kube-proxy mode.|Default value: iptables. Valid values:-   iptables
-   ipvs |
|DisableRollback|Boolean|No|No|Specifies whether to disable rollback for the resource if the Kubernetes cluster fails to be created.|Default value: true. Valid values:-   true: disables rollback for the resource if the Kubernetes cluster fails to be created.
-   false: enables rollback for the resource if the Kubernetes cluster fails to be created. If rollback is enabled when the Kubernetes cluster fails to be created, resources that were generated during the creation of the Kubernetes cluster are released. We recommend that you set this parameter to true. |
|SnatEntry|Boolean|No|No|Specifies whether to configure Source Network Address Translation \(SNAT\) rules for the network.|If you want to use an automatically created VPC, set this parameter to true.If an existing VPC is specified, set this parameter based on whether the VPC has Internet access. |
|VSwitchIds|List|No|No|The list of vSwitch IDs.|One to three vSwitch IDs can be specified.You must specify both the VpcId and VSwitchIds parameters or leave both parameters empty. |
|LoginPassword|String|No|No|The logon password.|The password must be 8 to 30 characters in length. It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? /`.You must specify one of the LoginPassword and KeyPair parameters. |
|KeyPair|String|No|No|The name of the key pair.|You must specify one of the LoginPassword and KeyPair parameters.|
|EndpointPublicAccess|Boolean|No|No|Specifies whether to enable access to the API server over the Internet.|Default value: true. Valid values: -   true: enables access to the API server over the Internet.
-   false: disables access to the API server over the Internet. The API server allows access only over the internal network. |
|WorkerSystemDiskSize|Number|No|No|The system disk size of the worker node.|Default value: 120.Unit: GiB. |
|WorkerSystemDiskCategory|String|No|No|The system disk category of the worker node.|Default value: cloud\_efficiency.|
|WorkerDataDisk|Boolean|No|No|Specifies whether to attach a data disk to the worker node.|Default value: false. Valid values:-   true
-   false |
|WorkerDataDiskSize|Integer|No|No|The size of a data disk attached to the worker node.|None.|
|WorkerDataDiskCategory|String|No|No|The category of a data disk attached to the worker node.|None.|
|TimeoutMins|Number|No|No|The timeout period for the system to create a cluster stack.|Default value: 60.Unit: minutes. |
|ContainerCidr|String|No|No|The container CIDR block.|The CIDR block cannot overlap with that of the VPC. If the VPC is created by the system, the container CIDR block is set to 172.16.0.0/16 by default.|
|CloudMonitorFlags|Boolean|No|No|Specifies whether to install the Cloud Monitor agent.|Default value: false. Valid values:-   true
-   false |

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
|Key|String|Yes|No|The key of a tag.|The tag key must be 1 to 64 characters in length and cannot start with `aliyun`, `acs:`, `http://`, or `https://`.|
|Value|String|No|No|The value of a tag.|The tag value can be up to 128 characters in length and cannot start with `aliyun`, `acs:`, `http://`, or `https://`.|

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
|Name|String|Yes|No|The name of the add-on.|None.|

## Return value

Fn::GetAtt

-   ClusterId: the ID of the cluster.
-   TaskId: the ID of the task. The task ID is assigned by the system and can be used to query the task status.
-   WorkerRamRoleName: the RAM role name of the worker node.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EndpointPublicAccess": {
      "Type": "Boolean",
      "Description": "Whether to enable the public network API Server:\ntrue: which means that the public network API Server is open.\nfalse: If set to false, the API server on the public network will not be created, only the API server on the private network will be created. Default to true.",
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

`YAML` format

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


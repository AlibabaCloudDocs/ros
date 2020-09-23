# ALIYUN::CS::ManagedEdgeKubernetesCluster

ALIYUN::CS::ManagedEdgeKubernetesCluster is used to create a managed edge Container Service for Kubernetes \(ACK\) cluster.

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
|Profile|String|No|No|The ID of the edge cluster.|None|
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\). If this parameter is not specified, the system automatically creates a VPC whose CIDR block is 192.168.0.0/16.|You must specify both the VpcId and VSwitchIds parameters or leave both parameters empty.|
|ServiceCidr|String|No|No|The CIDR block of the service.|The CIDR block cannot overlap with that of the VPC or container. If the VPC is automatically created by the system, the service CIDR block is set to 172.19.0.0/20 by default.|
|Name|String|Yes|No|The name of the cluster.|The name must start with a letter or digit. It can contain uppercase letters, lowercase letters, digits, and hyphens \(-\).|
|Tags|List|No|No|The tags of the cluster.|A maximum of 20 tags can be specified.For more information, see [Tags properties](/intl.en-US/Resource Types/CS/ALIYUN::CS::ManagedKubernetesCluster.md). |
|ProxyMode|String|No|No|The kube-proxy mode.|Default value: iptables. Valid values:-   iptables
-   IPVS |
|DisableRollback|Boolean|No|No|Specify whether to roll back resources when the operation fails.|Default value: true. Valid values:-   true: disables rollback upon failure.
-   false: enables rollback upon failure. If you choose to enable rollback when the operation fails, resources that are created during the operation are released. We recommend that you set this parameter to true. |
|SnatEntry|Boolean|No|No|Specifies whether to configure Source Network Address Translation \(SNAT\) rules for the network.|If you want to use an automatically created VPC, set this parameter to true.If an existing VPC is specified, set this parameter based on whether the VPC has Internet access. |
|VSwitchIds|List|No|No|The list of VSwitch IDs.|One to three VSwitch IDs can be specified.You must specify both the VpcId and VSwitchIds parameters or leave both parameters empty. |
|LoginPassword|String|No|No|The logon password.|The password must be 8 to 30 characters in length. It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include```
( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? /
```

You must specify one of the LoginPassword and KeyPair parameters. |
|KeyPair|String|No|No|The name of the key pair.|You must specify one of the LoginPassword and KeyPair parameters.|
|EndpointPublicAccess|Boolean|No|No|Specifies whether to enable access to the API server over the Internet.|Default value: true. Valid values:-   true: enables access to the API server over the Internet.
-   false: disables access to the API server over the Internet. The API server allows only access over an internal network.

**Note:** To create a managed edge cluster, enable Internet access to the API server. This allows edge nodes to connect to the management nodes in the cloud over the Internet. |
|WorkerSystemDiskSize|Number|No|No|The system disk size of worker nodes.|Default value: 120.Unit: GiB. |
|WorkerSystemDiskCategory|String|No|No|The system disk type of worker nodes.|Default value: cloud\_efficiency.|
|WorkerDataDisk|Boolean|No|No|Specifies whether to attach data disks to worker nodes.|Default value: false. Valid values:-   true
-   false |
|WorkerDataDiskSize|Integer|No|No|The data disk size of worker nodes.|None|
|WorkerDataDiskCategory|String|No|No|The type of the data disk.|None|
|TimeoutMins|Number|No|No|The timeout period for the system to create a cluster stack.|Default value: 60.Unit: minutes. |
|ContainerCidr|String|No|No|The container CIDR block.|The CIDR block cannot overlap with that of the VPC. If the VPC is automatically created by the system, the container CIDR block is set to 172.16.0.0/16 by default.|
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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 64 characters in length and cannot start with `aliyun`, `acs:`, `http://`, or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `aliyun`, `acs:`, `http://`, or `https://`.|

## Response parameters

Fn::GetAtt

-   ClusterId: the ID of the cluster.
-   TaskId: the ID of the task. The task ID is automatically assigned by the system and can be used to query the task status.
-   WorkerRamRoleName: the RAM role name of the worker node.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EndpointPublicAccess": {
      "Type": "Boolean",
      "Description": "Whether to enable the public network API Server:\ntrue: which means that the public network API Server is open.\nfalse: If set to false, the API server on the public network will not be created, only the API server on the private network will be created.Default to true.",
      "AllowedValues": [
        true,
        false
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
    "WorkerSystemDiskSize": {
      "Type": "Number",
      "Description": "Worker disk system disk size, the unit is GiB.\nDefault to 120.",
      "MinValue": 1,
      "Default": 120
    },
    "WorkerSystemDiskCategory": {
      "Type": "String",
      "Description": "Worker node system disk type. \nDefault to cloud_efficiency.",
      "Default": "cloud_efficiency"
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
        true,
        false
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
    "NumOfNodes": {
      "Type": "Number",
      "Description": "Number of worker nodes. The range is [0,300]",
      "MinValue": 0,
      "MaxValue": 300
    },
    "CloudMonitorFlags": {
      "Type": "Boolean",
      "Description": "Whether to install the cloud monitoring plugin:\ntrue: indicates installation\nfalse: Do not install\nDefault to false",
      "AllowedValues": [
        true,
        false
      ],
      "Default": false
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
        true,
        false
      ],
      "Default": true
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tag the cluster."
    },
    "ProxyMode": {
      "Type": "String",
      "Description": "kube-proxy proxy mode, supports both iptables and IPVS modes. The default is iptables.",
      "AllowedValues": [
        "iptables",
        "IPVS"
      ],
      "Default": "iptables"
    },
    "DisableRollback": {
      "Type": "Boolean",
      "Description": "Whether the failure was rolled back:\ntrue: indicates that it fails to roll back\nfalse: rollback failed\nThe default is true. If rollback fails, resources produced during the creation process will be released. False is not recommended.",
      "AllowedValues": [
        true,
        false
      ],
      "Default": true
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
        "WorkerSystemDiskSize": {
          "Ref": "WorkerSystemDiskSize"
        },
        "WorkerSystemDiskCategory": {
          "Ref": "WorkerSystemDiskCategory"
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
        "NumOfNodes": {
          "Ref": "NumOfNodes"
        },
        "CloudMonitorFlags": {
          "Ref": "CloudMonitorFlags"
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
        "Tags": {
          "Ref": "Tags"
        },
        "ProxyMode": {
          "Ref": "ProxyMode"
        },
        "DisableRollback": {
          "Ref": "DisableRollback"
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
      - true
      - false
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
  WorkerSystemDiskSize:
    Type: Number
    Description: |-
      Worker disk system disk size, the unit is GiB.
      Default to 120.
    MinValue: 1
    Default: 120
  WorkerSystemDiskCategory:
    Type: String
    Description: |-
      Worker node system disk type.
      Default to cloud_efficiency.
    Default: cloud_efficiency
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
      - true
      - false
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
  NumOfNodes:
    Type: Number
    Description: 'Number of worker nodes. The range is [0,300]'
    MinValue: 0
    MaxValue: 300
  CloudMonitorFlags:
    Type: Boolean
    Description: |-
      Whether to install the cloud monitoring plugin:
      true: indicates installation
      false: Do not install
      Default to false
    AllowedValues:
      - true
      - false
    Default: false
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
      - true
      - false
    Default: true
  Tags:
    Type: Json
    Description: Tag the cluster.
  ProxyMode:
    Type: String
    Description: >-
      kube-proxy proxy mode, supports both iptables and IPVS modes. The default
      is iptables.
    AllowedValues:
      - iptables
      - IPVS
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
      - true
      - false
    Default: true
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
      WorkerSystemDiskSize:
        Ref: WorkerSystemDiskSize
      WorkerSystemDiskCategory:
        Ref: WorkerSystemDiskCategory
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
      NumOfNodes:
        Ref: NumOfNodes
      CloudMonitorFlags:
        Ref: CloudMonitorFlags
      ServiceCidr:
        Ref: ServiceCidr
      WorkerDataDiskCategory:
        Ref: WorkerDataDiskCategory
      SnatEntry:
        Ref: SnatEntry
      Tags:
        Ref: Tags
      ProxyMode:
        Ref: ProxyMode
      DisableRollback:
        Ref: DisableRollback
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


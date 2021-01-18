# ALIYUN::CS::ServerlessKubernetesCluster

ALIYUN::CS::ServerlessKubernetesCluster is used to create a serverless Kubernetes cluster.

## Syntax

```
{
  "Type": "ALIYUN::CS::ServerlessKubernetesCluster",
  "Properties": {
    "VpcId": String,
    "Name": String,
    "Tags": List,
    "ZoneId": String,
    "PrivateZone": Boolean,
    "VSwitchId": String,
    "EndpointPublicAccess": Boolean,
    "SecurityGroupId": String,
    "VSwitchIds": List,
    "ServiceCidr": String,
    "Addons": List,
    "KubernetesVersion": String,
    "NatGateway": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|No|No|The ID of the VPC. If you do not specify this parameter, the system creates a VPC whose CIDR block is 192.168.0.0/16.|You must specify both the VpcId and VSwitchId parameters or leave both of the parameters empty.|
|Name|String|Yes|No|The description of the cluster.|The name must start with a digit or letter. The name can contain letters, digits, and hyphens \(-\).|
|Tags|List|No|No|The tags of the cluster.|For more information, see the [Tags properties](#section_7qg_fno_qn9) section.|
|ZoneId|String|No|No|The ID of the zone.|None|
|PrivateZone|Boolean|No|No|Specifies whether to enable Alibaba Cloud DNS PrivateZone for service discovery.|Default value: false. Valid values: -   true
-   false

For more information, see [Use the service discovery feature based on Alibaba Cloud DNS PrivateZone in ASK clusters](/intl.en-US/User Guide for Serverless Kubernetes Clusters/Application management/Use the service discovery feature based on Alibaba Cloud DNS PrivateZone in ASK clusters.md).|
|VSwitchId|String|No|No|The ID of the vSwitch. If this parameter is not specified, the system creates a vSwitch whose CIDR block is 192.168.0.0/16.|You must specify both the VpcId and VSwitchId parameters or leave both of the parameters empty.|
|EndpointPublicAccess|Boolean|No|No|Specifies whether to enables access to the API server over the Internet.|Default value: false. Valid values: -   true: enables access to the API server over the Internet.
-   false: disables access to the API server over the Internet. The API server allows access only over the internal network. |
|SecurityGroupId|String|No|No|The ID of the security group to which the ECS instances in the cluster belong.|None|
|VSwitchIds|List|No|No|The ID of the vSwitch. If you do not set this parameter, the system creates a vSwitch whose CIDR block is 192.168.0.0/16.|You can specify up to 10 vSwitch IDs.|
|ServiceCidr|String|No|No|The CIDR block of the service.|The CIDR block cannot overlap with that of the VPC or container. If the VPC is created by the system, the service CIDR block is set to 172.19.0.0/20 by default. |
|Addons|List|No|No|The list of add-ons to be installed. A serverless Kubernetes cluster supports only add-ons of Log Service.-   Create a new project: `[{"Name":"logtail-ds","Config":""}]`
-   Use an existing project: `[{"Name":"logtail-ds","Config":"{"sls_project_name":"your_sls_project_name"}"}]`

|None|
|KubernetesVersion|String|No|No|The version of the cluster.|Valid values:-   1.14.8-aliyun.1
-   1.16.9-aliyun.1 |
|NatGateway|Boolean|No|No|Specifies whether to create a NAT gateway.|Default value: false. Valid values: -   true
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
|Key|String|Yes|No|The tag key.|The key must be 1 to 64 characters in length and cannot start with `aliyun`, `acs:`, `https://`, or `http://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `aliyun`, `acs:`, `https://`, or `http://`.|

## Addons syntax

```
"Addons": [
  {
    "Disabled": String,
    "Config": String,
    "Name": String
  }
]
```

## Addons properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Disabled|String|No|No|Specifies whether to disable automatic installation of the add-on.|None|
|Config|String|No|No|The configurations of the add-on.|If this parameter is empty, no configuration is required.|
|Name|String|Yes|No|The name of the add-on.|None|

## Response parameters

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
    "KubernetesVersion": {
      "Type": "String",
      "Description": "Kubernetes version. Default to 1.14.8-aliyun.1, 1.16.9-aliyun.1 and so on .",
      "Default": "1.14.8-aliyun.1"
    },
    "EndpointPublicAccess": {
      "Type": "Boolean",
      "Description": "Whether to enable the public network API Server:\ntrue: which means that the public network API Server is open.\nfalse: If set to false, the API server on the public network will not be created, only the API server on the private network will be created.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone ID."
    },
    "VSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "The IDs of VSwitches. If you leave this property empty, the system automatically creates a VSwitch.\nNote You must specify both the VpcId and VSwitchIds or leave both of them empty.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Specifies the ID of the security group to which the cluster ECS instance belongs."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "If not set, the system will automatically create a switch, and the network segment of the switch created by the system is 192.168.0.0/18."
    },
    "Addons": {
      "Type": "Json",
      "Description": "The add-ons to be installed for the cluster."
    },
    "NatGateway": {
      "Type": "Boolean",
      "Description": "Whether to create a NAT gateway. The value can be true or false. If not set, the system defaults to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the cluster. The cluster name can use uppercase and lowercase letters, Chinese characters, numbers, and dashes."
    },
    "VpcId": {
      "Type": "String",
      "Description": "VPC ID. If not set, the system will automatically create a VPC, and the VPC network segment created by the system is 192.168.0.0/16. \nVpcId and VSwitchId can only be empty at the same time or set the corresponding values at the same time."
    },
    "ServiceCidr": {
      "Type": "String",
      "Description": "The service network segment cannot conflict with the VPC network segment and the container network segment. When the system is selected to automatically create a VPC, the network segment 172.19.0.0/20 is used by default.",
      "Default": "172.19.0.0/20"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tag the cluster."
    },
    "PrivateZone": {
      "Type": "Boolean",
      "Description": "Whether to enable PrivateZone for service discovery.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "ServerlessKubernetesCluster": {
      "Type": "ALIYUN::CS::ServerlessKubernetesCluster",
      "Properties": {
        "KubernetesVersion": {
          "Ref": "KubernetesVersion"
        },
        "EndpointPublicAccess": {
          "Ref": "EndpointPublicAccess"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchIds": {
          "Ref": "VSwitchIds"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Addons": {
          "Ref": "Addons"
        },
        "NatGateway": {
          "Ref": "NatGateway"
        },
        "Name": {
          "Ref": "Name"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "ServiceCidr": {
          "Ref": "ServiceCidr"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PrivateZone": {
          "Ref": "PrivateZone"
        }
      }
    }
  },
  "Outputs": {
    "TaskId": {
      "Description": "Task ID. Automatically assigned by the system, the user queries the task status.",
      "Value": {
        "Fn::GetAtt": [
          "ServerlessKubernetesCluster",
          "TaskId"
        ]
      }
    },
    "ClusterId": {
      "Description": "Cluster instance ID.",
      "Value": {
        "Fn::GetAtt": [
          "ServerlessKubernetesCluster",
          "ClusterId"
        ]
      }
    },
    "WorkerRamRoleName": {
      "Description": "Worker ram role name.",
      "Value": {
        "Fn::GetAtt": [
          "ServerlessKubernetesCluster",
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
  KubernetesVersion:
    Type: String
    Description: >-
      Kubernetes version. Default to 1.14.8-aliyun.1, 1.16.9-aliyun.1 and so on
      .
    Default: 1.14.8-aliyun.1
  EndpointPublicAccess:
    Type: Boolean
    Description: >-
      Whether to enable the public network API Server:

      true: which means that the public network API Server is open.

      false: If set to false, the API server on the public network will not be
      created, only the API server on the private network will be created.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  ZoneId:
    Type: String
    Description: The zone ID.
  VSwitchIds:
    Type: CommaDelimitedList
    Description: >-
      The IDs of VSwitches. If you leave this property empty, the system
      automatically creates a VSwitch.

      Note You must specify both the VpcId and VSwitchIds or leave both of them
      empty.
    MinLength: 1
    MaxLength: 10
  SecurityGroupId:
    Type: String
    Description: >-
      Specifies the ID of the security group to which the cluster ECS instance
      belongs.
  VSwitchId:
    Type: String
    Description: >-
      If not set, the system will automatically create a switch, and the network
      segment of the switch created by the system is 192.168.0.0/18.
  Addons:
    Type: Json
    Description: The add-ons to be installed for the cluster.
  NatGateway:
    Type: Boolean
    Description: >-
      Whether to create a NAT gateway. The value can be true or false. If not
      set, the system defaults to false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  Name:
    Type: String
    Description: >-
      The name of the cluster. The cluster name can use uppercase and lowercase
      letters, Chinese characters, numbers, and dashes.
  VpcId:
    Type: String
    Description: >-
      VPC ID. If not set, the system will automatically create a VPC, and the
      VPC network segment created by the system is 192.168.0.0/16. 

      VpcId and VSwitchId can only be empty at the same time or set the
      corresponding values at the same time.
  ServiceCidr:
    Type: String
    Description: >-
      The service network segment cannot conflict with the VPC network segment
      and the container network segment. When the system is selected to
      automatically create a VPC, the network segment 172.19.0.0/20 is used by
      default.
    Default: 172.19.0.0/20
  Tags:
    Type: Json
    Description: Tag the cluster.
  PrivateZone:
    Type: Boolean
    Description: Whether to enable PrivateZone for service discovery.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
Resources:
  ServerlessKubernetesCluster:
    Type: 'ALIYUN::CS::ServerlessKubernetesCluster'
    Properties:
      KubernetesVersion:
        Ref: KubernetesVersion
      EndpointPublicAccess:
        Ref: EndpointPublicAccess
      ZoneId:
        Ref: ZoneId
      VSwitchIds:
        Ref: VSwitchIds
      SecurityGroupId:
        Ref: SecurityGroupId
      VSwitchId:
        Ref: VSwitchId
      Addons:
        Ref: Addons
      NatGateway:
        Ref: NatGateway
      Name:
        Ref: Name
      VpcId:
        Ref: VpcId
      ServiceCidr:
        Ref: ServiceCidr
      Tags:
        Ref: Tags
      PrivateZone:
        Ref: PrivateZone
Outputs:
  TaskId:
    Description: >-
      Task ID. Automatically assigned by the system, the user queries the task
      status.
    Value:
      'Fn::GetAtt':
        - ServerlessKubernetesCluster
        - TaskId
  ClusterId:
    Description: Cluster instance ID.
    Value:
      'Fn::GetAtt':
        - ServerlessKubernetesCluster
        - ClusterId
  WorkerRamRoleName:
    Description: Worker ram role name.
    Value:
      'Fn::GetAtt':
        - ServerlessKubernetesCluster
        - WorkerRamRoleName
```


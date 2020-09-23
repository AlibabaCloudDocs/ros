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
    "NatGateway": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\). If this parameter is not specified, the system automatically creates a VPC whose CIDR block is 192.168.0.0/16.|You must specify both the VpcId and VSwitchId parameters or leave both parameters empty.|
|Name|String|Yes|No|The name of the cluster.|The name must start with a digit or letter. The name can contain letters, digits, and hyphens \(-\).|
|Tags|List|No|No|The tags of the cluster.|For more information, see [Tags properties](#section_7qg_fno_qn9).|
|ZoneId|String|No|No|The ID of the zone.|None|
|PrivateZone|Boolean|No|No|Specifies whether to enable Alibaba Cloud DNS PrivateZone for service discovery.|Default value: false. Valid values: -   true
-   false

For more information, see [Use the service discovery feature based on Alibaba Cloud DNS PrivateZone in serverless Kubernetes clusters](/intl.en-US/User Guide for Serverless Kubernetes Clusters/Application management/Serverless clusters support the service discovery based on Alibaba Cloud DNS PrivateZone.md).|
|VSwitchId|String|No|No|The ID of the VSwitch. If this parameter is not specified, the system automatically creates a VSwitch whose CIDR block is 192.168.0.0/16.|You must specify both the VpcId and VSwitchId parameters or leave both parameters empty.|
|NatGateway|Boolean|No|No|Specifies whether to create a Network Address Translation \(NAT\) gateway.|Default value: false. Valid values: -   true
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
    "VpcId": {
      "Type": "String",
      "Description": "VPC ID. If not set, the system will automatically create a VPC, and the VPC network segment created by the system is 192.168.0.0/16. \nVpcId and VSwitchId can only be empty at the same time or set the corresponding values at the same time."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone ID."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "If not set, the system will automatically create a switch, and the network segment of the switch created by the system is 192.168.0.0/18."
    },
    "NatGateway": {
      "Type": "Boolean",
      "Description": "Whether to create a NAT gateway. The value can be true or false. If not set, the system defaults to false.",
      "AllowedValues": [
        true,
        false
      ],
      "Default": false
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tag the cluster."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the cluster. The cluster name can use uppercase and lowercase letters, Chinese characters, numbers, and dashes."
    },
    "PrivateZone": {
      "Type": "Boolean",
      "Description": "Whether to enable PrivateZone for service discovery.",
      "AllowedValues": [
        true,
        false
      ]
    }
  },
  "Resources": {
    "ServerlessKubernetesCluster": {
      "Type": "ALIYUN::CS::ServerlessKubernetesCluster",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "NatGateway": {
          "Ref": "NatGateway"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "Name": {
          "Ref": "Name"
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
  VpcId:
    Type: String
    Description: >-
      VPC ID. If not set, the system will automatically create a VPC, and the
      VPC network segment created by the system is 192.168.0.0/16.

      VpcId and VSwitchId can only be empty at the same time or set the
      corresponding values at the same time.
  ZoneId:
    Type: String
    Description: The zone ID.
  VSwitchId:
    Type: String
    Description: >-
      If not set, the system will automatically create a switch, and the network
      segment of the switch created by the system is 192.168.0.0/18.
  NatGateway:
    Type: Boolean
    Description: >-
      Whether to create a NAT gateway. The value can be true or false. If not
      set, the system defaults to false.
    AllowedValues:
      - true
      - false
    Default: false
  Tags:
    Type: Json
    Description: Tag the cluster.
  Name:
    Type: String
    Description: >-
      The name of the cluster. The cluster name can use uppercase and lowercase
      letters, Chinese characters, numbers, and dashes.
  PrivateZone:
    Type: Boolean
    Description: Whether to enable PrivateZone for service discovery.
    AllowedValues:
      - true
      - false
Resources:
  ServerlessKubernetesCluster:
    Type: 'ALIYUN::CS::ServerlessKubernetesCluster'
    Properties:
      VpcId:
        Ref: VpcId
      ZoneId:
        Ref: ZoneId
      VSwitchId:
        Ref: VSwitchId
      NatGateway:
        Ref: NatGateway
      Tags:
        Ref: Tags
      Name:
        Ref: Name
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


# ALIYUN::CS::ServerlessKubernetesCluster

ALIYUN::CS::ServerlessKubernetesCluster类型用于创建Serverless Kubernetes集群实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|否|否|专有网络ID。如果不设置，系统会自动创建专有网络，系统创建的专有网络网段为192.168.0.0/16。|VpcId和VSwitchId只能同时为空或者同时都设置对应的值。|
|Name|String|是|否|集群名称。|必须以数字或英文字母开头。可包含英文字母、汉字、数字和短划线（-）。|
|Tags|List|否|否|集群标签。|详情请参见[Tags属性](#section_7qg_fno_qn9)。|
|ZoneId|String|否|否|可用区。|无|
|PrivateZone|Boolean|否|否|是否开启PrivateZone用于服务发现。|取值： -   true
-   false（默认值）

详情请参见[Serverless集群基于云解析PrivateZone的服务发现](/intl.zh-CN/Serverless Kubernetes集群用户指南/应用管理/Serverless集群基于云解析PrivateZone的服务发现.md)。|
|VSwitchId|String|否|否|交换机ID。如果不设置，系统会自动创建交换机，系统创建的交换机网段为192.168.0.0/16。|VpcId和VSwitchId只能同时为空或者同时都设置对应的值。|
|NatGateway|Boolean|否|否|是否创建NAT网关。|取值： -   true
-   false（默认值） |

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
|Key|String|是|否|标签键|长度为1~64个字符，不能以`aliyun`、`acs:`、`https://`或`http://`开头。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`、`acs:`、`https://`或`http://`开头。|

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

`YAML`格式

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


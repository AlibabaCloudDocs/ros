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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|否|否|专有网络ID。如果不设置，系统会自动创建专有网络，系统创建的专有网络网段为192.168.0.0/16。|VpcId和VSwitchId只能同时为空或者同时都设置对应的值。|
|Name|String|是|否|集群名称。|必须以数字或英文字母开头。可包含英文字母、汉字、数字和短划线（-）。|
|Tags|List|否|否|集群标签。|更多信息，请参见[Tags属性](#section_7qg_fno_qn9)。|
|ZoneId|String|否|否|可用区。|无|
|PrivateZone|Boolean|否|否|是否开启PrivateZone用于服务发现。|取值： -   true
-   false（默认值）

更多信息，请参见[Serverless集群基于云解析PrivateZone的服务发现](/cn.zh-CN/Serverless Kubernetes集群用户指南/应用管理/Serverless集群基于云解析PrivateZone的服务发现.md)。|
|VSwitchId|String|否|否|交换机ID。如果不设置，系统会自动创建交换机，系统创建的交换机网段为192.168.0.0/16。|VpcId和VSwitchId只能同时为空或者同时都设置对应的值。|
|EndpointPublicAccess|Boolean|否|否|是否开启公网API Server。|取值： -   true（默认值）：开启公网API Server。
-   false：仅开启私网API Server。 |
|SecurityGroupId|String|否|否|集群ECS实例所属的安全组ID。|无|
|VSwitchIds|List|否|否|交换机ID列表。若不设置，系统会自动创建交换机，系统自动创建的交换机网段为192.168.0.0/16。|最多支持10个交换机ID。|
|ServiceCidr|String|否|否|服务网段。|不能和专有网络网段以及容器网段冲突。 当选择系统自动创建专有网络时，默认使用172.19.0.0/20网段。 |
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


更多信息，请参见[Addons属性](#section_1q6_jga_mlb)。|
|KubernetesVersion|String|否|否|集群版本。|取值：-   1.14.8-aliyun.1
-   1.16.9-aliyun.1 |
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
|Key|String|是|否|标签键。|长度为1~64个字符，不能以`aliyun`、`acs:`、`https://`或`http://`开头。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`、`acs:`、`https://`或`http://`开头。|

## Addons语法

```
"Addons": [
  {
    "Disabled": String,
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

`YAML`格式

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


# ALIYUN::EDAS::K8sCluster

ALIYUN::EDAS::K8sCluster类型用于创建K8s集群。

## 语法

```
{
  "Type": "ALIYUN::EDAS::K8sCluster",
  "Properties": {
    "EnableAsm": String,
    "NamespaceId": String,
    "CsClusterId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EnableAsm|String|否|否|是否开启服务网格ASM。|取值：-   true：开启。
-   false：不开启。 |
|NamespaceId|String|否|否|命名空间ID。|格式：`地域ID:微服务空间标识符`。示例值：`cn-hangzhou:doc`。 |
|CsClusterId|String|是|否|集群ID。|您可以调用[GetK8sCluster]()接口获取集群ID。|

## 返回值

Fn::GetAtt

-   VpcId：专有网络ID。
-   NodeNum：节点数。
-   ClusterId：集群ID。
-   ClusterName：集群名称。
-   SubNetCidr：子网CIDR。
-   NetworkMode：网络模式。1表示经典网络，2表示专有网络。
-   ClusterType：集群类型。2表示ECS集群，5表示容器服务K8s集群或无服务器K8s集群。
-   CsClusterId：K8s集群ID。
-   VswitchId：交换机ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EnableAsm": {
      "Type": "String",
      "Description": "Whether enable ASM."
    },
    "NamespaceId": {
      "Type": "String",
      "Description": "The ID of the namespace to which the cluster that you want to import belongs."
    },
    "CsClusterId": {
      "Type": "String",
      "Description": "The ID of the CS cluster."
    }
  },
  "Resources": {
    "K8sCluster": {
      "Type": "ALIYUN::EDAS::K8sCluster",
      "Properties": {
        "EnableAsm": {
          "Ref": "EnableAsm"
        },
        "NamespaceId": {
          "Ref": "NamespaceId"
        },
        "CsClusterId": {
          "Ref": "CsClusterId"
        }
      }
    }
  },
  "Outputs": {
    "VpcId": {
      "Description": "The ID of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "VpcId"
        ]
      }
    },
    "NodeNum": {
      "Description": "Number of nodes.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "NodeNum"
        ]
      }
    },
    "ClusterId": {
      "Description": "The ID of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "ClusterId"
        ]
      }
    },
    "ClusterName": {
      "Description": "The name of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "ClusterName"
        ]
      }
    },
    "SubNetCidr": {
      "Description": "Sub net CIDR.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "SubNetCidr"
        ]
      }
    },
    "NetworkMode": {
      "Description": "Network node:\n1: Classic network\n2: VPC",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "NetworkMode"
        ]
      }
    },
    "ClusterType": {
      "Description": "The type of the cluster:\n2: ECS cluster\n5: Container Service K8s cluster or Serverless K8s cluster",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "ClusterType"
        ]
      }
    },
    "CsClusterId": {
      "Description": "The ID of the K8s cluster.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "CsClusterId"
        ]
      }
    },
    "VswitchId": {
      "Description": "The ID of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "K8sCluster",
          "VswitchId"
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
  CsClusterId:
    Description: The ID of the CS cluster.
    Type: String
  EnableAsm:
    Description: Whether enable ASM.
    Type: String
  NamespaceId:
    Description: The ID of the namespace to which the cluster that you want to import
      belongs.
    Type: String
Resources:
  K8sCluster:
    Properties:
      CsClusterId:
        Ref: CsClusterId
      EnableAsm:
        Ref: EnableAsm
      NamespaceId:
        Ref: NamespaceId
    Type: ALIYUN::EDAS::K8sCluster
Outputs:
  ClusterId:
    Description: The ID of the cluster.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - ClusterId
  ClusterName:
    Description: The name of the cluster.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - ClusterName
  ClusterType:
    Description: 'The type of the cluster:

      2: ECS cluster

      5: Container Service K8s cluster or Serverless K8s cluster'
    Value:
      Fn::GetAtt:
      - K8sCluster
      - ClusterType
  CsClusterId:
    Description: The ID of the K8s cluster.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - CsClusterId
  NetworkMode:
    Description: 'Network node:

      1: Classic network

      2: VPC'
    Value:
      Fn::GetAtt:
      - K8sCluster
      - NetworkMode
  NodeNum:
    Description: Number of nodes.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - NodeNum
  SubNetCidr:
    Description: Sub net CIDR.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - SubNetCidr
  VpcId:
    Description: The ID of the cluster.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - VpcId
  VswitchId:
    Description: The ID of the cluster.
    Value:
      Fn::GetAtt:
      - K8sCluster
      - VswitchId
```


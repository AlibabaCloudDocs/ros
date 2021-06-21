# ALIYUN::EDAS::K8sCluster

ALIYUN::EDAS::K8sCluster is used to create a Kubernetes cluster.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EnableAsm|String|No|No|Specifies whether to enable Alibaba Cloud Service Mesh \(ASM\).|Valid values:-   true: ASM is enabled.
-   false: ASM is disabled. |
|NamespaceId|String|No|No|The ID of the namespace.|The format is `<Region ID>:<Microservice namespace ID>`. Example: `cn-hangzhou:doc`. |
|CsClusterId|String|Yes|No|The ID of the cluster.|You can call the [t1941901.md\#]() operation to query the ID of the cluster.|

## Response parameters

Fn::GetAtt

-   VpcId: the ID of the virtual private cloud \(VPC\).
-   NodeNum: the number of nodes.
-   ClusterId: the ID of the cluster.
-   ClusterName: the name of the cluster.
-   SubNetCidr: the CIDR block of the subnet.
-   NetworkMode: the network type of the cluster. A value of 1 indicates the classic network. A value of 2 indicates a VPC.
-   ClusterType: the type of the cluster. A value of 2 indicates an Elastic Compute Service \(ECS\) cluster. A value of 5 indicates a Container Service for Kubernetes cluster or a serverless Kubernetes cluster.
-   CsClusterId: the ID of the Kubernetes cluster.
-   VSwitchId: the ID of the vSwitch.

## Examples

`JSON` format

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

`YAML` format

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


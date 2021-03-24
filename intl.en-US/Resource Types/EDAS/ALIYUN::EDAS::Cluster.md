# ALIYUN::EDAS::Cluster

ALIYUN::MSE::Cluster is used to create a cluster.

## Syntax

```
{
  "Type": "ALIYUN::EDAS::Cluster",
  "Properties": {
    "VpcId": String,
    "NetworkMode": Integer,
    "LogicalRegionId": String,
    "ClusterName": String,
    "ClusterType": Integer,
    "OversoldFactor": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|No|No|The VPC ID of the instance.|This parameter is required when the NetworkMode parameter is set to 2.|
|NetworkMode|Integer|Yes|No|The network type of the cluster.|Valid values: -   1: classic network
-   2: VPC |
|LogicalRegionId|String|No|No|The region ID of the custom namespace.|The region ID is in the format of `physical region:custom namespace identifier`.Example: `cn-beijing:prod`. |
|ClusterName|String|Yes|No|The name of the cluster.|The name must be 1 to 64 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\).|
|ClusterType|Integer|Yes|No|The type of the cluster.|Valid values: -   1: Swarm cluster
-   2: ECS cluster
-   3: Kubernetes cluster |
|OversoldFactor|Integer|No|No|The CPU overselling factor of the created cluster with Docker installed.|Valid values: -   2 \(1/2\)
-   4 \(1/4\)
-   8 \(1/8\) |

## Response parameters

Fn::GetAtt

-   ClusterName: the name of the cluster.
-   IaasProvider: the service provider
-   ClusterId: the ID of the cluster.
-   ClusterType: the type of the cluster.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Cluster": {
      "Type": "ALIYUN::EDAS::Cluster",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "NetworkMode": {
          "Ref": "NetworkMode"
        },
        "LogicalRegionId": {
          "Ref": "LogicalRegionId"
        },
        "ClusterName": {
          "Ref": "ClusterName"
        },
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "OversoldFactor": {
          "Ref": "OversoldFactor"
        }
      }
    }
  },
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "Description": "VPC network ID. If network selection VPC, this parameter Required"
    },
    "NetworkMode": {
      "Type": "Number",
      "Description": "Network Type. 1- classic network, 2-VPC"
    },
    "LogicalRegionId": {
      "Type": "String",
      "Description": "Custom namespace RegionId (format: Physical Region: custom namespace identifier)"
    },
    "ClusterName": {
      "Type": "String",
      "Description": "Cluster name"
    },
    "ClusterType": {
      "Type": "Number",
      "Description": "Cluster type. 1-Swarm cluster, 2-ECS cluster, 3-Kubernetes Cluster"
    },
    "OversoldFactor": {
      "Type": "Number",
      "Description": "Docker CPU cluster oversold. Support 2 (1: 2 ratio) / 4 (1: 4) / 8 (1: 8 ratio)",
      "AllowedValues": [
        2,
        4,
        8
      ]
    }
  },
  "Outputs": {
    "ClusterName": {
      "Description": "Cluster name",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "ClusterName"
        ]
      }
    },
    "IaasProvider": {
      "Description": "Provider",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "IaasProvider"
        ]
      }
    },
    "ClusterId": {
      "Description": "Cluster ID",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "ClusterId"
        ]
      }
    },
    "ClusterType": {
      "Description": "Cluster type",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "ClusterType"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Cluster:
    Type: 'ALIYUN::EDAS::Cluster'
    Properties:
      VpcId:
        Ref: VpcId
      NetworkMode:
        Ref: NetworkMode
      LogicalRegionId:
        Ref: LogicalRegionId
      ClusterName:
        Ref: ClusterName
      ClusterType:
        Ref: ClusterType
      OversoldFactor:
        Ref: OversoldFactor
Parameters:
  VpcId:
    Type: String
    Description: 'VPC network ID. If network selection VPC, this parameter Required'
  NetworkMode:
    Type: Number
    Description: 'Network Type. 1- classic network, 2-VPC'
  LogicalRegionId:
    Type: String
    Description: >-
      Custom namespace RegionId (format: Physical Region: custom namespace
      identifier)
  ClusterName:
    Type: String
    Description: Cluster name
  ClusterType:
    Type: Number
    Description: 'Cluster type. 1-Swarm cluster, 2-ECS cluster, 3-Kubernetes Cluster'
  OversoldFactor:
    Type: Number
    Description: >-
      Docker CPU cluster oversold. Support 2 (1: 2 ratio) / 4 (1: 4) / 8 (1: 8
      ratio)
    AllowedValues:
      - 2
      - 4
      - 8
Outputs:
  ClusterName:
    Description: Cluster name
    Value:
      'Fn::GetAtt':
        - Cluster
        - ClusterName
  IaasProvider:
    Description: Provider
    Value:
      'Fn::GetAtt':
        - Cluster
        - IaasProvider
  ClusterId:
    Description: Cluster ID
    Value:
      'Fn::GetAtt':
        - Cluster
        - ClusterId
  ClusterType:
    Description: Cluster type
    Value:
      'Fn::GetAtt':
        - Cluster
        - ClusterType
```


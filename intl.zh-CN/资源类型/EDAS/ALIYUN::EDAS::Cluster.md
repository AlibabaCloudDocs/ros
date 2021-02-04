# ALIYUN::EDAS::Cluster

ALIYUN::EDAS::Cluster类型用于创建集群。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|否|否|专有网络ID。|NetworkMode取值为2时，该参数必填。|
|NetworkMode|Integer|是|否|网络类型。|取值： -   1：经典网络。
-   2：专有网络。 |
|LogicalRegionId|String|否|否|自定义命名空间的地域ID。|格式：`物理Region:自定义命名空间标识符`。示例值：`cn-beijing:prod`。 |
|ClusterName|String|是|否|集群名称。|长度为1~64个字符，可包含英文字母、数字、下划线（\_）和英文句点（.）。|
|ClusterType|Integer|是|否|集群类型。|取值范围： -   1：Swarm集群。
-   2：ECS集群。
-   3：Kubernetes集群。 |
|OversoldFactor|Integer|否|否|Docker集群CPU超卖。|取值： -   2（1/2）
-   4（1/4）
-   8（1/8） |

## 返回值

Fn::GetAtt

-   ClusterName：集群名称。
-   IaasProvider：提供商。
-   ClusterId：集群ID。
-   ClusterType：集群类型。

## 示例

`JSON`格式

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

`YAML`格式

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


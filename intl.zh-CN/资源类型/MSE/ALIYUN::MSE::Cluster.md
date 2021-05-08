# ALIYUN::MSE::Cluster

ALIYUN::MSE::Cluster类型用于创建集群。

## 语法

```
{
  "Type": "ALIYUN::MSE::Cluster",
  "Properties": {
    "DiskType": String,
    "InstanceCount": Integer,
    "PrivateSlbSpecification": String,
    "VpcId": String,
    "ClusterVersion": String,
    "PubNetworkFlow": String,
    "ClusterSpecification": String,
    "VSwitchId": String,
    "PubSlbSpecification": String,
    "ClusterType": String,
    "NetType": String,
    "ClusterAliasName": String,
    "DiskCapacity": String,
    "ConnectionType": String,
    "RequestPars": String,
    "AclEntryList": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DiskType|String|否|否|磁盘类型。|取值：alicloud-disk-ssd-multi-zone。|
|InstanceCount|Integer|是|否|实例数。|取值范围：1~9。|
|PrivateSlbSpecification|String|否|否|私网SLB规格。|取值： -   slb.s1.small
-   slb.s3.medium |
|VpcId|String|否|否|专有网络ID。|无|
|ClusterVersion|String|是|否|集群版本。|取值： -   ZooKeeper\_3\_4\_14
-   ZooKeeper\_3\_5\_5
-   NACOS\_ANS\_1\_1\_3
-   EUREKA\_1\_9\_3 |
|PubNetworkFlow|String|否|否|公网带宽。|取值范围：0~5000。 单位：Mbps。

**说明：** 0表示不接入公网。 |
|ClusterSpecification|String|是|否|引擎规格。|取值： -   MSE\_SC\_1\_2\_200\_c：1核2 GB。
-   MSE\_SC\_2\_4\_200\_c：2核4 GB。
-   MSE\_SC\_4\_8\_200\_c：4核8 GB。
-   MSE\_SC\_8\_16\_200\_c：8核16 GB。 |
|VSwitchId|String|否|否|交换机ID。|无|
|PubSlbSpecification|String|否|否|公网SLB规格。|取值： -   slb.s1.small
-   slb.s3.medium |
|ClusterType|String|是|否|集群类型。|取值： -   ZooKeeper
-   Nacos-Ans
-   Eureka |
|NetType|String|是|否|网络类型。|取值： -   privatenet：专有网络。
-   pubnet：公网。 |
|ClusterAliasName|String|否|是|集群别名。|支持模糊匹配。|
|DiskCapacity|String|否|否|磁盘容量。|无|
|ConnectionType|String|否|否|网络连接类型。|无|
|RequestPars|String|否|否|扩展请求参数。|参数为JSON格式。|
|AclEntryList|List|否|是|白名单列表。|无|

## 返回值

Fn::GetAtt

-   InternetAddress：公网地址。
-   IntranetAddress：私网地址。
-   AclEntryList：白名单列表。
-   Cpu：CPU数量。
-   InternetPort：公网接口。
-   IntranetPort：私网接口。
-   DiskType：磁盘类型。
-   AppVersion：App版本。
-   PayInfo：付费类型。
-   ClusterName：集群名称。
-   IntranetDomain：内网域名。
-   NetType：网络类型。
-   ClusterVersion：集群版本。
-   InstanceId：实例ID。
-   ClusterId：集群ID。
-   InternetDomain：公网域名。
-   AclId：访问控制列表ID。
-   VSwitchId：交换机ID。
-   ClusterSpecification：引擎规格。
-   HealthStatus：健康状态。
-   MemoryCapacity：内存容量。
-   ClusterType：集群类型。
-   ClusterAliasName：集群别名。
-   InstanceCount：实例数量。
-   DiskCapacity：磁盘容量。
-   VpcId：专有网络ID。
-   PubNetworkFlow：公网带宽。
-   ConnectionType：网络连接类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PrivateSlbSpecification": {
      "Type": "String",
      "Description": ""
    },
    "ClusterVersion": {
      "Type": "String",
      "Description": "cluster version, Enum: ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3"
    },
    "ConnectionType": {
      "Type": "String",
      "Description": "network connect type"
    },
    "AclEntryList": {
      "Type": "Json",
      "Description": "acl entry list"
    },
    "ClusterSpecification": {
      "Type": "String",
      "Description": "cluster specification, Enum: MSE_SC_1_2_200_c,MSE_SC_2_4_200_c,MSE_SC_4_8_200_c,MSE_SC_8_16_200_c"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "switcher Id"
    },
    "PubSlbSpecification": {
      "Type": "String",
      "Description": ""
    },
    "ClusterType": {
      "Type": "String",
      "Description": "cluster type"
    },
    "DiskType": {
      "Type": "String",
      "Description": "disk type"
    },
    "ClusterAliasName": {
      "Type": "String",
      "Description": "cluster alias name"
    },
    "InstanceCount": {
      "Type": "Number",
      "Description": "instance count"
    },
    "DiskCapacity": {
      "Type": "String",
      "Description": ""
    },
    "VpcId": {
      "Type": "String",
      "Description": "vpc id"
    },
    "RequestPars": {
      "Type": "String",
      "Description": ""
    },
    "PubNetworkFlow": {
      "Type": "String",
      "Description": "pub network flow"
    },
    "NetType": {
      "Type": "String",
      "Description": "network type, Enum: privatenet,pubnet"
    }
  },
  "Resources": {
    "MSECluster": {
      "Type": "ALIYUN::MSE::Cluster",
      "Properties": {
        "PrivateSlbSpecification": {
          "Ref": "PrivateSlbSpecification"
        },
        "ClusterVersion": {
          "Ref": "ClusterVersion"
        },
        "ConnectionType": {
          "Ref": "ConnectionType"
        },
        "AclEntryList": {
          "Ref": "AclEntryList"
        },
        "ClusterSpecification": {
          "Ref": "ClusterSpecification"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "PubSlbSpecification": {
          "Ref": "PubSlbSpecification"
        },
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "DiskType": {
          "Ref": "DiskType"
        },
        "ClusterAliasName": {
          "Ref": "ClusterAliasName"
        },
        "InstanceCount": {
          "Ref": "InstanceCount"
        },
        "DiskCapacity": {
          "Ref": "DiskCapacity"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "RequestPars": {
          "Ref": "RequestPars"
        },
        "PubNetworkFlow": {
          "Ref": "PubNetworkFlow"
        },
        "NetType": {
          "Ref": "NetType"
        }
      }
    }
  },
  "Outputs": {
    "InternetAddress": {
      "Description": "internet address",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "InternetAddress"
        ]
      }
    },
    "AclEntryList": {
      "Description": "acl entry list",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "AclEntryList"
        ]
      }
    },
    "Cpu": {
      "Description": "cpu core size",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "Cpu"
        ]
      }
    },
    "InternetPort": {
      "Description": "internet port",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "InternetPort"
        ]
      }
    },
    "IntranetPort": {
      "Description": "intranet port",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "IntranetPort"
        ]
      }
    },
    "DiskType": {
      "Description": "disk type",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "DiskType"
        ]
      }
    },
    "AppVersion": {
      "Description": "app version",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "AppVersion"
        ]
      }
    },
    "PayInfo": {
      "Description": "pay info",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "PayInfo"
        ]
      }
    },
    "ClusterName": {
      "Description": "cluster name",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ClusterName"
        ]
      }
    },
    "IntranetDomain": {
      "Description": "intranet domain",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "IntranetDomain"
        ]
      }
    },
    "NetType": {
      "Description": "network type, Enum: privatenet,pubnet",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "NetType"
        ]
      }
    },
    "ClusterVersion": {
      "Description": "cluster version, Enum: ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ClusterVersion"
        ]
      }
    },
    "ConnectionType": {
      "Description": "network connect type",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ConnectionType"
        ]
      }
    },
    "InstanceId": {
      "Description": "instance id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "InstanceId"
        ]
      }
    },
    "ClusterId": {
      "Description": "cluster id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ClusterId"
        ]
      }
    },
    "InternetDomain": {
      "Description": "internet domain",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "InternetDomain"
        ]
      }
    },
    "AclId": {
      "Description": "acl id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "AclId"
        ]
      }
    },
    "ClusterSpecification": {
      "Description": "cluster specification, Enum: MSE_SC_1_2_200_c,MSE_SC_2_4_200_c,MSE_SC_4_8_200_c,MSE_SC_8_16_200_c",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ClusterSpecification"
        ]
      }
    },
    "VSwitchId": {
      "Description": "switcher Id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "VSwitchId"
        ]
      }
    },
    "HealthStatus": {
      "Description": "health status",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "HealthStatus"
        ]
      }
    },
    "MemoryCapacity": {
      "Description": "memory capacity",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "MemoryCapacity"
        ]
      }
    },
    "ClusterType": {
      "Description": "cluster type",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ClusterType"
        ]
      }
    },
    "ClusterAliasName": {
      "Description": "cluster alias name",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "ClusterAliasName"
        ]
      }
    },
    "InstanceCount": {
      "Description": "instance count",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "InstanceCount"
        ]
      }
    },
    "IntranetAddress": {
      "Description": "intranet address",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "IntranetAddress"
        ]
      }
    },
    "DiskCapacity": {
      "Description": "disk capacity, unit: G",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "DiskCapacity"
        ]
      }
    },
    "VpcId": {
      "Description": "vpc id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "VpcId"
        ]
      }
    },
    "PubNetworkFlow": {
      "Description": "pub network flow",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "PubNetworkFlow"
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
  AclEntryList:
    Description: acl entry list
    Type: Json
  ClusterAliasName:
    Description: cluster alias name
    Type: String
  ClusterSpecification:
    Description: 'cluster specification, Enum: MSE_SC_1_2_200_c,MSE_SC_2_4_200_c,MSE_SC_4_8_200_c,MSE_SC_8_16_200_c'
    Type: String
  ClusterType:
    Description: cluster type
    Type: String
  ClusterVersion:
    Description: 'cluster version, Enum: ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3'
    Type: String
  ConnectionType:
    Description: network connect type
    Type: String
  DiskCapacity:
    Description: ''
    Type: String
  DiskType:
    Description: disk type
    Type: String
  InstanceCount:
    Description: instance count
    Type: Number
  NetType:
    Description: 'network type, Enum: privatenet,pubnet'
    Type: String
  PrivateSlbSpecification:
    Description: ''
    Type: String
  PubNetworkFlow:
    Description: pub network flow
    Type: String
  PubSlbSpecification:
    Description: ''
    Type: String
  RequestPars:
    Description: ''
    Type: String
  VSwitchId:
    Description: switcher Id
    Type: String
  VpcId:
    Description: vpc id
    Type: String
Resources:
  MSECluster:
    Properties:
      AclEntryList:
        Ref: AclEntryList
      ClusterAliasName:
        Ref: ClusterAliasName
      ClusterSpecification:
        Ref: ClusterSpecification
      ClusterType:
        Ref: ClusterType
      ClusterVersion:
        Ref: ClusterVersion
      ConnectionType:
        Ref: ConnectionType
      DiskCapacity:
        Ref: DiskCapacity
      DiskType:
        Ref: DiskType
      InstanceCount:
        Ref: InstanceCount
      NetType:
        Ref: NetType
      PrivateSlbSpecification:
        Ref: PrivateSlbSpecification
      PubNetworkFlow:
        Ref: PubNetworkFlow
      PubSlbSpecification:
        Ref: PubSlbSpecification
      RequestPars:
        Ref: RequestPars
      VSwitchId:
        Ref: VSwitchId
      VpcId:
        Ref: VpcId
    Type: ALIYUN::MSE::Cluster
Outputs:
  AclEntryList:
    Description: acl entry list
    Value:
      Fn::GetAtt:
      - MSECluster
      - AclEntryList
  AclId:
    Description: acl id
    Value:
      Fn::GetAtt:
      - MSECluster
      - AclId
  AppVersion:
    Description: app version
    Value:
      Fn::GetAtt:
      - MSECluster
      - AppVersion
  ClusterAliasName:
    Description: cluster alias name
    Value:
      Fn::GetAtt:
      - MSECluster
      - ClusterAliasName
  ClusterId:
    Description: cluster id
    Value:
      Fn::GetAtt:
      - MSECluster
      - ClusterId
  ClusterName:
    Description: cluster name
    Value:
      Fn::GetAtt:
      - MSECluster
      - ClusterName
  ClusterSpecification:
    Description: 'cluster specification, Enum: MSE_SC_1_2_200_c,MSE_SC_2_4_200_c,MSE_SC_4_8_200_c,MSE_SC_8_16_200_c'
    Value:
      Fn::GetAtt:
      - MSECluster
      - ClusterSpecification
  ClusterType:
    Description: cluster type
    Value:
      Fn::GetAtt:
      - MSECluster
      - ClusterType
  ClusterVersion:
    Description: 'cluster version, Enum: ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3'
    Value:
      Fn::GetAtt:
      - MSECluster
      - ClusterVersion
  ConnectionType:
    Description: network connect type
    Value:
      Fn::GetAtt:
      - MSECluster
      - ConnectionType
  Cpu:
    Description: cpu core size
    Value:
      Fn::GetAtt:
      - MSECluster
      - Cpu
  DiskCapacity:
    Description: 'disk capacity, unit: G'
    Value:
      Fn::GetAtt:
      - MSECluster
      - DiskCapacity
  DiskType:
    Description: disk type
    Value:
      Fn::GetAtt:
      - MSECluster
      - DiskType
  HealthStatus:
    Description: health status
    Value:
      Fn::GetAtt:
      - MSECluster
      - HealthStatus
  InstanceCount:
    Description: instance count
    Value:
      Fn::GetAtt:
      - MSECluster
      - InstanceCount
  InstanceId:
    Description: instance id
    Value:
      Fn::GetAtt:
      - MSECluster
      - InstanceId
  InternetAddress:
    Description: internet address
    Value:
      Fn::GetAtt:
      - MSECluster
      - InternetAddress
  InternetDomain:
    Description: internet domain
    Value:
      Fn::GetAtt:
      - MSECluster
      - InternetDomain
  InternetPort:
    Description: internet port
    Value:
      Fn::GetAtt:
      - MSECluster
      - InternetPort
  IntranetAddress:
    Description: intranet address
    Value:
      Fn::GetAtt:
      - MSECluster
      - IntranetAddress
  IntranetDomain:
    Description: intranet domain
    Value:
      Fn::GetAtt:
      - MSECluster
      - IntranetDomain
  IntranetPort:
    Description: intranet port
    Value:
      Fn::GetAtt:
      - MSECluster
      - IntranetPort
  MemoryCapacity:
    Description: memory capacity
    Value:
      Fn::GetAtt:
      - MSECluster
      - MemoryCapacity
  NetType:
    Description: 'network type, Enum: privatenet,pubnet'
    Value:
      Fn::GetAtt:
      - MSECluster
      - NetType
  PayInfo:
    Description: pay info
    Value:
      Fn::GetAtt:
      - MSECluster
      - PayInfo
  PubNetworkFlow:
    Description: pub network flow
    Value:
      Fn::GetAtt:
      - MSECluster
      - PubNetworkFlow
  VSwitchId:
    Description: switcher Id
    Value:
      Fn::GetAtt:
      - MSECluster
      - VSwitchId
  VpcId:
    Description: vpc id
    Value:
      Fn::GetAtt:
      - MSECluster
      - VpcId
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MSE/JSON/Cluster.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MSE/YAML/Cluster.yml)。


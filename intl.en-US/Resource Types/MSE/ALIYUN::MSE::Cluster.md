# ALIYUN::MSE::Cluster

ALIYUN::MSE::Cluster is used to create a cluster.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DiskType|String|No|No|The type of the disk.|Set the value to alicloud-disk-ssd-multi-zone.|
|InstanceCount|Integer|Yes|No|The number of instances.|Valid values: 1 to 9.|
|PrivateSlbSpecification|String|No|No|The instance type of the internal-facing Server Load Balancer \(SLB\) instance.|Valid values: -   slb.s1.small
-   slb.s3.medium |
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\).|None|
|ClusterVersion|String|Yes|No|The version of the cluster.|Valid values: -   ZooKeeper\_3\_4\_14
-   ZooKeeper\_3\_5\_5
-   NACOS\_ANS\_1\_1\_3
-   EUREKA\_1\_9\_3 |
|PubNetworkFlow|String|No|No|The public bandwidth.|Valid values: 0 to 5000. Unit: Mbit/s.

**Note:** A value of 0 indicates that the instance is not connected to the Internet. |
|ClusterSpecification|String|Yes|No|The specifications of the engine.|Valid values: -   MSE\_SC\_1\_2\_200\_c: 1 CPU core and 2 GB memory
-   MSE\_SC\_2\_4\_200\_c: 2 CPU cores and 4 GB memory
-   MSE\_SC\_4\_8\_200\_c: 4 CPU cores and 8 GB memory
-   MSE\_SC\_8\_16\_200\_c: 8 CPU cores and 16 GB memory |
|VSwitchId|String|No|No|The ID of the vSwitch.|None|
|PubSlbSpecification|String|No|No|The instance type of the Internet-facing SLB instance.|Valid values: -   slb.s1.small
-   slb.s3.medium |
|ClusterType|String|Yes|No|The type of the cluster.|Valid values: -   ZooKeeper
-   Nacos-Ans
-   Eureka |
|NetType|String|Yes|No|The network type of the cluster.|Valid values: -   privatenet: VPC
-   pubnet: Internet |
|ClusterAliasName|String|No|Yes|The alias of the cluster.|Fuzzy match is supported.|
|DiskCapacity|String|No|No|The size of the disk.|None|
|ConnectionType|String|No|No|The network connection type of the cluster.|None|
|RequestPars|String|No|No|The extended request parameters.|The format must be JSON.|
|AclEntryList|List|No|Yes|The list of IP addresses in the whitelist.|None|

## Response parameters

Fn::GetAtt

-   InternetAddress: the public IP address.
-   IntranetAddress: the internal IP address.
-   AclEntryList: the whitelist.
-   Cpu: the number of CPU cores.
-   InternetPort: the public port.
-   IntranetPort: the internal port.
-   DiskType: the disk type.
-   AppVersion: the app version.
-   PayInfo: the billing method.
-   ClusterName: the name of the cluster.
-   IntranetDomain: the internal domain name.
-   NetType: the network type.
-   ClusterVersion: the cluster version.
-   InstanceId: the ID of the instance.
-   ClusterId: the ID of the cluster.
-   InternetDomain: the public domain name.
-   AclId: the ID of the access control list \(ACL\).
-   VSwitchId: the ID of the vSwitch.
-   ClusterSpecification: the specifications of the engine.
-   HealthStatus: the health status.
-   MemoryCapacity: the memory capacity.
-   ClusterType: the type of the cluster.
-   ClusterAliasName: the alias of the cluster.
-   InstanceCount: the number of instances.
-   DiskCapacity: the disk capacity.
-   VpcId: the ID of the VPC.
-   PubNetworkFlow: the public bandwidth.
-   ConnectionType: the network connection type of the cluster.

## Examples

`JSON` format

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

`YAML` format

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

To view more examples, visit [Cluster.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MSE/JSON/Cluster.json) and [Cluster.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MSE/YAML/Cluster.yml).


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
    "NetType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DiskType|String|No|No|The type of the disk.|Set the value to alicloud-disk-ssd-multi-zone.|
|InstanceCount|Integer|Yes|No|The number of instances.|Valid values: 1 to 5.|
|PrivateSlbSpecification|String|No|No|The instance type of the internal SLB instance.|Valid values: -   slb.s1.small
-   slb.s3.medium |
|VpcId|String|No|No|The ID of the VPC.|None|
|ClusterVersion|String|Yes|No|The version of the cluster.|Valid values: -   ZooKeeper\_3\_4\_14
-   NACOS\_ANS\_1\_1\_3
-   EUREKA\_1\_9\_3 |
|PubNetworkFlow|String|No|No|The public bandwidth.|Valid values: 0 to 5000. Unit: Mbit/s.

**Note:** A value of 0 indicates that the instance is not connected to the Internet. |
|ClusterSpecification|String|Yes|No|The specifications of the engine.|Valid values: -   MSE\_SC\_1\_2\_200\_c: 1 CPU and 2 GB memory
-   MSE\_SC\_2\_4\_200\_c: 2 CPUs and 4 GB memory
-   MSE\_SC\_4\_8\_200\_c: 4 CPUs and 8 GB memory
-   MSE\_SC\_8\_16\_200\_c: 8 CPUs and 16 GB memory |
|VSwitchId|String|No|No|The ID of the vSwitch.|None|
|PubSlbSpecification|String|No|No|The instance type of the public SLB instance.|Valid values: -   slb.s1.small
-   slb.s3.medium |
|ClusterType|String|Yes|No|The type of the cluster.|Valid values: -   ZooKeeper
-   Nacos-Ans
-   Eureka |
|NetType|String|Yes|No|The network type of the cluster.|Valid values: -   privatenet: VPC
-   pubnet: Internet |

## Response parameters

Fn::GetAtt

-   InternetAddress: the public IP address.
-   IntranetAddress: the private IP address.
-   AclEntryList: the whitelist.
-   Cpu: the number of CPUs.
-   InternetPort: the Internet port.
-   IntranetPort: the private port.
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
-   AclId: the ID of the ACL.
-   VSwitchId: the ID of the vSwitch.
-   ClusterSpecification: the specifications of the engine.
-   HealthStatus: the health status.
-   MemoryCapacity: the memory capacity.
-   ClusterType: the type of the cluster.
-   OrderId: the ID of the order.
-   ClusterAliasName: the alias of the cluster.
-   InstanceCount: the number of instances.
-   DiskCapacity: the disk capacity.
-   VpcId: the ID of the VPC.
-   PubNetworkFlow: the public bandwidth.
-   RegionId: the region ID.
-   InitStatus: the creation status of the cluster.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DiskType": {
      "Type": "String",
      "Description": "disk type"
    },
    "PrivateSlbSpecification": {
      "Type": "String",
      "Description": ""
    },
    "InstanceCount": {
      "Type": "Number",
      "Description": "instance count"
    },
    "VpcId": {
      "Type": "String",
      "Description": "vpc id"
    },
    "ClusterVersion": {
      "Type": "String",
      "Description": "cluster version, Enum: ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3"
    },
    "PubNetworkFlow": {
      "Type": "String",
      "Description": "pub network flow"
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
    "NetType": {
      "Type": "String",
      "Description": "network type, Enum: privatenet,pubnet"
    }
  },
  "Resources": {
    "MSECluster": {
      "Type": "ALIYUN::MSE::Cluster",
      "Properties": {
        "DiskType": {
          "Ref": "DiskType"
        },
        "PrivateSlbSpecification": {
          "Ref": "PrivateSlbSpecification"
        },
        "InstanceCount": {
          "Ref": "InstanceCount"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "ClusterVersion": {
          "Ref": "ClusterVersion"
        },
        "PubNetworkFlow": {
          "Ref": "PubNetworkFlow"
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
    "VSwitchId": {
      "Description": "switcher Id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "VSwitchId"
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
    "OrderId": {
      "Description": "order id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "OrderId"
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
    },
    "RegionId": {
      "Description": "region id",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "RegionId"
        ]
      }
    },
    "InitStatus": {
      "Description": "init status, Enum: INIT_ING, INIT_FAILED, INIT_SUCCESS, INIT_TIME_OUT,DESTROY_ING, DESTROY_FAILED, DESTROY_SUCCESS, RESTART_ING, RESTART_SUCCESS, RESTART_FAILED, SCALE_ING, SCALE_SUCCESS, SCALE_FAILED",
      "Value": {
        "Fn::GetAtt": [
          "MSECluster",
          "InitStatus"
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
  DiskType:
    Type: String
    Description: disk type
  PrivateSlbSpecification:
    Type: String
    Description: ''
  InstanceCount:
    Type: Number
    Description: instance count
  VpcId:
    Type: String
    Description: vpc id
  ClusterVersion:
    Type: String
    Description: >-
      cluster version, Enum:
      ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3
  PubNetworkFlow:
    Type: String
    Description: pub network flow
  ClusterSpecification:
    Type: String
    Description: >-
      cluster specification, Enum:
      MSE_SC_1_2_200_c,MSE_SC_2_4_200_c,MSE_SC_4_8_200_c,MSE_SC_8_16_200_c
  VSwitchId:
    Type: String
    Description: switcher Id
  PubSlbSpecification:
    Type: String
    Description: ''
  ClusterType:
    Type: String
    Description: cluster type
  NetType:
    Type: String
    Description: 'network type, Enum: privatenet,pubnet'
Resources:
  MSECluster:
    Type: 'ALIYUN::MSE::Cluster'
    Properties:
      DiskType:
        Ref: DiskType
      PrivateSlbSpecification:
        Ref: PrivateSlbSpecification
      InstanceCount:
        Ref: InstanceCount
      VpcId:
        Ref: VpcId
      ClusterVersion:
        Ref: ClusterVersion
      PubNetworkFlow:
        Ref: PubNetworkFlow
      ClusterSpecification:
        Ref: ClusterSpecification
      VSwitchId:
        Ref: VSwitchId
      PubSlbSpecification:
        Ref: PubSlbSpecification
      ClusterType:
        Ref: ClusterType
      NetType:
        Ref: NetType
Outputs:
  InternetAddress:
    Description: internet address
    Value:
      'Fn::GetAtt':
        - MSECluster
        - InternetAddress
  AclEntryList:
    Description: acl entry list
    Value:
      'Fn::GetAtt':
        - MSECluster
        - AclEntryList
  Cpu:
    Description: cpu core size
    Value:
      'Fn::GetAtt':
        - MSECluster
        - Cpu
  InternetPort:
    Description: internet port
    Value:
      'Fn::GetAtt':
        - MSECluster
        - InternetPort
  IntranetPort:
    Description: intranet port
    Value:
      'Fn::GetAtt':
        - MSECluster
        - IntranetPort
  DiskType:
    Description: disk type
    Value:
      'Fn::GetAtt':
        - MSECluster
        - DiskType
  AppVersion:
    Description: app version
    Value:
      'Fn::GetAtt':
        - MSECluster
        - AppVersion
  PayInfo:
    Description: pay info
    Value:
      'Fn::GetAtt':
        - MSECluster
        - PayInfo
  ClusterName:
    Description: cluster name
    Value:
      'Fn::GetAtt':
        - MSECluster
        - ClusterName
  IntranetDomain:
    Description: intranet domain
    Value:
      'Fn::GetAtt':
        - MSECluster
        - IntranetDomain
  NetType:
    Description: 'network type, Enum: privatenet,pubnet'
    Value:
      'Fn::GetAtt':
        - MSECluster
        - NetType
  ClusterVersion:
    Description: >-
      cluster version, Enum:
      ZooKeeper_3_4_14,ZooKeeper_3_5_5,NACOS_ANS_1_1_3,EUREKA_1_9_3
    Value:
      'Fn::GetAtt':
        - MSECluster
        - ClusterVersion
  InstanceId:
    Description: instance id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - InstanceId
  ClusterId:
    Description: cluster id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - ClusterId
  InternetDomain:
    Description: internet domain
    Value:
      'Fn::GetAtt':
        - MSECluster
        - InternetDomain
  AclId:
    Description: acl id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - AclId
  VSwitchId:
    Description: switcher Id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - VSwitchId
  ClusterSpecification:
    Description: >-
      cluster specification, Enum:
      MSE_SC_1_2_200_c,MSE_SC_2_4_200_c,MSE_SC_4_8_200_c,MSE_SC_8_16_200_c
    Value:
      'Fn::GetAtt':
        - MSECluster
        - ClusterSpecification
  HealthStatus:
    Description: health status
    Value:
      'Fn::GetAtt':
        - MSECluster
        - HealthStatus
  MemoryCapacity:
    Description: memory capacity
    Value:
      'Fn::GetAtt':
        - MSECluster
        - MemoryCapacity
  ClusterType:
    Description: cluster type
    Value:
      'Fn::GetAtt':
        - MSECluster
        - ClusterType
  OrderId:
    Description: order id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - OrderId
  ClusterAliasName:
    Description: cluster alias name
    Value:
      'Fn::GetAtt':
        - MSECluster
        - ClusterAliasName
  InstanceCount:
    Description: instance count
    Value:
      'Fn::GetAtt':
        - MSECluster
        - InstanceCount
  IntranetAddress:
    Description: intranet address
    Value:
      'Fn::GetAtt':
        - MSECluster
        - IntranetAddress
  DiskCapacity:
    Description: 'disk capacity, unit: G'
    Value:
      'Fn::GetAtt':
        - MSECluster
        - DiskCapacity
  VpcId:
    Description: vpc id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - VpcId
  PubNetworkFlow:
    Description: pub network flow
    Value:
      'Fn::GetAtt':
        - MSECluster
        - PubNetworkFlow
  RegionId:
    Description: region id
    Value:
      'Fn::GetAtt':
        - MSECluster
        - RegionId
  InitStatus:
    Description: >-
      init status, Enum: INIT_ING, INIT_FAILED, INIT_SUCCESS,
      INIT_TIME_OUT,DESTROY_ING, DESTROY_FAILED, DESTROY_SUCCESS, RESTART_ING,
      RESTART_SUCCESS, RESTART_FAILED, SCALE_ING, SCALE_SUCCESS, SCALE_FAILED
    Value:
      'Fn::GetAtt':
        - MSECluster
        - InitStatus
```


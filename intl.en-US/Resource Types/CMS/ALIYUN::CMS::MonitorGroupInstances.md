# ALIYUN::CMS::MonitorGroupInstances

ALIYUN::CMS::MonitorGroupInstances is used to add instances to an application group.

## Syntax

```
{
  "Type": "ALIYUN::CMS::MonitorGroupInstances",
  "Properties": {
    "Instances": List,
    "GroupId": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Instances|List|Yes|No|The instances.|For more information, see [Instances properties](#section_wzx_r0l_4fx).|
|GroupId|Integer|Yes|No|The ID of the application group.|None|

## Instances syntax

```
"Instances": [
  {
    "InstanceName": String,
    "Category": String,
    "InstanceId": String,
    "RegionId": String
  }
]
```

## Instances properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceName|String|Yes|No|The name of the instance.|None|
|Category|String|Yes|No|The name and specifications of the cloud service to which the instance belongs.|Valid values:-   ecs: Elastic Compute Service
-   rds: ApsaraDB for RDS
-   ads: AnalyticDB for MySQL
-   slb: Server Load Balancer
-   vpc: Virtual Private Cloud
-   apigateway: API Gateway
-   cdn: Alibaba Cloud CDN
-   cs: Alibaba Cloud Container Service for Kubernetes \(ACK\)
-   dcdn: Dynamic Route for CDN
-   ddos: Anti-DDoS Pro
-   eip: Elastic IP Address
-   elasticsearch: Elasticsearch
-   emr: E-MapReduce
-   ess: Auto Scaling
-   hbase: ApsaraDB for Hbase
-   iot\_edge: IoT Edge
-   k8s\_pod: pods in ACK
-   kvstore\_sharding: ApsaraDB for Redis of the cluster architecture
-   kvstore\_splitrw: ApsaraDB for Redis of the read/write splitting architecture
-   kvstore\_standard: ApsaraDB for Redis of the standard architecture
-   memcache: ApsaraDB for Memcache
-   mns: Message Service
-   mongodb: ApsaraDB for MongoDB of the replica set architecture
-   mongodb\_cluster: ApsaraDB for MongoDB of the cluster architecture
-   mongodb\_sharding: ApsaraDB for MongoDB of the sharded cluster architecture
-   mq\_topic: MNS topics
-   ocs: ApsaraDB for Memcache
-   opensearch: Open Search
-   oss: Object Storage Service
-   polardb: PolarDB
-   petadata: HybridDB for MySQL
-   scdn: Secure Content Delivery Network
-   sharebandwidthpackages: EIP Bandwidth Plan
-   sls: Log Service
-   vpn: VPN Gateway |
|InstanceId|String|Yes|No|The ID of the instance.|None|
|RegionId|String|Yes|No|The region ID of the instance.|None|

## Response parameters

Fn::GetAtt

GroupId: the ID of the application group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Instances": {
      "Type": "Json"
    },
    "GroupId": {
      "Type": "Number",
      "Description": "The ID of the application group."
    }
  },
  "Resources": {
    "MonitorGroupInstances": {
      "Type": "ALIYUN::CMS::MonitorGroupInstances",
      "Properties": {
        "Instances": {
          "Ref": "Instances"
        },
        "GroupId": {
          "Ref": "GroupId"
        }
      }
    }
  },
  "Outputs": {
    "GroupId": {
      "Description": "The ID of the application group.",
      "Value": {
        "Fn::GetAtt": [
          "MonitorGroupInstances",
          "GroupId"
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
  Instances:
    Type: Json
  GroupId:
    Type: Number
    Description: The ID of the application group.
Resources:
  MonitorGroupInstances:
    Type: 'ALIYUN::CMS::MonitorGroupInstances'
    Properties:
      Instances:
        Ref: Instances
      GroupId:
        Ref: GroupId
Outputs:
  GroupId:
    Description: The ID of the application group.
    Value:
      'Fn::GetAtt':
        - MonitorGroupInstances
        - GroupId
```


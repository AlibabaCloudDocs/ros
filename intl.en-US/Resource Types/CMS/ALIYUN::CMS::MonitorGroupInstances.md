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
|Instances|List|Yes|No|The list of one or more instances.|For more information, see the [Instances properties](#section_wzx_r0l_4fx) section.|
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
|Category|String|Yes|No|The name and specifications of the service to which the instance in the application group belongs.|Valid values:-   ecs: Elastic Compute Service \(ECS\)
-   rds: ApsaraDB RDS
-   ads: AnalyticDB for MySQL
-   slb: Server Load Balancer \(SLB\)
-   vpc: Virtual Private Cloud \(VPC\)
-   apigateway: API Gateway
-   cdn: Alibaba Cloud CDN \(CDN\)
-   cs: Container Service for Kubernetes \(ACK\)
-   dcdn: Dynamic Route for CDN \(DCDN\)
-   ddos: Anti-DDoS Pro and Anti-DDoS Premium
-   eip: Elastic IP Address \(EIP\)
-   elasticsearch: Elasticsearch
-   emr: E-MapReduce \(EMR\)
-   ess: Auto Scaling \(ESS\)
-   hbase: ApsaraDB for HBase
-   iot\_edge: IoT Edge
-   k8s\_pod: pods in ACK
-   kvstore\_sharding: ApsaraDB for Redis that uses the cluster master-replica architecture
-   kvstore\_splitrw: ApsaraDB for Redis that uses the read/write splitting architecture
-   kvstore\_standard: ApsaraDB for Redis that uses the standard master-replica architecture
-   memcache: ApsaraDB for Memcache
-   mns: Message Service \(MNS\)
-   mongodb: ApsaraDB for MongoDB that uses the replica set architecture
-   mongodb\_cluster: ApsaraDB for MongoDB that uses the standalone architecture
-   mongodb\_sharding: ApsaraDB for MongoDB that uses the sharded cluster architecture
-   mq\_topic: MNS topics
-   ocs: ApsaraDB for Memcache \(OCS\)
-   opensearch: Open Search
-   oss: Object Storage Service \(OSS\)
-   polardb: PolarDB
-   petadata: HybridDB for MySQL
-   scdn: Secure CDN \(SCDN\)
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


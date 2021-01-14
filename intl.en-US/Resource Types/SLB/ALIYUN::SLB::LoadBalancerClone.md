# ALIYUN::SLB::LoadBalancerClone

ALIYUN::SLB::LoadBalancerClone is used to clone an SLB instance.

## Syntax

```
{
  "Type": "ALIYUN::SLB::LoadBalancerClone",
  "Properties": {
    "Tags": List,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "LoadBalancerName": String,
    "SourceLoadBalancerId": String,
    "TagsPolicy": String,
    "BackendServersPolicy": String,
    "BackendServers": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the SLB instance belongs.|None.|
|VSwitchId|String|No|No|The ID of the VSwitch.|The VSwitch must be in the same VPC as the source SLB instance. If you do not specify this parameter, the VSwitch of the source SLB instance is used.|
|SourceLoadBalancerId|String|Yes|No|The ID of the SLB instance to be cloned.|None.|
|BackendServersPolicy|String|No|No|The clone policy, which specifies the ECS instances listened by the new SLB instance and the weight of each ECS instance.|Default value: clone. Valid values: -   clone: The ECS instances listened by the source SLB instance and the weight of each ECS instance are cloned to the new SLB instance.
-   empty: No ECS instances are attached to the new SLB instance.
-   append: The ECS instances listened by the source SLB instance and the weight of each ECS instance are cloned to the new SLB instance. New ECS instances that have weights specified are also attached to the new SLB instance.
-   replace: New ECS instances that have weights specified are attached to the new SLB instance. However, the ECS instances listened by the source SLB instance and the weight of each ECS instance are not cloned to the new SLB instance. |
|BackendServers|List|No|Yes|The list of new ECS instances to be listened.|For more information, see [BackendServers properties](#section_3xt_cew_nfq).|
|LoadBalancerName|String|No|No|The name of the new SLB instance.|You can customize the instance name. The name must be 1 to 80 characters in length, and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\).|
|Tags|List|No|Yes|The list of tags to be bound to the SLB instance.|Tags must be specified as key-value pairs. A maximum of five tags can be specified.For more information, see [Tags properties](#section_yi0_9mi_nsy). |
|TagsPolicy|String|No|No|The policy for handling tags.|Default value: empty. Valid values: -   clone: The tags of the source SLB instance are used.
-   empty: No tags are configured.
-   append: The tags of the source SLB instance are reserved while new tags are added.
-   replace: The tags of the source SLB instance are deleted while new tags are added. |

## BackendServers syntax

```
"BackendServers": [
  {
    "Type": String,
    "ServerId": String,
    "Description": String,
    "ServerIp": String,
    "Weight": Integer
  }
] 
```

## BackendServers properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServerId|String|Yes|Yes|The ID of the backend server.|Only ECS instances in the running state can be attached to the SLB instance as backend servers. A maximum of 20 backend servers can be attached each time.You can specify elastic network interfaces \(ENIs\) as the backend servers for only guaranteed-performance SLB instances. |
|Weight|Integer|Yes|Yes|The weight of the ECS instance to be attached to the SLB instance.|Valid values: 0 to 100. Default value: 100. |
|ServerIp|String|No|No|The IP address of the backend server.|None.|
|Type|String|No|No|The type of the backend server.|Default value: ecs. Valid values: -   ecs: ECS instance
-   eni: ENI
-   eci: Elastic Container Instance \(ECI\) |
|Description|String|No|Yes|The description of the backend server.|The description must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\).|

## Tags syntax

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

LoadBalancerId: the ID of the new SLB instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "LoadBalancerName": {
      "Type": "String",
      "Description": "Name of created load balancer. Length is limited to 1-80 characters, allowed to contain letters, numbers, '-, /, _,.' When not specified, a default name will be assigned."
    },
    "SourceLoadBalancerId": {
      "Type": "String",
      "Description": "Source load balancer id to clone"
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "TagsPolicy": {
      "Type": "String",
      "Description": "Solution for handle the tags. If select 'clone', it will clone from source load balancer. If select 'empty' it will not coppy tags. If select 'append' it will append the new tags. If select 'replace' it will add new tags.\nDefault is 'empty'. ",
      "AllowedValues": [
        "clone",
        "empty",
        "append",
        "replace"
      ],
      "Default": "empty"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The new VSwitch ID to create load balancer instance. For VPC network only and the VSwitch should belong to the VPC which source load balancer is located. When not specified, source load balancer VSwitch ID will be used."
    },
    "BackendServers": {
      "Type": "Json",
      "Description": "The list of ECS instance, which will attached to load balancer."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to slb. Max support 5 tags to add during create slb. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 5
    },
    "BackendServersPolicy": {
      "Type": "String",
      "Description": "Solution for handle the backend server and weights. If select 'clone', it will clone from source load balancer. If select 'empty' it will not attach any backend servers. If select 'append' it will append the new backend server list to source backed servers. If select 'replace' it will only attach new backend server list. Default is 'clone'. ",
      "AllowedValues": [
        "clone",
        "empty",
        "append",
        "replace"
      ],
      "Default": "clone"
    }
  },
  "Resources": {
    "LoadBalancerClone": {
      "Type": "ALIYUN::SLB::LoadBalancerClone",
      "Properties": {
        "LoadBalancerName": {
          "Ref": "LoadBalancerName"
        },
        "SourceLoadBalancerId": {
          "Ref": "SourceLoadBalancerId"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "TagsPolicy": {
          "Ref": "TagsPolicy"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "BackendServers": {
          "Ref": "BackendServers"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "BackendServersPolicy": {
          "Ref": "BackendServersPolicy"
        }
      }
    }
  },
  "Outputs": {
    "LoadBalancerId": {
      "Description": "The id of load balance generated",
      "Value": {
        "Fn::GetAtt": [
          "LoadBalancerClone",
          "LoadBalancerId"
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
  LoadBalancerName:
    Type: String
    Description: >-
      Name of created load balancer. Length is limited to 1-80 characters,
      allowed to contain letters, numbers, '-, /, _,.' When not specified, a
      default name will be assigned.
  SourceLoadBalancerId:
    Type: String
    Description: Source load balancer id to clone
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  TagsPolicy:
    Type: String
    Description: >-
      Solution for handle the tags. If select 'clone', it will clone from source
      load balancer. If select 'empty' it will not coppy tags. If select
      'append' it will append the new tags. If select 'replace' it will add new
      tags.

      Default is 'empty'.
    AllowedValues:
      - clone
      - empty
      - append
      - replace
    Default: empty
  VSwitchId:
    Type: String
    Description: >-
      The new VSwitch ID to create load balancer instance. For VPC network only
      and the VSwitch should belong to the VPC which source load balancer is
      located. When not specified, source load balancer VSwitch ID will be used.
  BackendServers:
    Type: Json
    Description: 'The list of ECS instance, which will attached to load balancer.'
  Tags:
    Type: Json
    Description: >-
      Tags to attach to slb. Max support 5 tags to add during create slb. Each
      tag with two properties Key and Value, and Key is required.
    MaxLength: 5
  BackendServersPolicy:
    Type: String
    Description: >-
      Solution for handle the backend server and weights. If select 'clone', it
      will clone from source load balancer. If select 'empty' it will not attach
      any backend servers. If select 'append' it will append the new backend
      server list to source backed servers. If select 'replace' it will only
      attach new backend server list. Default is 'clone'.
    AllowedValues:
      - clone
      - empty
      - append
      - replace
    Default: clone
Resources:
  LoadBalancerClone:
    Type: 'ALIYUN::SLB::LoadBalancerClone'
    Properties:
      LoadBalancerName:
        Ref: LoadBalancerName
      SourceLoadBalancerId:
        Ref: SourceLoadBalancerId
      ResourceGroupId:
        Ref: ResourceGroupId
      TagsPolicy:
        Ref: TagsPolicy
      VSwitchId:
        Ref: VSwitchId
      BackendServers:
        Ref: BackendServers
      Tags:
        Ref: Tags
      BackendServersPolicy:
        Ref: BackendServersPolicy
Outputs:
  LoadBalancerId:
    Description: The id of load balance generated
    Value:
      'Fn::GetAtt':
        - LoadBalancerClone
        - LoadBalancerId
```


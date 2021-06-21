# ALIYUN::SLB::BackendServerToVServerGroupAddition

ALIYUN::SLB::BackendServerToVServerGroupAddition is used to add backend servers to an existing vServer group.

## Syntax

```
{
  "Type": "ALIYUN::SLB::BackendServerToVServerGroupAddition",
  "Properties": {
    "BackendServers": List,
    "VServerGroupId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VServerGroupId|String|Yes|No|The ID of the vServer group.|None|
|BackendServers|List|Yes|Yes|The list of backend servers.|For more information, see [BackendServers properties](#section_ivs_w1d_4do).|

## BackendServers syntax

```
"BackendServers": [
  {
    "ServerId": String,
    "Port": Integer,
    "Weight": Integer,
    "Type": String,
    "Description": String,
    "ServerIp": String
  }
]
```

## BackendServers properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServerId|String|Yes|Yes|The ID of the backend server.|None|
|Port|Integer|Yes|Yes|The port that is used by the backend server.|Valid values: 1 to 65535.|
|Weight|Integer|No|Yes|The weight of the backend server.|Valid values: 0 to 100.|
|Type|String|No|Yes|The type of the backend server.|Default value: ecs. Valid values:-   ecs: Elastic Compute Service \(ECS\) instances
-   eni: elastic network interfaces \(ENIs\)

**Note:** You can specify ENIs as backend servers only for high-performance SLB instances. |
|Description|String|No|Yes|The description of the backend server.|The description must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\),and underscores \(\_\).|
|ServerIp|String|No|Yes|The IP address of the backend server.|The IP addresses of ECS instances or ENIs are supported.|

## Response parameters

Fn::GetAtt

VServerGroupId: the ID of the vServer group.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VServerGroupId": {
      "Type": "String",
      "Description": "The ID of virtual server group."
    },
    "BackendServers": {
      "Type": "Json",
      "Description": "The list of a combination of ECS Instance-Port-Weight.Same ecs instance with different port is allowed, but same ecs instance with same port isn't."
    }
  },
  "Resources": {
    "BackendServerToVServerGroupAddition": {
      "Type": "ALIYUN::SLB::BackendServerToVServerGroupAddition",
      "Properties": {
        "VServerGroupId": {
          "Ref": "VServerGroupId"
        },
        "BackendServers": {
          "Ref": "BackendServers"
        }
      }
    }
  },
  "Outputs": {
    "VServerGroupId": {
      "Description": "The ID of virtual server group.",
      "Value": {
        "Fn::GetAtt": [
          "BackendServerToVServerGroupAddition",
          "VServerGroupId"
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
  VServerGroupId:
    Type: String
    Description: The ID of virtual server group.
  BackendServers:
    Type: Json
    Description: >-
      The list of a combination of ECS Instance-Port-Weight.Same ecs instance
      with different port is allowed, but same ecs instance with same port
      isn't.
Resources:
  BackendServerToVServerGroupAddition:
    Type: 'ALIYUN::SLB::BackendServerToVServerGroupAddition'
    Properties:
      VServerGroupId:
        Ref: VServerGroupId
      BackendServers:
        Ref: BackendServers
Outputs:
  VServerGroupId:
    Description: The ID of virtual server group.
    Value:
      'Fn::GetAtt':
        - BackendServerToVServerGroupAddition
        - VServerGroupId
```

To view more examples, visit [Listener.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json) and [Listener.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml). In the examples, the ALIYUN::SLB::Listener, ALIYUN::SLB::LoadBalancerClone, ALIYUN::SLB::Certificate, ALIYUN::SLB::DomainExtension, ALIYUN::SLB::VServerGroup, ALIYUN::SLB::Rule, and ALIYUN::SLB::BackendServerToVServerGroupAddition resource types are involved.


# ALIYUN::SLB::VServerGroup

ALIYUN::SLB::VServerGroup is used to create a vServer group and attach backend servers to a Server Load Balancer \(SLB\) instance.

## Syntax

```
{
  "Type": "ALIYUN::SLB::VServerGroup",
  "Properties": {
    "VServerGroupName": String,
    "BackendServers": List,
    "LoadBalancerId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VServerGroupName|String|Yes|No|The name of the vServer group.|None|
|BackendServers|List|No|Yes|The list of backend servers.|You can attach a maximum of 20 Elastic Compute Service \(ECS\) instances. For more information, see [BackendServers properties](#section_xgu_duh_zg3). |
|LoadBalancerId|String|Yes|No|The ID of the SLB instance.|None|

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
|Type|String|No|Yes|The type of the backend server.|Default value: ecs. Valid values:-   ecs: ECS instances
-   eni: elastic network interfaces \(ENIs\) |
|Description|String|No|Yes|The description of the backend server.|The description must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\),and underscores \(\_\).|
|ServerIp|String|No|Yes|The IP address of the backend server.|The IP addresses of ECS instances or ENIs are supported.|

## Response parameters

Fn::GetAtt

-   VServerGroupId: the ID of the vServer group.
-   BackendServers: the list of backend servers attached to the SLB instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VServerGroupName": {
      "Type": "String",
      "Description": "Display name of the VServerGroup."
    },
    "LoadBalancerId": {
      "Type": "String",
      "Description": "The id of load balancer."
    },
    "BackendServers": {
      "Type": "Json",
      "Description": "The list of a combination of ECS Instance-Port-Weight.Same ecs instance with different port is allowed, but same ecs instance with same port isn't."
    }
  },
  "Resources": {
    "VServerGroup": {
      "Type": "ALIYUN::SLB::VServerGroup",
      "Properties": {
        "VServerGroupName": {
          "Ref": "VServerGroupName"
        },
        "LoadBalancerId": {
          "Ref": "LoadBalancerId"
        },
        "BackendServers": {
          "Ref": "BackendServers"
        }
      }
    }
  },
  "Outputs": {
    "VServerGroupId": {
      "Description": "The id of VServerGroup created.",
      "Value": {
        "Fn::GetAtt": [
          "VServerGroup",
          "VServerGroupId"
        ]
      }
    },
    "BackendServers": {
      "Description": "Backend server list in this VServerGroup.",
      "Value": {
        "Fn::GetAtt": [
          "VServerGroup",
          "BackendServers"
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
  VServerGroupName:
    Type: String
    Description: Display name of the VServerGroup.
  LoadBalancerId:
    Type: String
    Description: The id of load balancer.
  BackendServers:
    Type: Json
    Description: >-
      The list of a combination of ECS Instance-Port-Weight.Same ecs instance
      with different port is allowed, but same ecs instance with same port
      isn't.
Resources:
  VServerGroup:
    Type: 'ALIYUN::SLB::VServerGroup'
    Properties:
      VServerGroupName:
        Ref: VServerGroupName
      LoadBalancerId:
        Ref: LoadBalancerId
      BackendServers:
        Ref: BackendServers
Outputs:
  VServerGroupId:
    Description: The id of VServerGroup created.
    Value:
      'Fn::GetAtt':
        - VServerGroup
        - VServerGroupId
  BackendServers:
    Description: Backend server list in this VServerGroup.
    Value:
      'Fn::GetAtt':
        - VServerGroup
        - BackendServers
```

To view more examples, visit [Listener.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json) and [Listener.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml). In the examples, the ALIYUN::SLB::Listener, ALIYUN::SLB::LoadBalancerClone, ALIYUN::SLB::Certificate, ALIYUN::SLB::DomainExtension, ALIYUN::SLB::VServerGroup, ALIYUN::SLB::Rule, and ALIYUN::SLB::BackendServerToVServerGroupAddition resource types are involved.


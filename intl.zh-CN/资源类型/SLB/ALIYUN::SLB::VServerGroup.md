# ALIYUN::SLB::VServerGroup

ALIYUN::SLB::VServerGroup类型用于创建虚拟服务器组并添加后端服务器到负载均衡实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VServerGroupName|String|是|否|虚拟服务器组名称。|无|
|BackendServers|List|否|是|需要添加的ECS实例列表。|最多添加20个ECS实例。 详情请参见[BackendServers属性](#section_xgu_duh_zg3)。 |
|LoadBalancerId|String|是|否|负载均衡实例ID。|无|

## BackendServers语法

```
"BackendServers": [
  {
    "ServerId": String,
    "Port": Integer,
    "Weight": Integer
  }
]          
```

## BackendServers属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerId|String|是|是|ECS实例ID。|无|
|Port|Integer|是|是|在负载均衡中监听的ECS端口号。|取值范围：1~65,535。|
|Weight|Integer|否|是|ECS实例在负载均衡实例中的权重。|取值范围：0~100。|

## 返回值

Fn::GetAtt

-   VServerGroupId：虚拟服务器组的ID。
-   BackendServers：添加到负载均衡实例的后端服务器列表。

## 示例

`JSON`格式

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

`YAML`格式

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


# ALIYUN::SLB::VServerGroup

ALIYUN::SLB::VServerGroup类型用于创建服务器组并添加后端服务器到负载均衡实例。

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
|VServerGroupName|String|是|否|服务器组名称。|无|
|BackendServers|List|否|是|后端服务器列表。|最多添加20个ECS实例。更多信息，请参见[BackendServers属性](#section_xgu_duh_zg3)。 |
|LoadBalancerId|String|是|否|负载均衡实例ID。|无|

## BackendServers语法

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

## BackendServers属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerId|String|是|是|后端服务器的实例ID。|无|
|Port|Integer|是|是|后端服务器使用的端口。|取值范围：1~65,535。|
|Weight|Integer|否|是|后端服务器的权重。|取值范围：0~100。|
|Type|String|否|是|后端服务器类型。|取值：-   ecs（默认值）：ECS实例。
-   eni：弹性网卡实例。 |
|Description|String|否|是|后端服务器描述。|长度为1~80个字符，支持英文字母、汉字、数字、短划线（-）、正斜线（/）、半角句号（.）和下划线（\_）。|
|ServerIp|String|否|是|后端服务器的IP地址。|ECS或者ENI的实例IP。|

## 返回值

Fn::GetAtt

-   VServerGroupId：服务器组的ID。
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

更多示例，请参见创建负载均衡监听、克隆负载均衡实例、上传证书、创建扩展域名、创建服务器组并添加后端服务器到负载均衡实例、为HTTP或HTTPS监听添加转发规则和将后端服务器添加到服务器组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml)。


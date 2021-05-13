# ALIYUN::SLB::BackendServerToVServerGroupAddition

ALIYUN::SLB::BackendServerToVServerGroupAddition类型用于把后端服务器添加到已存在的服务器组中。

## 语法

```
{
  "Type": "ALIYUN::SLB::BackendServerToVServerGroupAddition",
  "Properties": {
    "BackendServers": List,
    "VServerGroupId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VServerGroupId|String|是|否|服务器组ID。|无|
|BackendServers|List|是|是|服务器列表。|更多信息，请参见[BackendServers属性](#section_ivs_w1d_4do)。|

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
-   eni：弹性网卡实例。

**说明：** 只有性能保障型实例支持添加ENI类型的后端服务器。 |
|Description|String|否|是|后端服务器描述。|长度为1~80个字符，可包含英文字母、汉字、数字、短划线（-）、正斜线（/）、半角句号（.）和下划线（\_）。|
|ServerIp|String|否|是|后端服务器的IP地址。|ECS或者ENI的实例IP地址。|

## 返回值

Fn::GetAtt

VServerGroupId：服务器组的ID。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建负载均衡监听、克隆负载均衡实例、上传证书、创建扩展域名、创建服务器组并添加后端服务器到负载均衡实例、为HTTP或HTTPS监听添加转发规则和将后端服务器添加到服务器组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml)。


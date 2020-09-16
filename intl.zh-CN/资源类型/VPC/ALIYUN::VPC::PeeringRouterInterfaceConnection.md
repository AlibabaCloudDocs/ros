# ALIYUN::VPC::PeeringRouterInterfaceConnection

ALIYUN::VPC::PeeringRouterInterfaceConnection类型用于发起路由器接口连接。

## 语法

```
{
  "Type": "ALIYUN::VPC::PeeringRouterInterfaceConnection",
  "Properties": {
    "OppositeInterfaceId": String,
    "RouterInterfaceId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OppositeInterfaceId|String|是|否|接收端路由器接口的ID。|无|
|RouterInterfaceId|String|是|否|发起端路由器接口的ID。|无|

## 返回值

Fn::GetAtt

-   OppositeInterfaceId：接收端路由器接口的ID。
-   RouterInterfaceId：发起端路由器接口的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "OppositeInterfaceId": {
      "Type": "String",
      "Description": "The Receiver RouterInterface ID to accept peer RouterInterface."
    },
    "RouterInterfaceId": {
      "Type": "String",
      "Description": "The Initiator RouterInterface ID to connect peer RouterInterface."
    }
  },
  "Resources": {
    "RouterInterfaceConnection": {
      "Type": "ALIYUN::VPC::PeeringRouterInterfaceConnection",
      "Properties": {
        "OppositeInterfaceId": {
          "Ref": "OppositeInterfaceId"
        },
        "RouterInterfaceId": {
          "Ref": "RouterInterfaceId"
        }
      }
    }
  },
  "Outputs": {
    "OppositeInterfaceId": {
      "Description": "The receiver RouterInterface ID.",
      "Value": {
        "Fn::GetAtt": [
          "RouterInterfaceConnection",
          "OppositeInterfaceId"
        ]
      }
    },
    "RouterInterfaceId": {
      "Description": "The initiator RouterInterface ID.",
      "Value": {
        "Fn::GetAtt": [
          "RouterInterfaceConnection",
          "RouterInterfaceId"
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
  OppositeInterfaceId:
    Type: String
    Description: The Receiver RouterInterface ID to accept peer RouterInterface.
  RouterInterfaceId:
    Type: String
    Description: The Initiator RouterInterface ID to connect peer RouterInterface.
Resources:
  RouterInterfaceConnection:
    Type: 'ALIYUN::VPC::PeeringRouterInterfaceConnection'
    Properties:
      OppositeInterfaceId:
        Ref: OppositeInterfaceId
      RouterInterfaceId:
        Ref: RouterInterfaceId
Outputs:
  OppositeInterfaceId:
    Description: The receiver RouterInterface ID.
    Value:
      'Fn::GetAtt':
        - RouterInterfaceConnection
        - OppositeInterfaceId
  RouterInterfaceId:
    Description: The initiator RouterInterface ID.
    Value:
      'Fn::GetAtt':
        - RouterInterfaceConnection
        - RouterInterfaceId
```


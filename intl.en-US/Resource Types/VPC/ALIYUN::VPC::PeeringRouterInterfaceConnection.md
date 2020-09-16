# ALIYUN::VPC::PeeringRouterInterfaceConnection

ALIYUN::VPC::PeeringRouterInterfaceConnection is used to initiate a router interface connection.

## Syntax

```
{
  "Type": "ALIYUN::VPC::PeeringRouterInterfaceConnection",
  "Properties": {
    "OppositeInterfaceId": String,
    "RouterInterfaceId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OppositeInterfaceId|String|Yes|No|The ID of the router interface that accepts the connection.|None|
|RouterInterfaceId|String|Yes|No|The ID of the router interface that initiates the connection.|None|

## Response parameters

Fn::GetAtt

-   OppositeInterfaceId: the ID of the router interface that accepts the connection.
-   RouterInterfaceId: the ID of the router interface that initiates the connection.

## Examples

`JSON` format

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

`YAML` format

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


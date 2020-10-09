# ALIYUN::ECS::AssignIpv6Addresses

ALIYUN::ECS::AssignIpv6Addresses类型用于为弹性网卡分配IPv6地址。

## 语法

```
{
  "Type": "ALIYUN::ECS::AssignIpv6Addresses",
  "Properties": {
    "Ipv6Addresses": List,
    "Ipv6AddressCount": Integer,
    "NetworkInterfaceId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Ipv6Addresses|List|否|否|弹性网卡指定的IPv6地址。|示例：\["2001:db8:1234:1a00::\*\*\*"\]。目前仅支持指定一个IPv6地址。不能同时指定参数Ipv6Addresses和Ipv6AddressCount。|
|Ipv6AddressCount|Integer|否|否|为弹性网卡指定的随机生成的IPv6地址数量。|不能同时指定参数Ipv6Addresses和Ipv6AddressCount。|
|NetworkInterfaceId|String|是|否|弹性网卡ID。|无|

## 返回值

Fn::GetAtt

-   Ipv6Addresses：IPv6地址。
-   Ipv6AddressIds：IPv6地址ID。
-   NetworkInterfaceId：弹性网卡ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AssignIpv6Addresses": {
      "Type": "ALIYUN::ECS::AssignIpv6Addresses",
      "Properties": {
        "Ipv6AddressCount": {
          "Ref": "Ipv6AddressCount"
        },
        "Ipv6Addresses": {
          "Ref": "Ipv6Addresses"
        },
        "NetworkInterfaceId": {
          "Ref": "NetworkInterfaceId"
        }
      }
    }
  },
  "Parameters": {
    "Ipv6AddressCount": {
      "Type": "Number",
      "Description": "IPv6 addresses specified number of randomly generated interfaces elasticity.\nNote You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount at the same time.",
      "MinValue": 0
    },
    "Ipv6Addresses": {
      "Type": "CommaDelimitedList",
      "Description": "Specify one or more IPv6 addresses for the elastic NIC. Currently, the maximum list size is 1. Example value: 2001:db8:1234:1a00::*** .\nNote You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount at the same time.",
      "MaxLength": 1
    },
    "NetworkInterfaceId": {
      "Type": "String",
      "Description": "Elastic network interface ID."
    }
  },
  "Outputs": {
    "Ipv6AddressIds": {
      "Description": "Assigned IPv6 address IDs.",
      "Value": {
        "Fn::GetAtt": [
          "AssignIpv6Addresses",
          "Ipv6AddressIds"
        ]
      }
    },
    "Ipv6Addresses": {
      "Description": "Assigned IPv6 addresses.",
      "Value": {
        "Fn::GetAtt": [
          "AssignIpv6Addresses",
          "Ipv6Addresses"
        ]
      }
    },
    "NetworkInterfaceId": {
      "Description": "Elastic network interface ID.",
      "Value": {
        "Fn::GetAtt": [
          "AssignIpv6Addresses",
          "NetworkInterfaceId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  AssignIpv6Addresses:
    Type: 'ALIYUN::ECS::AssignIpv6Addresses'
    Properties:
      Ipv6AddressCount:
        Ref: Ipv6AddressCount
      Ipv6Addresses:
        Ref: Ipv6Addresses
      NetworkInterfaceId:
        Ref: NetworkInterfaceId
Parameters:
  Ipv6AddressCount:
    Type: Number
    Description: >-
      IPv6 addresses specified number of randomly generated interfaces
      elasticity.

      Note You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount
      at the same time.
    MinValue: 0
  Ipv6Addresses:
    Type: CommaDelimitedList
    Description: >-
      Specify one or more IPv6 addresses for the elastic NIC. Currently, the
      maximum list size is 1. Example value: 2001:db8:1234:1a00::*** .

      Note You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount
      at the same time.
    MaxLength: 1
  NetworkInterfaceId:
    Type: String
    Description: Elastic network interface ID.
Outputs:
  Ipv6AddressIds:
    Description: Assigned IPv6 address IDs.
    Value:
      'Fn::GetAtt':
        - AssignIpv6Addresses
        - Ipv6AddressIds
  Ipv6Addresses:
    Description: Assigned IPv6 addresses.
    Value:
      'Fn::GetAtt':
        - AssignIpv6Addresses
        - Ipv6Addresses
  NetworkInterfaceId:
    Description: Elastic network interface ID.
    Value:
      'Fn::GetAtt':
        - AssignIpv6Addresses
        - NetworkInterfaceId
```


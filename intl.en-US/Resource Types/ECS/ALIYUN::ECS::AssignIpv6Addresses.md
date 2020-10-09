# ALIYUN::ECS::AssignIpv6Addresses

ALIYUN::ECS::AssignIpv6Addresses is used to assign one or more IPv6 addresses to an elastic network interface \(ENI\).

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Ipv6Addresses|List|No|No|The list of IPv6 addresses that are assigned to the ENI.|Example: \["2001:db8:1234:1a00::\*\*\*"\]. Only one IPv6 address can be specified. You can specify one of the Ipv6Addresses and Ipv6AddressCount parameters, but you cannot specify both of them.|
|Ipv6AddressCount|Integer|No|No|The number of randomly generated IPv6 addresses that are assigned to the ENI.|You can specify one of the Ipv6Addresses and Ipv6AddressCount parameters, but you cannot specify both of them.|
|NetworkInterfaceId|String|Yes|No|The ID of the ENI.|None|

## Response parameters

Fn::GetAtt

-   Ipv6Addresses: the list of IPv6 addresses.
-   Ipv6Addresses: the list of IPv6 address IDs.
-   NetworkInterfaceId: the ID of the ENI.

## Examples

`JSON` format

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

`YAML` format

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


# ALIYUN::ECS::AssignPrivateIpAddresses

ALIYUN::ECS::AssignPrivateIpAddresses is used to assign one or more secondary private IP addresses to an ENI. You can specify private IP addresses within the CIDR block of the VSwitch that hosts the ENI. You can also specify the number of private IP addresses for ECS to assign them automatically.

## Syntax

```
{
  "Type": "ALIYUN::ECS::AssignPrivateIpAddresses",
  "Properties": {
    "NetworkInterfaceId": String,
    "SecondaryPrivateIpAddressCount": Integer,
    "PrivateIpAddresses": List
  }
}
```

## Properties

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|NetworkInterfaceId|String|Yes|No|The ID of the ENI.|None|
|SecondaryPrivateIpAddressCount|Integer|No|No|The number of private IP addresses assigned to the ENI.|None|
|PrivateIpAddresses|List|No|No|The list of one or more secondary private IP addresses selected from the CIDR block of the VSwitch that hosts the ENI.|When the ENI is in the Available state, up to 10 IP addresses can be specified. When the ENI is in the InUse state, the number of IP addresses that can be specified depends on the instance type. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md). To assign secondary private IP addresses, you must specify either the PrivateIpAddress parameter or the SecondaryPrivateIpAddressCount parameter. But you cannot specify both of them.|

## Response parameters

Fn::GetAtt

-   NetworkInterfaceId: the ID of the ENI.
-   PrivateIpAddresses: the secondary private IP addresses assigned to the ENI.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AssignPrivateIpAddresses": {
      "Type": "ALIYUN::ECS::AssignPrivateIpAddresses",
      "Properties": {
        "NetworkInterfaceId": {
          "Ref": "NetworkInterfaceId"
        },
        "SecondaryPrivateIpAddressCount": {
          "Ref": "SecondaryPrivateIpAddressCount"
        },
        "PrivateIpAddresses": {
          "Fn::Split": [
            ",",
            {
              "Ref": "PrivateIpAddresses"
            }
          ]
        }
      }
    }
  },
  "Parameters": {
    "NetworkInterfaceId": {
      "Type": "String",
      "Description": "The ID of the ENI."
    },
    "SecondaryPrivateIpAddressCount": {
      "Type": "Number",
      "Description": "The specified number of private IP addresses to be assigned by the ECS instance.",
      "MinValue": 0
    },
    "PrivateIpAddresses": {
      "Type": "CommaDelimitedList",
      "Description": "One or multiple secondary private IP addresses selected from the CIDR block of the VSwitch that hosts the ENI. Valid values of number of private ip addresses:When the ENI is in the Available state: 1 to 10.When the ENI is in the InUse state: limited by the instance type. For more information, see Instance type families. You must specify either the PrivateIpAddresses parameter or the SecondaryPrivateIpAddressCount parameter to assign secondary private IP addresses.",
      "MaxLength": 10
    }
  },
  "Outputs": {
    "NetworkInterfaceId": {
      "Description": "The ID of the ENI.",
      "Value": {
        "Fn::GetAtt": [
          "AssignPrivateIpAddresses",
          "NetworkInterfaceId"
        ]
      }
    },
    "PrivateIpAddresses": {
      "Description": "Assigned private ip addresses.",
      "Value": {
        "Fn::GetAtt": [
          "AssignPrivateIpAddresses",
          "PrivateIpAddresses"
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
  AssignPrivateIpAddresses:
    Type: ALIYUN::ECS::AssignPrivateIpAddresses
    Properties:
      NetworkInterfaceId:
        Ref: NetworkInterfaceId
      SecondaryPrivateIpAddressCount:
        Ref: SecondaryPrivateIpAddressCount
      PrivateIpAddresses:
        Fn::Split:
        - ","
        - Ref: PrivateIpAddresses
Parameters:
  NetworkInterfaceId:
    Type: String
    Description: The ID of the ENI.
  SecondaryPrivateIpAddressCount:
    Type: Number
    Description: The specified number of private IP addresses to be assigned by the
      ECS instance.
    MinValue: 0
  PrivateIpAddresses:
    Type: CommaDelimitedList
    Description: 'One or multiple secondary private IP addresses selected from the
      CIDR block of the VSwitch that hosts the ENI. Valid values of number of private
      ip addresses:When the ENI is in the Available state: 1 to 10.When the ENI is
      in the InUse state: limited by the instance type. For more information, see
      Instance type families. You must specify either the PrivateIpAddresses parameter
      or the SecondaryPrivateIpAddressCount parameter to assign secondary private
      IP addresses.'
    MaxLength: 10
Outputs:
  NetworkInterfaceId:
    Description: The ID of the ENI.
    Value:
      Fn::GetAtt:
      - AssignPrivateIpAddresses
      - NetworkInterfaceId
  PrivateIpAddresses:
    Description: Assigned private ip addresses.
    Value:
      Fn::GetAtt:
      - AssignPrivateIpAddresses
      - PrivateIpAddresses
```


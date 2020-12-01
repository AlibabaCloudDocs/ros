# ALIYUN::VPC::EIPAssociation

ALIYUN::VPC::EIPAssociation is used to associate an elastic IP address \(EIP\) with a cloud service instance.

## Syntax

```
{
  "Type": "ALIYUN::VPC::EIPAssociation",
  "Properties": {
    "AllocationId": String,
    "InstanceId": String,
    "PrivateIpAddress": String,
    "Mode": String
  }
}         
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AllocationId|String|Yes|Yes|The ID of the EIP.|None|
|InstanceId|String|Yes|Yes|The ID of the cloud service instance.|The following instance types are supported: -   VPC-type ECS instances
-   VPC-type SLB instances
-   NAT gateways
-   High-Availability Virtual IP Address \(HAVIP\)
-   Elastic network interfaces \(ENIs\) |
|PrivateIpAddress|String|No|Yes|The private IP address in the CIDR block of the vSwitch.|None|
|Mode|String|No|Yes|The association mode.|Valid values: -   NAT
-   MULTI\_BINDED |

## Response parameters

Fn::GetAtt

-   EipAddress: the allocated EIP.
-   AllocationId: the ID of the instance to which the EIP is allocated.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "An IP address in the CIDR block of the VSwitch.\nIf you leave the option empty, the system allocates a private IP address according to the VPC ID and VSwitch ID."
    },
    "InstanceId": {
      "Type": "String",
      "Description": "ECS/SLB/NAT/HaVip/ENI instance id to bid the EIP."
    },
    "AllocationId": {
      "Type": "String",
      "Description": "EIP instance id to bind."
    },
    "Mode": {
      "Type": "String",
      "Description": "The mode of association. Valid values:\nNAT(Default): NAT mode.\nBINDED: Cut-through mode.\nMULTI_BINDED: Multi-EIP to ENI mode.\nThis is required only when the value of InstanceType is NetworkInterface.",
      "AllowedValues": [
        "NAT",
        "MULTI_BINDED",
        "BINDED"
      ]
    }
  },
  "Resources": {
    "ElasticIpAssociation": {
      "Type": "ALIYUN::VPC::EIPAssociation",
      "Properties": {
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "AllocationId": {
          "Ref": "AllocationId"
        },
        "Mode": {
          "Ref": "Mode"
        }
      }
    }
  },
  "Outputs": {
    "AllocationId": {
      "Description": "ID that Aliyun assigns to represent the allocation of the address for use with VPC. Returned only for VPC elastic IP addresses.",
      "Value": {
        "Fn::GetAtt": [
          "ElasticIpAssociation",
          "AllocationId"
        ]
      }
    },
    "EipAddress": {
      "Description": "IP address of created EIP.",
      "Value": {
        "Fn::GetAtt": [
          "ElasticIpAssociation",
          "EipAddress"
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
  PrivateIpAddress:
    Type: String
    Description: >-
      An IP address in the CIDR block of the VSwitch.

      If you leave the option empty, the system allocates a private IP address
      according to the VPC ID and VSwitch ID.
  InstanceId:
    Type: String
    Description: ECS/SLB/NAT/HaVip/ENI instance id to bid the EIP.
  AllocationId:
    Type: String
    Description: EIP instance id to bind.
  Mode:
    Type: String
    Description: |-
      The mode of association. Valid values:
      NAT(Default): NAT mode.
      BINDED: Cut-through mode.
      MULTI_BINDED: Multi-EIP to ENI mode.
      This is required only when the value of InstanceType is NetworkInterface.
    AllowedValues:
      - NAT
      - MULTI_BINDED
      - BINDED
Resources:
  ElasticIpAssociation:
    Type: 'ALIYUN::VPC::EIPAssociation'
    Properties:
      PrivateIpAddress:
        Ref: PrivateIpAddress
      InstanceId:
        Ref: InstanceId
      AllocationId:
        Ref: AllocationId
      Mode:
        Ref: Mode
Outputs:
  AllocationId:
    Description: >-
      ID that Aliyun assigns to represent the allocation of the address for use
      with VPC. Returned only for VPC elastic IP addresses.
    Value:
      'Fn::GetAtt':
        - ElasticIpAssociation
        - AllocationId
  EipAddress:
    Description: IP address of created EIP.
    Value:
      'Fn::GetAtt':
        - ElasticIpAssociation
        - EipAddress
```


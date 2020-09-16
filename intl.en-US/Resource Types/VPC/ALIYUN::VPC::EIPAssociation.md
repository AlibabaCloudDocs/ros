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
-   HAVIP
-   Elastic network interfaces \(ENIs\) |
|PrivateIpAddress|String|No|Yes|The private IP address in the CIDR block of the VSwitch.|None|
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
  "Resources": {
    "Eip": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "InternetChargeType": "PayByTraffic",
          "Bandwidth": 200
      }
    },
    "EipAssociation": {
      "Type": "ALIYUN::VPC::EIPAssociation", 
      "Properties": {
        "InstanceId": "<LoadBalancerId>", 
        "InstanceType": "EcsInstance", 
        "AllocationId": {
          "Fn::GetAtt": ["Eip", "AllocationId"]
        }
      }
    }
  },
  "Outputs": {
    "EipAddress": {
      "Value" : {"Fn::GetAtt": ["EipAssociation", "EipAddress"]}
    },
    "AllocationId": {
      "Value" : {"Fn::GetAtt": ["EipAssociation", "AllocationId"]}
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Eip:
    Type: ALIYUN::VPC::EIP
    Properties:
      InternetChargeType: PayByTraffic
      Bandwidth: 200
  EipAssociation:
    Type: ALIYUN::VPC::EIPAssociation
    Properties:
      InstanceId: "<LoadBalancerId>"
      InstanceType: EcsInstance
      AllocationId:
        Fn::GetAtt:
        - Eip
        - AllocationId
Outputs:
  EipAddress:
    Value:
      Fn::GetAtt:
      - EipAssociation
      - EipAddress
  AllocationId:
    Value:
      Fn::GetAtt:
      - EipAssociation
      - AllocationId     
```


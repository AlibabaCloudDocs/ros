# ALIYUN::VPC::EIPAssociation

ALIYUN::VPC::EIPAssociation用于绑定弹性公网IP。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AllocationId|String|是|是|需要进行绑定操作的EIP ID。|无|
|InstanceId|String|是|是|需要进行绑定操作的云产品实例ID。|支持以下云产品实例类型： -   VPC类型的ECS实例。
-   VPC类型的SLB实例。
-   NAT网关。
-   HAVIP。
-   弹性网卡。 |
|PrivateIpAddress|String|否|是|交换机的CIDR地址段中的私有IP地址。|无|
|Mode|String|否|是|关联模式。|取值： -   NAT
-   MULTI\_BINDED |

## 返回值

Fn::GetAtt

-   EipAddress：分配的弹性公网IP。
-   AllocationId：弹性公网IP的实例ID。

## 示例

`JSON`格式

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

`YAML`格式

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


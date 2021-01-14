# ALIYUN::VPC::EIPAssociation

ALIYUN::VPC::EIPAssociation用于为云产品实例绑定弹性公网IP（EIP）。

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
|AllocationId|String|是|是|弹性公网IP的ID。|无|
|InstanceId|String|是|是|云产品实例的ID。|支持以下云产品实例类型： -   VPC类型的ECS实例。
-   VPC类型的SLB实例。
-   NAT网关。
-   高可用虚拟IP（HaVip）。
-   弹性网卡。 |
|PrivateIpAddress|String|否|是|交换机网段内的一个私网IP地址。|如果不指定该参数，系统将根据VPC ID和交换机ID自动分配一个私网IP地址。|
|Mode|String|否|是|绑定模式。|取值： -   NAT（默认值）：NAT模式（普通模式）。
-   MULTI\_BINDED：多EIP网卡可见模式。
-   BINDED：EIP网卡可见模式。

**说明：** 关于如何设置BINDED，请参见[设置EIP网卡可见模式](/intl.zh-CN/用户指南/绑定云资源/绑定辅助弹性网卡/设置EIP网卡可见模式.md)。 |

## 返回值

Fn::GetAtt

-   EipAddress：弹性公网IP的地址。
-   AllocationId：弹性公网IP的ID。

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


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
|AllocationId|String|是|是|需要进行绑定操作的EIP ID|无|
|InstanceId|String|是|是|需要进行绑定操作的云产品实例ID|支持以下云产品实例类型： -   VPC类型的ECS实例
-   VPC类型的SLB实例
-   NAT网关
-   HAVIP
-   弹性网卡 |
|PrivateIpAddress|String|否|是|虚拟交换机的CIDR地址段中的私有IP地址|无|
|Mode|String|否|是|关联模式|取值： -   NAT
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

`YAML`格式

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


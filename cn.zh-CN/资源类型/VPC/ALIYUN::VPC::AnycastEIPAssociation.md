# ALIYUN::VPC::AnycastEIPAssociation

ALIYUN::VPC::AnycastEIPAssociation类型用于将任播弹性公网IP（Anycast EIP）绑定到指定地域的云资源实例上。

## 语法

```
{
  "Type": "ALIYUN::VPC::AnycastEIPAssociation",
  "Properties": {
    "BindInstanceId": String,
    "BindInstanceRegionId": String,
    "BindInstanceType": String,
    "AnycastId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|BindInstanceId|String|是|否|待绑定的云资源实例ID。|无|
|BindInstanceRegionId|String|是|否|待绑定的云资源实例地域ID。|无|
|BindInstanceType|String|是|否|待绑定的云资源实例类型。|取值：SlbInstance，表示私网负载均衡（SLB）实例。|
|AnycastId|String|是|否|Anycast EIP实例ID。|无|

## 返回值

Fn::GetAtt

-   BindInstanceId：已绑定的云资源实例ID。
-   BindInstanceRegionId：已绑定的云资源实例地域ID。
-   BindInstanceType：已绑定的云资源实例类型。
-   AnycastId：Anycast EIP实例ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "BindInstanceId": {
      "Type": "String",
      "Description": "The ID of the cloud resource instance to be bound."
    },
    "BindInstanceRegionId": {
      "Type": "String",
      "Description": "The region ID of the cloud resource instance to be bound."
    },
    "BindInstanceType": {
      "Type": "String",
      "Description": "The cloud resource instance type to be bound. Valid value: SlbInstance, SLB instance of private network type."
    },
    "AnycastId": {
      "Type": "String",
      "Description": "Anycast EIP instance ID."
    }
  },
  "Resources": {
    "AnycastEIPAssociation": {
      "Type": "ALIYUN::VPC::AnycastEIPAssociation",
      "Properties": {
        "BindInstanceId": {
          "Ref": "BindInstanceId"
        },
        "BindInstanceRegionId": {
          "Ref": "BindInstanceRegionId"
        },
        "BindInstanceType": {
          "Ref": "BindInstanceType"
        },
        "AnycastId": {
          "Ref": "AnycastId"
        }
      }
    }
  },
  "Outputs": {
    "BindInstanceId": {
      "Description": "The ID of the cloud resource instance to be bound.",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEIPAssociation",
          "BindInstanceId"
        ]
      }
    },
    "BindInstanceRegionId": {
      "Description": "The region ID of the cloud resource instance to be bound.",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEIPAssociation",
          "BindInstanceRegionId"
        ]
      }
    },
    "BindInstanceType": {
      "Description": "The cloud resource instance type to be bound.",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEIPAssociation",
          "BindInstanceType"
        ]
      }
    },
    "AnycastId": {
      "Description": "Anycast EIP instance ID.",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEIPAssociation",
          "AnycastId"
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
  AnycastId:
    Description: Anycast EIP instance ID.
    Type: String
  BindInstanceId:
    Description: The ID of the cloud resource instance to be bound.
    Type: String
  BindInstanceRegionId:
    Description: The region ID of the cloud resource instance to be bound.
    Type: String
  BindInstanceType:
    Description: 'The cloud resource instance type to be bound. Valid value: SlbInstance,
      SLB instance of private network type.'
    Type: String
Resources:
  AnycastEIPAssociation:
    Properties:
      AnycastId:
        Ref: AnycastId
      BindInstanceId:
        Ref: BindInstanceId
      BindInstanceRegionId:
        Ref: BindInstanceRegionId
      BindInstanceType:
        Ref: BindInstanceType
    Type: ALIYUN::VPC::AnycastEIPAssociation
Outputs:
  AnycastId:
    Description: Anycast EIP instance ID.
    Value:
      Fn::GetAtt:
      - AnycastEIPAssociation
      - AnycastId
  BindInstanceId:
    Description: The ID of the cloud resource instance to be bound.
    Value:
      Fn::GetAtt:
      - AnycastEIPAssociation
      - BindInstanceId
  BindInstanceRegionId:
    Description: The region ID of the cloud resource instance to be bound.
    Value:
      Fn::GetAtt:
      - AnycastEIPAssociation
      - BindInstanceRegionId
  BindInstanceType:
    Description: The cloud resource instance type to be bound.
    Value:
      Fn::GetAtt:
      - AnycastEIPAssociation
      - BindInstanceType
```


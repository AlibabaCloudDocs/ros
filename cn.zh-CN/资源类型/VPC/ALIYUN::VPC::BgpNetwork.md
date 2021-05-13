# ALIYUN::VPC::BgpNetwork

ALIYUN::VPC::BgpNetwork类型用于宣告BGP网络。

## 语法

```
{
  "Type": "ALIYUN::VPC::BgpNetwork",
  "Properties": {
    "DstCidrBlock": String,
    "RouterId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DstCidrBlock|String|是|否|需要和本地数据中心（IDC）互连的VPC或交换机的网段。|无|
|RouterId|String|是|否|路由器接口关联的路由器ID。|无|

## 返回值

Fn::GetAtt

-   DstCidrBlock：需要和本地IDC互连的VPC或交换机的网段。
-   RouterId：路由器接口关联的路由器ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DstCidrBlock": {
      "Type": "String",
      "Description": "The CIDR block of the virtual private cloud (VPC) or vSwitch that you want to connect\nto a data center."
    },
    "RouterId": {
      "Type": "String",
      "Description": "The ID of the vRouter associated with the router interface."
    }
  },
  "Resources": {
    "BgpNetwork": {
      "Type": "ALIYUN::VPC::BgpNetwork",
      "Properties": {
        "DstCidrBlock": {
          "Ref": "DstCidrBlock"
        },
        "RouterId": {
          "Ref": "RouterId"
        }
      }
    }
  },
  "Outputs": {
    "DstCidrBlock": {
      "Description": "The CIDR block of the virtual private cloud (VPC) or vSwitch that you want to connect\nto a data center.",
      "Value": {
        "Fn::GetAtt": [
          "BgpNetwork",
          "DstCidrBlock"
        ]
      }
    },
    "RouterId": {
      "Description": "The ID of the vRouter associated with the router interface.",
      "Value": {
        "Fn::GetAtt": [
          "BgpNetwork",
          "RouterId"
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
  DstCidrBlock:
    Description: 'The CIDR block of the virtual private cloud (VPC) or vSwitch that
      you want to connect

      to a data center.'
    Type: String
  RouterId:
    Description: The ID of the vRouter associated with the router interface.
    Type: String
Resources:
  BgpNetwork:
    Properties:
      DstCidrBlock:
        Ref: DstCidrBlock
      RouterId:
        Ref: RouterId
    Type: ALIYUN::VPC::BgpNetwork
Outputs:
  DstCidrBlock:
    Description: 'The CIDR block of the virtual private cloud (VPC) or vSwitch that
      you want to connect

      to a data center.'
    Value:
      Fn::GetAtt:
      - BgpNetwork
      - DstCidrBlock
  RouterId:
    Description: The ID of the vRouter associated with the router interface.
    Value:
      Fn::GetAtt:
      - BgpNetwork
      - RouterId
```


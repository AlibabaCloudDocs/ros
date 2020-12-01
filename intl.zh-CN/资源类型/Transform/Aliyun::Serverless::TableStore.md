# Aliyun::Serverless::TableStore

Aliyun::Serverless::TableStore类型用于创建表格存储实例。

## 语法

```
{
  "Type": "Aliyun::Serverless::TableStore",
  "Properties": {
    "ClusterType": String,
    "Description": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ClusterType|String|是|否|实例规格|取值：-   HYBRID：容量型实例。
-   SSD：高性能实例。 |
|Description|String|是|否|实例描述|无。|

## 返回值

Fn::GetAtt

-   PrivateEndpoint：私网地址。
-   PublicEndpoint：公网地址。
-   VpcEndpoint：专有网络终端节点。
-   InstanceName：实例名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Parameters": {
    "ClusterType": {
      "Type": "String",
      "Default": "HYBRID"
    }
  },
  "Resources": {
    "MyInstance": {
      "Type": "Aliyun::Serverless::TableStore",
      "Properties": {
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "Description": "Description for MyOtsInstance"
      }
    }
  },
  "Outputs": {
    "PrivateEndpoint": {
      "Value": {
        "Fn::GetAtt": [
          "MyInstance",
          "PrivateEndpoint"
        ]
      }
    },
    "PublicEndpoint": {
      "Value": {
        "Fn::GetAtt": [
          "MyInstance",
          "PublicEndpoint"
        ]
      }
    },
    "VpcEndpoint": {
      "Value": {
        "Fn::GetAtt": [
          "MyInstance",
          "VpcEndpoint"
        ]
      }
    },
    "InstanceName": {
      "Value": {
        "Fn::GetAtt": [
          "MyInstance",
          "InstanceName"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Parameters:
  ClusterType:
    Type: String
    Default: HYBRID
Resources:
  MyInstance:
    Type: 'Aliyun::Serverless::TableStore'
    Properties:
      ClusterType:
        Ref: ClusterType
      Description: Description for MyOtsInstance
Outputs:
  PrivateEndpoint:
    Value:
      'Fn::GetAtt':
        - MyInstance
        - PrivateEndpoint
  PublicEndpoint:
    Value:
      'Fn::GetAtt':
        - MyInstance
        - PublicEndpoint
  VpcEndpoint:
    Value:
      'Fn::GetAtt':
        - MyInstance
        - VpcEndpoint
  InstanceName:
    Value:
      'Fn::GetAtt':
        - MyInstance
        - InstanceName
```


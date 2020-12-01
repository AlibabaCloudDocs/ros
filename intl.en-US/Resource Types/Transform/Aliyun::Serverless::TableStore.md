# Aliyun::Serverless::TableStore

Aliyun::Serverless::TableStore is used to create a create a Tablestore instance.

## Syntax

```
{
  "Type": "Aliyun::Serverless::TableStore",
  "Properties": {
    "ClusterType": String,
    "Description": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ClusterType|String|Yes|No|The instance type.|Valid values:-   HYBRID: capacity instance
-   SSD: high-performance instance |
|Description|String|Yes|No|The description of the instance.|None|

## Response parameters

Fn::GetAtt

-   PrivateEndpoint: the private endpoint of the instance.
-   PublicEndpoint: the public endpoint of the instance.
-   VpcEndpoint: the endpoint of the VPC.
-   InstanceName: the name of the instance.

## Examples

`JSON` format

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

`YAML` format

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


# ALIYUN::ROCKETMQ::Instance

ALIYUN::ROCKETMQ::Instance is used to create a Standard Edition instance.

## Syntax

```
{
  "Type": "ALIYUN::ROCKETMQ::Instance",
  "Properties": {
    "Remark": String,
    "InstanceName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Remark|String|No|Yes|The description of the instance.|The description can be up to 128 character in length.|
|InstanceName|String|Yes|Yes|The name of the instance.|The name must be 3 to 64 characters in length, and can contain letters, digits, hyphens \(-\), and underscores \(\_\).|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance.
-   InstanceType: the type of the instance. If 1 is returned, the created instance is of the Standard Edition.
-   HttpInternetEndpoint: the public HTTP endpoint.
-   HttpInternetSecureEndpoint: the public HTTPS endpoint.
-   TcpEndpoint: the TCP endpoint.
-   HttpInternalEndpoint: the internal HTTP endpoint.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the instance, which contains 3 to 64 characters in Chinese or English.",
      "MinLength": 3,
      "MaxLength": 64
    },
    "Remark": {
      "Type": "String",
      "Description": "The remark of instance."
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::ROCKETMQ::Instance",
      "Properties": {
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "Remark": {
          "Ref": "Remark"
        }
      }
    }
  },
  "Outputs": {
    "HttpInternalEndpoint": {
      "Description": "The internal HTTP endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HttpInternalEndpoint"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance ID created",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "TcpEndpoint": {
      "Description": "The TCP endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "TcpEndpoint"
        ]
      }
    },
    "HttpInternetEndpoint": {
      "Description": "The Internet HTTP endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HttpInternetEndpoint"
        ]
      }
    },
    "InstanceType": {
      "Description": "Instance Type",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceType"
        ]
      }
    },
    "HttpInternetSecureEndpoint": {
      "Description": "The Internet HTTPS endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HttpInternetSecureEndpoint"
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
  InstanceName:
    Type: String
    Description: >-
      The name of the instance, which contains 3 to 64 characters in Chinese or
      English.
    MinLength: 3
    MaxLength: 64
  Remark:
    Type: String
    Description: The remark of instance.
Resources:
  Instance:
    Type: 'ALIYUN::ROCKETMQ::Instance'
    Properties:
      InstanceName:
        Ref: InstanceName
      Remark:
        Ref: Remark
Outputs:
  HttpInternalEndpoint:
    Description: >-
      The internal HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HttpInternalEndpoint
  InstanceId:
    Description: Instance ID created
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  TcpEndpoint:
    Description: The TCP endpoint for the Message Queue for Apache RocketMQ instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - TcpEndpoint
  HttpInternetEndpoint:
    Description: >-
      The Internet HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HttpInternetEndpoint
  InstanceType:
    Description: Instance Type
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceType
  HttpInternetSecureEndpoint:
    Description: >-
      The Internet HTTPS endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HttpInternetSecureEndpoint
```


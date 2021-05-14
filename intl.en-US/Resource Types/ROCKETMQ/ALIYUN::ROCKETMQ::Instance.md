# ALIYUN::ROCKETMQ::Instance

ALIYUN::ROCKETMQ::Instance is used to create a Standard Edition instance.

## Syntax

```
{
  "Type": "ALIYUN::ROCKETMQ::Instance",
  "Properties": {
    "Remark": String,
    "InstanceName": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Remark|String|No|Yes|The description of the instance.|The description can be up to 128 character in length.|
|InstanceName|String|Yes|Yes|The name of the instance.|The name must be 3 to 64 characters in length, and can contain letters, digits, hyphens \(-\), and underscores \(\_\).|
|Tags|List|No|Yes|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_gor_asi_f84). |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance.
-   InstanceType: the type of the instance. If 1 is returned, the created instance is of the Standard Edition.
-   HttpInternetEndpoint: the public HTTP endpoint.
-   HttpInternetSecureEndpoint: the public HTTPS endpoint.
-   TcpEndpoint: the TCP endpoint.
-   HttpInternalEndpoint: the internal HTTP endpoint.
-   InstanceName: the name of the instance.

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
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
        "Tags": {
          "Ref": "Tags"
        },
        "Remark": {
          "Ref": "Remark"
        }
      }
    }
  },
  "Outputs": {
    "InstanceName": {
      "Description": "Instance name",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceName"
        ]
      }
    },
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
    Description: The name of the instance, which contains 3 to 64 characters in Chinese
      or English.
    MaxLength: 64
    MinLength: 3
    Type: String
  Remark:
    Description: The remark of instance.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  Instance:
    Properties:
      InstanceName:
        Ref: InstanceName
      Remark:
        Ref: Remark
      Tags:
        Ref: Tags
    Type: ALIYUN::ROCKETMQ::Instance
Outputs:
  HttpInternalEndpoint:
    Description: The internal HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      Fn::GetAtt:
      - Instance
      - HttpInternalEndpoint
  HttpInternetEndpoint:
    Description: The Internet HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      Fn::GetAtt:
      - Instance
      - HttpInternetEndpoint
  HttpInternetSecureEndpoint:
    Description: The Internet HTTPS endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      Fn::GetAtt:
      - Instance
      - HttpInternetSecureEndpoint
  InstanceId:
    Description: Instance ID created
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceId
  InstanceName:
    Description: Instance name
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceName
  InstanceType:
    Description: Instance Type
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceType
  TcpEndpoint:
    Description: The TCP endpoint for the Message Queue for Apache RocketMQ instance.
    Value:
      Fn::GetAtt:
      - Instance
      - TcpEndpoint
```

For more examples, visit [ROCKETMQ.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROCKETMQ/JSON/ROCKETMQ.json) and [ROCKETMQ.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROCKETMQ/YAML/ROCKETMQ.yml). In the examples, the ALIYUN::ROCKETMQ::Instance, ALIYUN::ROCKETMQ::Group, and ALIYUN::ROCKETMQ::Topic resource types are involved.


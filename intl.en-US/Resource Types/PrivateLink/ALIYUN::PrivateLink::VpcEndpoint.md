# ALIYUN::PrivateLink::VpcEndpoint

ALIYUN::PrivateLink::VpcEndpoint is used to create an endpoint.

## Syntax

```
{
  "Type": "ALIYUN::PrivateLink::VpcEndpoint",
  "Properties": {
    "VpcId": String,
    "EndpointName": String,
    "ServiceName": String,
    "Zone": List,
    "SecurityGroupId": List,
    "EndpointDescription": String,
    "ServiceId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcId|String|Yes|No|The VPC in which to create the endpoint.|None|
|EndpointName|String|No|Yes|The name of the endpoint.|The name must be 2 to 128 characters in length, and can contain letters, digits, hyphens \(-\), and underscores \(\_\). It must start with a letter.|
|ServiceName|String|No|No|The name of the endpoint service that is associated with the endpoint.|None|
|Zone|List|No|Yes|The list of one or more zones.|Up to 10 zones are supported.For more information, see [Zone properties](#section_kxm_hm7_qju). |
|SecurityGroupId|List|Yes|Yes|The list of one or more security groups that are associated with the endpoint elastic container instance \(ENI\). Security groups can be used to control data communication between the VPC and the endpoint ENI.|The instance can be associated with up to 10 security groups.|
|EndpointDescription|String|No|Yes|The description of the endpoint.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|ServiceId|String|No|No|The ID of the endpoint service that is associated with the endpoint.|None|

## Zone syntax

```
"Zone": [
  {
    "ZoneId": String,
    "VSwitchId": String
  }
]
```

## Zone properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ZoneId|String|Yes|No|The zone ID of the endpoint service.|None|
|VSwitchId|String|Yes|No|The ID of the vSwitch within which you want to create an ENI.|None|

## Response parameters

Fn::GetAtt

-   EndpointDomain: the domain name of the endpoint.
-   Bandwidth: the badwidth of the endpoint.
-   EndpointId: the ID of the endpoint.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "Description": "The VPC to which the endpoint belongs."
    },
    "EndpointName": {
      "Type": "String",
      "Description": "The name of the endpoint.\nThe name must be 2 to 128 characters in length and can contain digits, underscores\n(_), and hyphens (-). The name must start with a letter.",
      "MinLength": 2,
      "MaxLength": 128
    },
    "ServiceName": {
      "Type": "String",
      "Description": "The name of the endpoint service that is associated with the endpoint. One of ServiceId and ServiceName is required."
    },
    "Zone": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 10
    },
    "SecurityGroupId": {
      "Type": "Json",
      "Description": "The security group associated with the endpoint network interface. The security group can control the data communication from the VPC to the endpoint network interface.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "EndpointDescription": {
      "Type": "String",
      "Description": "The description of the endpoint.\nThe description must be 2 to 256 characters in length and cannot start with http:// or https://.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "ServiceId": {
      "Type": "String",
      "Description": "The endpoint service that is associated with the endpoint. One of ServiceId and ServiceName is required."
    }
  },
  "Resources": {
    "VpcEndpoint": {
      "Type": "ALIYUN::PrivateLink::VpcEndpoint",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "EndpointName": {
          "Ref": "EndpointName"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Zone": {
          "Ref": "Zone"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "EndpointDescription": {
          "Ref": "EndpointDescription"
        },
        "ServiceId": {
          "Ref": "ServiceId"
        }
      }
    }
  },
  "Outputs": {
    "EndpointDomain": {
      "Description": "The domain name of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointDomain"
        ]
      }
    },
    "Bandwidth": {
      "Description": "The bandwidth of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "Bandwidth"
        ]
      }
    },
    "EndpointId": {
      "Description": "The ID of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointId"
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
  VpcId:
    Type: String
    Description: The VPC to which the endpoint belongs.
  EndpointName:
    Type: String
    Description: >-
      The name of the endpoint.

      The name must be 2 to 128 characters in length and can contain digits,
      underscores

      (_), and hyphens (-). The name must start with a letter.
    MinLength: 2
    MaxLength: 128
  ServiceName:
    Type: String
    Description: >-
      The name of the endpoint service that is associated with the endpoint. One
      of ServiceId and ServiceName is required.
  Zone:
    Type: Json
    Description: ''
    MinLength: 1
    MaxLength: 10
  SecurityGroupId:
    Type: Json
    Description: >-
      The security group associated with the endpoint network interface. The
      security group can control the data communication from the VPC to the
      endpoint network interface.
    MinLength: 1
    MaxLength: 10
  EndpointDescription:
    Type: String
    Description: >-
      The description of the endpoint.

      The description must be 2 to 256 characters in length and cannot start
      with http:// or https://.
    MinLength: 2
    MaxLength: 256
  ServiceId:
    Type: String
    Description: >-
      The endpoint service that is associated with the endpoint. One of
      ServiceId and ServiceName is required.
Resources:
  VpcEndpoint:
    Type: 'ALIYUN::PrivateLink::VpcEndpoint'
    Properties:
      VpcId:
        Ref: VpcId
      EndpointName:
        Ref: EndpointName
      ServiceName:
        Ref: ServiceName
      Zone:
        Ref: Zone
      SecurityGroupId:
        Ref: SecurityGroupId
      EndpointDescription:
        Ref: EndpointDescription
      ServiceId:
        Ref: ServiceId
Outputs:
  EndpointDomain:
    Description: The domain name of the endpoint.
    Value:
      'Fn::GetAtt':
        - VpcEndpoint
        - EndpointDomain
  Bandwidth:
    Description: The bandwidth of the endpoint.
    Value:
      'Fn::GetAtt':
        - VpcEndpoint
        - Bandwidth
  EndpointId:
    Description: The ID of the endpoint.
    Value:
      'Fn::GetAtt':
        - VpcEndpoint
        - EndpointId
```


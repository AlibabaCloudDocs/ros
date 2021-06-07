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
|VpcId|String|Yes|No|The virtual private cloud \(VPC\) in which to create the endpoint.|None|
|EndpointName|String|No|Yes|The name of the endpoint.|The name must be 2 to 128 characters in length and must start with a letter. The name can contain letters, digits, hyphens \(-\), and underscores \(\_\).|
|ServiceName|String|No|No|The name of the endpoint service that is associated with the endpoint.|None|
|Zone|List|No|Yes|The list of one or more zones.|Up to 10 zones are supported. For more information, see [Zone properties](#section_kxm_hm7_qju). |
|SecurityGroupId|List|Yes|Yes|The list of one or more security groups that are associated with the elastic network interfaces \(ENIs\) for the endpoint. Security groups can be used to control data communication between the VPC and VPC and the ENIs.|The endpoint can be associated with up to 10 security groups.|
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
-   Bandwidth: the bandwidth of the endpoint.
-   EndpointId: the ID of the endpoint.
-   EndpointName: the name of the endpoint.
-   VpcId: the VPC ID of the endpoint.
-   ServiceName: the name of the endpoint service that is associated with the endpoint.
-   ServiceId: the ID of the endpoint service that is associated with the endpoint.

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
    "VpcId": {
      "Description": "The vpc ID of endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "VpcId"
        ]
      }
    },
    "EndpointDomain": {
      "Description": "The domain name of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointDomain"
        ]
      }
    },
    "EndpointName": {
      "Description": "The name of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointName"
        ]
      }
    },
    "ServiceName": {
      "Description": "The name of endpoint service that is associated with the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "ServiceName"
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
    },
    "ServiceId": {
      "Description": "The ID of endpoint service that is associated with the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "ServiceId"
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
  EndpointDescription:
    Description: 'The description of the endpoint.

      The description must be 2 to 256 characters in length and cannot start with
      http:// or https://.'
    MaxLength: 256
    MinLength: 2
    Type: String
  EndpointName:
    Description: 'The name of the endpoint.

      The name must be 2 to 128 characters in length and can contain digits, underscores

      (_), and hyphens (-). The name must start with a letter.'
    MaxLength: 128
    MinLength: 2
    Type: String
  SecurityGroupId:
    Description: The security group associated with the endpoint network interface.
      The security group can control the data communication from the VPC to the endpoint
      network interface.
    MaxLength: 10
    MinLength: 1
    Type: Json
  ServiceId:
    Description: The endpoint service that is associated with the endpoint. One of
      ServiceId and ServiceName is required.
    Type: String
  ServiceName:
    Description: The name of the endpoint service that is associated with the endpoint.
      One of ServiceId and ServiceName is required.
    Type: String
  VpcId:
    Description: The VPC to which the endpoint belongs.
    Type: String
  Zone:
    Description: ''
    MaxLength: 10
    MinLength: 1
    Type: Json
Resources:
  VpcEndpoint:
    Properties:
      EndpointDescription:
        Ref: EndpointDescription
      EndpointName:
        Ref: EndpointName
      SecurityGroupId:
        Ref: SecurityGroupId
      ServiceId:
        Ref: ServiceId
      ServiceName:
        Ref: ServiceName
      VpcId:
        Ref: VpcId
      Zone:
        Ref: Zone
    Type: ALIYUN::PrivateLink::VpcEndpoint
Outputs:
  Bandwidth:
    Description: The bandwidth of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - Bandwidth
  EndpointDomain:
    Description: The domain name of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - EndpointDomain
  EndpointId:
    Description: The ID of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - EndpointId
  EndpointName:
    Description: The name of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - EndpointName
  ServiceId:
    Description: The ID of endpoint service that is associated with the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - ServiceId
  ServiceName:
    Description: The name of endpoint service that is associated with the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - ServiceName
  VpcId:
    Description: The vpc ID of endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - VpcId
```


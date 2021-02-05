# ALIYUN::PrivateLink::VpcEndpointService

ALIYUN::PrivateLink::VpcEndpointService is used to create an endpoint service.

## Syntax

```
{
  "Type": "ALIYUN::PrivateLink::VpcEndpointService",
  "Properties": {
    "User": List,
    "ServiceDescription": String,
    "Resource": List,
    "ConnectBandwidth": Integer,
    "AutoAcceptEnabled": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|User|List|No|Yes|The whitelist of Alibaba Cloud accounts for the endpoint service.|You can add up to 20 Alibaba Cloud accounts to the whitelist.|
|ServiceDescription|String|No|Yes|The description of the endpoint service.|The description must be 2 to 256 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a digit or letter.|
|Resource|List|No|Yes|The list of one or more service resources added to the endpoint service.|You can add up to 20 service resources to the endpoint service.For more information, see [Resource properties](#section_80p_9av_3vl). |
|ConnectBandwidth|Integer|No|Yes|The default maximum bandwidth.|Valid values: 100 to 1024.Unit: Mbit/s. |
|AutoAcceptEnabled|Boolean|No|Yes|Specifies whether endpoint connection requests are automatically accepted.|Valid values:-   true: Endpoint connection requests are automatically accepted.
-   false: Endpoint connection requests are not automatically accepted. |

## Resource syntax

```
"Resource": [
  {
    "ZoneId": String,
    "ResourceId": String,
    "ResourceType": String
  }
]
```

## Resource properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ZoneId|String|Yes|No|The zone ID of the service resource.|None|
|ResourceId|String|Yes|No|The service resource added to the endpoint service.|None|
|ResourceType|String|Yes|No|The type of the service resource added to the endpoint service.|Set the value to slb, which indicates the VPC-type Server Load Balancer \(SLB\) instances that support PrivateLink.**Note:** Only SLB instances that support PrivateLink can serve as service resources for endpoint services. |

## Response parameters

Fn::GetAtt

-   ServiceName: the name of the endpoint service.
-   ServiceDomain: the domain name of the endpoint service.
-   ServiceId: the ID of the endpoint service.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "User": {
      "Type": "Json",
      "Description": "Account IDs to the whitelist of an endpoint service.",
      "MinLength": 1,
      "MaxLength": 20
    },
    "ServiceDescription": {
      "Type": "String",
      "Description": "The description for the endpoint service.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "Resource": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 20
    },
    "ConnectBandwidth": {
      "Type": "Number",
      "Description": "The default maximum bandwidth of the endpoint connection. Valid values: 100 to 1024. Unit: Mbit/s.",
      "MinValue": 100,
      "MaxValue": 1024
    },
    "AutoAcceptEnabled": {
      "Type": "Boolean",
      "Description": "Specifies whether to automatically accept endpoint connection requests. Valid values:\ntrue: automatically accepts endpoint connection requests.\nfalse: does not automatically accept endpoint connection requests.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Resources": {
    "VpcEndpointService": {
      "Type": "ALIYUN::PrivateLink::VpcEndpointService",
      "Properties": {
        "User": {
          "Ref": "User"
        },
        "ServiceDescription": {
          "Ref": "ServiceDescription"
        },
        "Resource": {
          "Ref": "Resource"
        },
        "ConnectBandwidth": {
          "Ref": "ConnectBandwidth"
        },
        "AutoAcceptEnabled": {
          "Ref": "AutoAcceptEnabled"
        }
      }
    }
  },
  "Outputs": {
    "ServiceName": {
      "Description": "The name of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "ServiceName"
        ]
      }
    },
    "ServiceDomain": {
      "Description": "The domain name of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
          "ServiceDomain"
        ]
      }
    },
    "ServiceId": {
      "Description": "The ID of the endpoint service.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointService",
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
  User:
    Type: Json
    Description: Account IDs to the whitelist of an endpoint service.
    MinLength: 1
    MaxLength: 20
  ServiceDescription:
    Type: String
    Description: The description for the endpoint service.
    MinLength: 2
    MaxLength: 256
  Resource:
    Type: Json
    Description: ''
    MinLength: 1
    MaxLength: 20
  ConnectBandwidth:
    Type: Number
    Description: >-
      The default maximum bandwidth of the endpoint connection. Valid values:
      100 to 1024. Unit: Mbit/s.
    MinValue: 100
    MaxValue: 1024
  AutoAcceptEnabled:
    Type: Boolean
    Description: >-
      Specifies whether to automatically accept endpoint connection requests.
      Valid values:

      true: automatically accepts endpoint connection requests.

      false: does not automatically accept endpoint connection requests.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
Resources:
  VpcEndpointService:
    Type: 'ALIYUN::PrivateLink::VpcEndpointService'
    Properties:
      User:
        Ref: User
      ServiceDescription:
        Ref: ServiceDescription
      Resource:
        Ref: Resource
      ConnectBandwidth:
        Ref: ConnectBandwidth
      AutoAcceptEnabled:
        Ref: AutoAcceptEnabled
Outputs:
  ServiceName:
    Description: The name of the endpoint service.
    Value:
      'Fn::GetAtt':
        - VpcEndpointService
        - ServiceName
  ServiceDomain:
    Description: The domain name of the endpoint service.
    Value:
      'Fn::GetAtt':
        - VpcEndpointService
        - ServiceDomain
  ServiceId:
    Description: The ID of the endpoint service.
    Value:
      'Fn::GetAtt':
        - VpcEndpointService
        - ServiceId 
```


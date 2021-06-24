# ALIYUN::PrivateLink::VpcEndpointServiceAttachment

ALIYUN::PrivateLink::VpcEndpointServiceAttachment is used to add a service resource to an endpoint service.

## Syntax

```
{
  "Type": "ALIYUN::PrivateLink::VpcEndpointServiceAttachment",
  "Properties": {
    "ResourceId": String,
    "ResourceType": String,
    "ServiceId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceId|String|Yes|No|The ID of the service resource.|None|
|ResourceType|String|Yes|No|The type of the service resource.|Set the value to slb. Only Server Load Balancer \(SLB\) instances that support PrivateLink and are deployed in virtual private clouds \(VPCs\) can serve as service resources.|
|ServiceId|String|Yes|No|The ID of the endpoint service to which you want to add the service resource.|None|

## Response parameters

Fn::GetAtt

-   ResourceId: the ID of the service resource.
-   ServiceId: the ID of the endpoint service that is associated with the endpoint.
-   ResourceType: the type of the service resource.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ResourceId": {
      "Type": "String",
      "Description": "The resource id. "
    },
    "ResourceType": {
      "Type": "String",
      "Description": "The resource type. "
    },
    "ServiceId": {
      "Type": "String",
      "Description": "The endpoint service that is associated with the endpoint. "
    }
  },
  "Resources": {
    "VpcEndpointServiceAttachment": {
      "Type": "ALIYUN::PrivateLink::VpcEndpointServiceAttachment",
      "Properties": {
        "ResourceId": {
          "Ref": "ResourceId"
        },
        "ResourceType": {
          "Ref": "ResourceType"
        },
        "ServiceId": {
          "Ref": "ServiceId"
        }
      }
    }
  },
  "Outputs": {
    "ResourceId": {
      "Description": "The resource id. ",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointServiceAttachment",
          "ResourceId"
        ]
      }
    },
    "ResourceType": {
      "Description": "The resource type. ",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointServiceAttachment",
          "ResourceType"
        ]
      }
    },
    "ServiceId": {
      "Description": "The endpoint service that is associated with the endpoint. ",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpointServiceAttachment",
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
  ResourceId:
    Description: 'The resource id. '
    Type: String
  ResourceType:
    Description: 'The resource type. '
    Type: String
  ServiceId:
    Description: 'The endpoint service that is associated with the endpoint. '
    Type: String
Resources:
  VpcEndpointServiceAttachment:
    Properties:
      ResourceId:
        Ref: ResourceId
      ResourceType:
        Ref: ResourceType
      ServiceId:
        Ref: ServiceId
    Type: ALIYUN::PrivateLink::VpcEndpointServiceAttachment
Outputs:
  ResourceId:
    Description: 'The resource id. '
    Value:
      Fn::GetAtt:
      - VpcEndpointServiceAttachment
      - ResourceId
  ResourceType:
    Description: 'The resource type. '
    Value:
      Fn::GetAtt:
      - VpcEndpointServiceAttachment
      - ResourceType
  ServiceId:
    Description: 'The endpoint service that is associated with the endpoint. '
    Value:
      Fn::GetAtt:
      - VpcEndpointServiceAttachment
      - ServiceId
```


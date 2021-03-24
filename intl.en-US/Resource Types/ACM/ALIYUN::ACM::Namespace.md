# ALIYUN::ACM::Namespace

ALIYUN::ACM::Namespace is used to create a namespace.

## Syntax

```
{
  "Type": "ALIYUN::ACM::Namespace",
  "Properties": {
    "Name": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|Yes|Yes|The name of the namespace.|None|

## Response parameters

Fn::GetAtt

-   NamespaceId: the ID of the namespace.
-   Endpoint: the endpoint of the namespace.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Namespace": {
      "Type": "ALIYUN::ACM::Namespace",
      "Properties": {
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Name": {
      "Type": "String",
      "Description": "Namespace name"
    }
  },
  "Outputs": {
    "Endpoint": {
      "Description": "Endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Namespace",
          "Endpoint"
        ]
      }
    },
    "NamespaceId": {
      "Description": "ID namespace",
      "Value": {
        "Fn::GetAtt": [
          "Namespace",
          "NamespaceId"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Namespace:
    Type: 'ALIYUN::ACM::Namespace'
    Properties:
      Name:
        Ref: Name
Parameters:
  Name:
    Type: String
    Description: Namespace name
Outputs:
  Endpoint:
    Description: Endpoint
    Value:
      'Fn::GetAtt':
        - Namespace
        - Endpoint
  NamespaceId:
    Description: ID namespace
    Value:
      'Fn::GetAtt':
        - Namespace
        - NamespaceId
```

For more information about the combination example of the namespace and the configuration, visit [Configuration.json](https://github.com/aliyun/ros-templates/blob/master/ResourceTemplates/ACM/JSON/Configuration.json) and [Configuration.yml](https://github.com/aliyun/ros-templates/blob/master/ResourceTemplates/ACM/YAML/Configuration.yml).


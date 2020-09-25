# ALIYUN::CR::Namespace

ALIYUN::CR::Namespace is used to create a namespace.

## Syntax

```
{
  "Type": "ALIYUN::CR::Namespace",
  "Properties": {
    "Namespace": String,
    "DefaultVisibility": String,
    "AutoCreate": Boolean
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Namespace|String|Yes|No|The name of the namespace.|The name must be 2 to 30 characters in length and can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\). The name cannot start with a hyphen \(-\) or an underscore \(\_\).|
|DefaultVisibility|String|No|Yes|The default repository type.|Valid values: -   PUBLIC
-   PRIVATE |
|AutoCreate|Boolean|No|Yes|Specifies whether to automatically create a repository.|Valid values: -   true
-   false |

## Response parameters

Fn::GetAtt

NamespaceId: the ID of the namespace.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AutoCreate": {
      "Type": "Boolean",
      "Description": "whether auto create repository",
      "AllowedValues": [
        true,
        false
      ],
      "Default": false
    },
    "DefaultVisibility": {
      "Type": "String",
      "Description": "repository default visibility, public or private",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ],
      "Default": "PRIVATE"
    },
    "Namespace": {
      "Type": "String",
      "Description": "domain name",
      "MinLength": 2,
      "MaxLength": 30
    }
  },
  "Resources": {
    "NameSpace": {
      "Type": "ALIYUN::CR::Namespace",
      "Properties": {
        "AutoCreate": {
          "Ref": "AutoCreate"
        },
        "DefaultVisibility": {
          "Ref": "DefaultVisibility"
        },
        "Namespace": {
          "Ref": "Namespace"
        }
      }
    }
  },
  "Outputs": {
    "NamespaceId": {
      "Description": "The namespace id",
      "Value": {
        "Fn::GetAtt": [
          "NameSpace",
          "NamespaceId"
        ]
      }
    }
  }
}
```


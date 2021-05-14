# ALIYUN::SAG::CloudConnectNetwork

ALIYUN::SAG::CloudConnectNetwork is used to create a Cloud Connect Network \(CCN\) instance. CNN is a device access matrix composed of Alibaba Cloud distributed Smart Access Gateways \(SAGs\). You can add multiple SAGs to a CCN instance and then attach the CCN instance to a Cloud Enterprise Network \(CEN\) instance. In this way, you can connect your local branches to Alibaba Cloud.

## Syntax

```
{
  "Type": "ALIYUN::SAG::CloudConnectNetwork",
  "Properties": {
    "Description": String,
    "IsDefault": Boolean,
    "Name": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the CCN instance.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|IsDefault|Boolean|No|No|Indicates whether the CCN instance is created by the system.|Default value: false. Valid values:-   true
-   false |
|Name|String|No|Yes|The name of the CCN instance.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with `http://` or `https://`. It can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|Tags|List|No|Yes|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_doq_eh0_2fb) section in this topic. |

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

CcnId: the ID of the CCN instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "IsDefault": {
      "Type": "Boolean",
      "Description": "Whether is created by system",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the CCN instance.\nThe description can contain 2 to 256 characters. The description cannot start with http:// or https://."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the CCN instance.\nThe name can contain 2 to 128 characters including a-z, A-Z, 0-9, chinese, underlines, and hyphens. The name must start with an English letter, but cannot start with http:// or https://."
    }
  },
  "Resources": {
    "CloudConnectNetwork": {
      "Type": "ALIYUN::SAG::CloudConnectNetwork",
      "Properties": {
        "IsDefault": {
          "Ref": "IsDefault"
        },
        "Description": {
          "Ref": "Description"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "CcnId": {
      "Description": "The ID of the CCN instance.",
      "Value": {
        "Fn::GetAtt": [
          "CloudConnectNetwork",
          "CcnId"
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
  Description:
    Description: 'The description of the CCN instance.

      The description can contain 2 to 256 characters. The description cannot start
      with http:// or https://.'
    Type: String
  IsDefault:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: Whether is created by system
    Type: Boolean
  Name:
    Description: 'The name of the CCN instance.

      The name can contain 2 to 128 characters including a-z, A-Z, 0-9, chinese, underlines,
      and hyphens. The name must start with an English letter, but cannot start with
      http:// or https://.'
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  CloudConnectNetwork:
    Properties:
      Description:
        Ref: Description
      IsDefault:
        Ref: IsDefault
      Name:
        Ref: Name
      Tags:
        Ref: Tags
    Type: ALIYUN::SAG::CloudConnectNetwork
Outputs:
  CcnId:
    Description: The ID of the CCN instance.
    Value:
      Fn::GetAtt:
      - CloudConnectNetwork
      - CcnId
```

For more examples, visit [Cen.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CEN/JSON/Cen.json) and [Cen.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CEN/YAML/Cen.yml). The ALIYUN::CEN::CenInstance, ALIYUN::CEN::CenBandwidthPackage, ALIYUN::CEN::CenBandwidthPackageAssociation, ALIYUN::CEN::CenInstanceAttachment, ALIYUN::CEN::CenBandwidthLimit, ALIYUN::CEN::RouteEntry, ALIYUN::SAG::CloudConnectNetwork, ALIYUN::SAG::GrantCcnToCen, and ALIYUN::VPC::GrantInstanceToCen resource types are involved.


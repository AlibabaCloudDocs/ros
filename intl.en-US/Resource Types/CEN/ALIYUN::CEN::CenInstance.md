# ALIYUN::CEN::CenInstance

ALIYUN::CEN::CenInstance is used to create a Cloud Enterprise Network \(CEN\) instance.

## Syntax

```
{
  "Type": "ALIYUN::CEN::CenInstance",
  "Properties": {
    "Description": String,
    "Name": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the CEN instance.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|Name|String|No|Yes|The name of the CEN instance.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. The name can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|Tags|List|No|Yes|The tags of the CEN instance.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_stb_q7p_pxx). |

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
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

CenId: The ID of the created CEN instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the instance.\nThe name can be 2-256 characters in length. It can start with an uppercase letter, lowercase letter, or Chinese character. It can contain numbers, underscores (_), and hyphens (-), but cannot start with http:// or https://."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the instance.\nThe name can be 2-128 characters in length. It can start with an uppercase letter, lowercase letter, or Chinese character. It can contain numbers, underscores (_), and hyphens (-), but cannot start with http:// or https://."
    }
  },
  "Resources": {
    "CenInstance": {
      "Type": "ALIYUN::CEN::CenInstance",
      "Properties": {
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
    "CenId": {
      "Description": "The ID of the request.",
      "Value": {
        "Fn::GetAtt": [
          "CenInstance",
          "CenId"
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
    Description: 'The description of the instance.

      The name can be 2-256 characters in length. It can start with an uppercase letter,
      lowercase letter, or Chinese character. It can contain numbers, underscores
      (_), and hyphens (-), but cannot start with http:// or https://.'
    Type: String
  Name:
    Description: 'The name of the instance.

      The name can be 2-128 characters in length. It can start with an uppercase letter,
      lowercase letter, or Chinese character. It can contain numbers, underscores
      (_), and hyphens (-), but cannot start with http:// or https://.'
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  CenInstance:
    Properties:
      Description:
        Ref: Description
      Name:
        Ref: Name
      Tags:
        Ref: Tags
    Type: ALIYUN::CEN::CenInstance
Outputs:
  CenId:
    Description: The ID of the request.
    Value:
      Fn::GetAtt:
      - CenInstance
      - CenId
```

For more examples, visit [Cen.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CEN/JSON/Cen.json) and [Cen.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CEN/YAML/Cen.yml). In the examples, the ALIYUN::CEN::CenInstance, ALIYUN::CEN::CenInstanceAttachment, ALIYUN::CEN::CenBandwidthPackage, ALIYUN::CEN::CenBandwidthLimit, ALIYUN::CEN::RouteEntry, ALIYUN::SAG::CloudConnectNetwork, ALIYUN::SAG::GrantCcnToCen, and ALIYUN::VPC::GrantInstanceToCen resources are involved.


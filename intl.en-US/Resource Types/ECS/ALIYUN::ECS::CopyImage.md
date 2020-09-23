# ALIYUN::ECS::CopyImage

ALIYUN::ECS::CopyImage is used to copy a custom image from one region to another region. You can use the image copy to create an ECS instance in another region.

## Syntax

```
{
  "Type": "ALIYUN::ECS::CopyImage",
  "Properties": {
    "Encrypted": Boolean,
    "DestinationImageName": String,
    "ImageId": String,
    "DestinationRegionId": String,
    "Tag": List,
    "DestinationDescription": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Encrypted|Boolean|No|No|Specifies whether to encrypt the image.|Default value: false. Valid values: -   true
-   false |
|DestinationImageName|String|No|No|The name of the image copy.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, colons\(:\), underscores \(\_\), and hyphens \(-\).

 Example value: FinanceJoshua. |
|ImageId|String|Yes|No|The ID of the source custom image.|Example value: m-bp1h46wfpjsjastc\*\*\*\*.|
|DestinationRegionId|String|Yes|No|The region ID of the image copy.|Example value: cn-shanghai.|
|Tag|List|No|No|The tags of the image.|For more information, see [Tag properties](#section_hi2_fxq_zym).|
|DestinationDescription|String|No|No|The description of the image copy.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

 Example value: FinanceDept. |

## Tag syntax

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|No|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

ImageId: the ID of the image copy.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DestinationRegionId": {
      "Type": "String",
      "Description": "ID of the region to where the destination custom image belongs."
    },
    "Encrypted": {
      "Type": "Boolean",
      "Description": "Whether to encrypt the image.",
      "AllowedValues": [
        "true",
        "false"
      ]
    },
    "ImageId": {
      "Type": "String",
      "Description": "ID of the source custom image."
    },
    "DestinationDescription": {
      "Type": "String",
      "Description": "The description of the destination custom image.It cannot begin with http:// or https://.  Default value: null."
    },
    "Tag": {
      "Type": "Json",
      "Description": ""
    },
    "DestinationImageName": {
      "Type": "String",
      "Description": "Name of the destination custom image.The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods (.), colons (:), underscores (_), and hyphens (-).  Default value: null."
    }
  },
  "Resources": {
    "CopyImage": {
      "Type": "ALIYUN::ECS::CopyImage",
      "Properties": {
        "DestinationRegionId": {
          "Ref": "DestinationRegionId"
        },
        "Encrypted": {
          "Ref": "Encrypted"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "DestinationDescription": {
          "Ref": "DestinationDescription"
        },
        "Tag": {
          "Ref": "Tag"
        },
        "DestinationImageName": {
          "Ref": "DestinationImageName"
        }
      }
    }
  },
  "Outputs": {
    "ImageId": {
      "Description": "ID of the source custom image.",
      "Value": {
        "Fn::GetAtt": [
          "CopyImage",
          "ImageId"
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
  DestinationRegionId:
    Type: String
    Description: ID of the region to where the destination custom image belongs.
  Encrypted:
    Type: Boolean
    Description: Whether to encrypt the image.
    AllowedValues:
      - 'true'
      - 'false'
  ImageId:
    Type: String
    Description: ID of the source custom image.
  DestinationDescription:
    Type: String
    Description: >-
      The description of the destination custom image.It cannot begin with
      http:// or https://.  Default value: null.
  Tag:
    Type: Json
    Description: ''
  DestinationImageName:
    Type: String
    Description: >-
      Name of the destination custom image.The name is a string of 2 to 128
      characters. It must begin with an English or a Chinese character. It can
      contain A-Z, a-z, Chinese characters, numbers, periods (.), colons (:),
      underscores (_), and hyphens (-).  Default value: null.
Resources:
  CopyImage:
    Type: 'ALIYUN::ECS::CopyImage'
    Properties:
      DestinationRegionId:
        Ref: DestinationRegionId
      Encrypted:
        Ref: Encrypted
      ImageId:
        Ref: ImageId
      DestinationDescription:
        Ref: DestinationDescription
      Tag:
        Ref: Tag
      DestinationImageName:
        Ref: DestinationImageName
Outputs:
  ImageId:
    Description: ID of the source custom image.
    Value:
      'Fn::GetAtt':
        - CopyImage
        - ImageId
```


# ALIYUN::ECS::CopyImage {#concept_187899 .concept}

ALIYUN::ECS::CopyImage is used to copy a custom image from one region to another region. You can use the copied image to create an ECS instance in the other region.

## Syntax {#section_hdo_w9h_3ed .section}

```language-json
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

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Encrypted|Boolean|No|No|Indicates whether to encrypt the image.|Example value: false.|
|DestinationImageName|String|No|No|The name of the destination custom image.| The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. It can contain letters, digits, colons\(:\), underscores \(\_\), and hyphens \(-\).

 Default value: null.

 Example value: FinanceJoshua.

 |
|ImageId|String|Yes|No|The ID of the copied custom image.|Example value: m-imageid1.|
|DestinationRegionId|String|Yes|No|The ID of the region where the destination custom image resides.|Example value: cn-shanghai.|
|Tag|List|No|No|The image tags.|None|
|DestinationDescription|String|No|No|The description of the destination custom image.| The description must be 2 to 256 characters in length. It cannot start with http:// or https://.

 Default value: null.

 Example value: FinanceDept.

 |

## Tag syntax {#section_7ja_b8l_hbg .section}

```language-json
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|No|No|The tag key of the custom image.|None|
|Value|String|No|No|The tag value of the custom image.|None|

## Response parameters {#section_e27_e8o_slg .section}

**Fn::GetAtt**

ImageId: the ID of the destination custom image.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CopyImage": {
      "Type": "ALIYUN::ECS::CopyImage",
      "Properties": {
        "Encrypted": {
          "Ref": "Encrypted"
        },
        "DestinationImageName": {
          "Ref": "DestinationImageName"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "DestinationRegionId": {
          "Ref": "DestinationRegionId"
        },
        "Tag": {
          "Fn::Split": [
            ",",
            {
              "Ref": "Tag"
            },
            {
              "Ref": "Tag"
            }
          ]
        },
        "DestinationDescription": {
          "Ref": "DestinationDescription"
        }
      }
    }
  },
  "Parameters": {
    "Encrypted": {
      "Type": "Boolean",
      "Description": "Whether to encrypt the image.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "DestinationImageName": {
      "Type": "String",
      "Description": "Name of the destination custom image.The name is a string of 2 to 128 characters. It must begin with a letter. It can contain A-Z, a-z, numbers, periods (.), colons (:), underscores (_), and hyphens (-).  Default value: null."
    },
    "ImageId": {
      "Type": "String",
      "Description": "ID of the source custom image."
    },
    "DestinationRegionId": {
      "Type": "String",
      "Description": "ID of the region where the destination custom image resides."
    },
    "Tag": {
      "Type": "CommaDelimitedList",
      "Description": ""
    },
    "DestinationDescription": {
      "Type": "String",
      "Description": "The description of the destination custom image. It cannot begin with http:// or https://.  Default value: null."
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


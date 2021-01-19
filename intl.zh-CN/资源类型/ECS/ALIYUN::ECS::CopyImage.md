# ALIYUN::ECS::CopyImage

ALIYUN::ECS::CopyImage类型用于将一个地域下的自定义镜像复制到其他地域。您可以在其他地域使用复制后的镜像创建ECS实例。

## 语法

```
{
  "Type": "ALIYUN::ECS::CopyImage",
  "Properties": {
    "Encrypted": Boolean,
    "DestinationImageName": String,
    "ImageId": String,
    "DestinationRegionId": String,
    "Tag": List,
    "DestinationDescription": String,
    "KMSKeyId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Encrypted|Boolean|否|否|是否加密复制后的镜像。|取值： -   true
-   false（默认值） |
|DestinationImageName|String|否|否|复制后的镜像的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）或短划线（-）。

示例值：FinanceJoshua。 |
|ImageId|String|是|否|源自定义镜像的ID。|示例值：m-bp1h46wfpjsjastc\*\*\*\*。|
|DestinationRegionId|String|是|否|复制到目标地域的ID。|示例值： cn-shanghai。|
|Tag|List|否|否|标签。|详情请参见[Tag属性](#section_hi2_fxq_zym)。|
|DestinationDescription|String|否|否|复制后的镜像的描述信息。|长度为2~256个字符，不能以`http://`和`https://`开头。

示例值： FinanceDept。 |
|KMSKeyId|String|否|否|加密镜像使用的密钥ID。|无|

## Tag语法

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|否|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

ImageId：复制后的镜像的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "KMSKeyId": {
      "Type": "String",
      "Description": "The ID of the key used to encrypt the image."
    },
    "DestinationRegionId": {
      "Type": "String",
      "Description": "ID of the region to where the destination custom image belongs."
    },
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
        "KMSKeyId": {
          "Ref": "KMSKeyId"
        },
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

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  KMSKeyId:
    Type: String
    Description: The ID of the key used to encrypt the image.
  DestinationRegionId:
    Type: String
    Description: ID of the region to where the destination custom image belongs.
  Encrypted:
    Type: Boolean
    Description: Whether to encrypt the image.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
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
      KMSKeyId:
        Ref: KMSKeyId
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


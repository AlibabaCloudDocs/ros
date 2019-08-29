# ALIYUN::ECS::CopyImage {#concept_187899 .concept}

ALIYUN::ECS::CopyImage 类型用于复制一个地域下的自定义镜像到其他地域。您可以在其他地域使用复制后的镜像创建 ECS 实例。

## 语法 {#section_hdo_w9h_3ed .section}

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

## 属性 { .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|Encrypted|Boolean|否|否|是否加密镜像。|示例值：false。|
|DestinationImageName|String|否|否|复制后的镜像的名称。| 长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空。

 示例值：FinanceJoshua。

 |
|ImageId|String|是|否|源自定义镜像的 ID。|示例值：m-imageid1。|
|DestinationRegionId|String|是|否|复制到目标地域的 ID。|示例值： cn-shanghai。|
|Tag|List|否|否|标签。|无|
|DestinationDescription|String|否|否|目标镜像的描述信息。| 长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。

 默认值：空。

 示例值： FinanceDept。

 |

## Tag语法 {#section_7ja_b8l_hbg .section}

```language-json
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag属性 { .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|Key|String|否|否|自定义镜像的标签键。|无|
|Value|String|否|否|自定义镜像的标签值。|无|

## 返回值 {#section_e27_e8o_slg .section}

**Fn::GetAtt**

ImageId：复制后的镜像的 ID。

## 示例 { .section}

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
      "Description": "Name of the destination custom image.The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods (.), colons (:), underscores (_), and hyphens (-).  Default value: null."
    },
    "ImageId": {
      "Type": "String",
      "Description": "ID of the source custom image."
    },
    "DestinationRegionId": {
      "Type": "String",
      "Description": "ID of the region to where the destination custom image belongs."
    },
    "Tag": {
      "Type": "CommaDelimitedList",
      "Description": ""
    },
    "DestinationDescription": {
      "Type": "String",
      "Description": "The description of the destination custom image.It cannot begin with http:// or https://.  Default value: null."
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


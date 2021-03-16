# ALIYUN::CEN::CenInstance

ALIYUN::CEN::CenInstance类型用于创建云企业网实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|云企业网实例的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。|
|Name|String|否|是|云企业网实例的名称。|长度为2~128个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_stb_q7p_pxx)。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

CenId：新建的云企业网实例的ID。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建云企业网实例、加载网络实例到云企业网实例中、创建带宽包、将带宽包绑定到指定的云企业网实例、设置带宽包中两个地域间的跨地域互通带宽、将加载到CEN中的VPC或VBR的路由条目发布到CEN中、创建云连接网、将云企业网实例授权给云连接网和为云企业网实例授权的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CEN/JSON/Cen.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CEN/YAML/Cen.yml)。


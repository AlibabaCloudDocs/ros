# ALIYUN::RAM::Group

ALIYUN::RAM::Group类型用于创建RAM用户组。

## 语法

```
{
  "Type": "ALIYUN::RAM::Group",
  "Properties": {
    "GroupName": String,
    "Comments": String,
    "Policies": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupName|String|是|否|用户组名称|长度为1~64个字符，可包含英文字母、数字和短划线（-）。|
|Comments|String|否|否|备注信息|长度为1~128个字符。|
|Policies|List|否|是|权限策略|详情请参见[Policies属性](#section_uro_we9_rqi)。|

## Policies语法

```
"Policies": [
  {
    "PolicyName": String,
    "PolicyDocument": {
      "Version": String,
      "Statement": [
        {
          "Effect": String,
          "Action": List,
          "Resource": List
        }
      ]
    }
  }
]            
```

## Policies属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|String|是|否|权限策略名称。|长度为1~128个字符，可包含英文字母、数字和短划线（-）。|
|PolicyDocument|Map|是|是|权限策略内容。|长度为1~2048个字符。|
|Version|String|否|否|权限策略版本。|无|
|Statement|List|否|否|权限策略具体的规则。|无|
|Action|List|否|否|权限策略针对的具体操作。|无|
|Resource|List|否|否|权限策略针对的具体资源。|无|
|Effect|String|否|否|允许或拒绝对某资源进行某种操作。|无|

## 返回值

Fn::GetAtt

GroupName：用户组名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupName": {
      "Type": "String",
      "Description": "Specifies the group name, containing up to 64 characters."
    },
    "Policies": {
      "Type": "Json",
      "Description": "Describes what actions are allowed on what resources."
    },
    "Comments": {
      "Type": "String",
      "Description": "Remark information, up to 128 characters or Chinese characters.",
      "MaxLength": 128
    }
  },
  "Resources": {
    "Group": {
      "Type": "ALIYUN::RAM::Group",
      "Properties": {
        "GroupName": {
          "Ref": "GroupName"
        },
        "Policies": {
          "Ref": "Policies"
        },
        "Comments": {
          "Ref": "Comments"
        }
      }
    }
  },
  "Outputs": {
    "GroupName": {
      "Description": "Id of ram group.",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GroupName"
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
  GroupName:
    Type: String
    Description: 'Specifies the group name, containing up to 64 characters.'
  Policies:
    Type: Json
    Description: Describes what actions are allowed on what resources.
  Comments:
    Type: String
    Description: 'Remark information, up to 128 characters or Chinese characters.'
    MaxLength: 128
Resources:
  Group:
    Type: 'ALIYUN::RAM::Group'
    Properties:
      GroupName:
        Ref: GroupName
      Policies:
        Ref: Policies
      Comments:
        Ref: Comments
Outputs:
  GroupName:
    Description: Id of ram group.
    Value:
      'Fn::GetAtt':
        - Group
        - GroupName
```


# ALIYUN::ApiGateway::Group

ALIYUN::ApiGateway::Group类型用于创建API分组。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::Group",
  "Properties": {
    "GroupName": String,
    "Description": String,
    "InstanceId": String,
    "PassthroughHeaders": String,
    "Tags": List
  }
}   
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupName|String|是|是|分组名称|名称必须唯一。 长度为4~50个字符。必须以英文字母或汉字开头。可包含英文字母、汉字、数字和下划线（\_）。 |
|Description|String|否|是|API分组描述|长度不超过180个字符。|
|InstanceId|String|否|否|API网关实例类型|取值： -   api-shared-vpc-001：专有网络。
-   api-shared-classic-001：经典网络。 |
|PassthroughHeaders|String|否|否|配置透传|取值：host。|
|Tags|List|否|是|标签|最多可以设置20个标签。 详情请参见[Tags属性](#section_g6e_w2h_g40)。 |

## Tags语法

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   SubDomain：系统给分组绑定的二级域名，用于测试API调用。
-   GroupId：API分组ID。通过系统生成，全局唯一。
-   Tags：标签。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupName": {
      "Type": "String",
      "Description": "The name of the Group.Need [4, 50] Chinese\\English\\Number characters or \"_\",and should start with Chinese/English character."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the Group, less than 180 characters."
    },
    "InstanceId": {
      "Type": "String",
      "Description": "API gateway instance ID. For example, \"api-shared-vpc-001\" means vpc instance, while \"api-shared-classic-001\" means classic instance."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to group. Max support 20 tags to add during create group. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "Group": {
      "Type": "ALIYUN::ApiGateway::Group",
      "Properties": {
        "GroupName": {
          "Ref": "GroupName"
        },
        "Description": {
          "Ref": "Description"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "SubDomain": {
      "Description": "The sub domain assigned to the Group by the system",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "SubDomain"
        ]
      }
    },
    "Tags": {
      "Description": "Tags of app",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "Tags"
        ]
      }
    },
    "GroupId": {
      "Description": "The id of the created Group resource",
      "Value": {
        "Fn::GetAtt": [
          "Group",
          "GroupId"
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
    Description: >-
      The name of the Group.Need [4, 50] Chinese\English\Number characters or
      "_",and should start with Chinese/English character.
  Description:
    Type: String
    Description: 'Description of the Group, less than 180 characters.'
  InstanceId:
    Type: String
    Description: >-
      API gateway instance ID. For example, "api-shared-vpc-001" means vpc
      instance, while "api-shared-classic-001" means classic instance.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to group. Max support 20 tags to add during create group.
      Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
Resources:
  Group:
    Type: 'ALIYUN::ApiGateway::Group'
    Properties:
      GroupName:
        Ref: GroupName
      Description:
        Ref: Description
      InstanceId:
        Ref: InstanceId
      Tags:
        Ref: Tags
Outputs:
  SubDomain:
    Description: The sub domain assigned to the Group by the system
    Value:
      'Fn::GetAtt':
        - Group
        - SubDomain
  Tags:
    Description: Tags of app
    Value:
      'Fn::GetAtt':
        - Group
        - Tags
  GroupId:
    Description: The id of the created Group resource
    Value:
      'Fn::GetAtt':
        - Group
        - GroupId
```


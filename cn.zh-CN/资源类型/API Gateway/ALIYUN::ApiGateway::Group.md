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
    "InternetEnable": Boolean,
    "VpcIntranetEnable": Boolean,
    "Tags": List
  }
}   
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupName|String|是|是|API分组名称。|名称必须唯一。 长度为4~50个字符。必须以英文字母或汉字开头。可包含英文字母、汉字、数字和下划线（\_）。 |
|Description|String|否|是|API分组描述。|长度不超过180个字符。|
|InstanceId|String|否|否|API网关实例类型。|取值： -   api-shared-vpc-001：专有网络。
-   api-shared-classic-001：经典网络。 |
|InternetEnable|Boolean|否|是|是否启用公网子域名。|取值：-   true
-   false |
|VpcIntranetEnable|Boolean|否|是|是否启用私网子域名。|取值：-   true
-   false |
|PassthroughHeaders|String|否|否|配置透传。|取值：host。|
|Tags|List|否|是|标签。|最多可以设置20个标签。更多信息，请参见[Tags属性](#section_g6e_w2h_g40)。 |

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

-   SubDomain：系统给API分组绑定的二级域名，用于测试API调用情况。
-   GroupId：API分组ID。通过系统生成，全局唯一。
-   Tags：标签。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InternetEnable": {
      "Type": "Boolean",
      "Description": "Enable or disable internet subdomain. True for enable. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
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
    "VpcIntranetEnable": {
      "Type": "Boolean",
      "Description": "Enable or disable VPC intranet subdomain. True for enable. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to group. Max support 20 tags to add during create group. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "PassthroughHeaders": {
      "Type": "String",
      "Description": "Pass through headers setting. values:\nhost: pass through host headers"
    }
  },
  "Resources": {
    "Group": {
      "Type": "ALIYUN::ApiGateway::Group",
      "Properties": {
        "InternetEnable": {
          "Ref": "InternetEnable"
        },
        "GroupName": {
          "Ref": "GroupName"
        },
        "Description": {
          "Ref": "Description"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "VpcIntranetEnable": {
          "Ref": "VpcIntranetEnable"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PassthroughHeaders": {
          "Ref": "PassthroughHeaders"
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
  InternetEnable:
    Type: Boolean
    Description: 'Enable or disable internet subdomain. True for enable. '
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
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
  VpcIntranetEnable:
    Type: Boolean
    Description: 'Enable or disable VPC intranet subdomain. True for enable. '
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Tags:
    Type: Json
    Description: >-
      Tags to attach to group. Max support 20 tags to add during create group.
      Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  PassthroughHeaders:
    Type: String
    Description: |-
      Pass through headers setting. values:
      host: pass through host headers
Resources:
  Group:
    Type: 'ALIYUN::ApiGateway::Group'
    Properties:
      InternetEnable:
        Ref: InternetEnable
      GroupName:
        Ref: GroupName
      Description:
        Ref: Description
      InstanceId:
        Ref: InstanceId
      VpcIntranetEnable:
        Ref: VpcIntranetEnable
      Tags:
        Ref: Tags
      PassthroughHeaders:
        Ref: PassthroughHeaders
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


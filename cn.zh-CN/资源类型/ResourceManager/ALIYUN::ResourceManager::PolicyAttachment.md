# ALIYUN::ResourceManager::PolicyAttachment

ALIYUN::ResourceManager::PolicyAttachment类型用于为指定对象添加权限策略，即授权。完成授权后，被授权对象将获得当前资源组或阿里云账号内资源的操作权限。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::PolicyAttachment",
  "Properties": {
    "PolicyType": String,
    "ResourceGroupId": String,
    "PolicyName": String,
    "PrincipalName": String,
    "PrincipalType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyType|String|是|否|权限策略类型。|取值-   Custom：自定义策略。
-   System：系统策略。 |
|ResourceGroupId|String|是|否|资源组ID或阿里云账号ID。|指定要在哪个资源组或阿里云账号中进行授权。|
|PolicyName|String|是|否|权限策略名称。|长度为1~128个字符，可包含英文字母、数字和短划线（-）。|
|PrincipalName|String|是|否|被授权对象名称。|无|
|PrincipalType|String|是|否|被授权对象类型。|取值：-   IMSUser：RAM用户。
-   IMSGroup：RAM用户组。
-   ServiceRole：RAM角色。 |

## 返回值

Fn::GetAtt

-   PolicyType：被授权对象类型。
-   Description：权限策略说明。
-   ResourceGroupId：资源组ID或阿里云账号ID。指定要在哪个资源组或阿里云账号中进行授权。
-   AttachDate：授权时间。
-   PolicyName：权限策略名称。
-   PrincipalName：被授权对象名称。
-   PrincipalType：被授权对象类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PolicyType": {
      "Type": "String",
      "Description": "The type of the policy"
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group or the ID of the Alibaba Cloud account to which the resource group belongs."
    },
    "PolicyName": {
      "Type": "String",
      "Description": "The name of the policy"
    },
    "PrincipalName": {
      "Type": "String",
      "Description": "The name of the object to which you want to attach the policy"
    },
    "PrincipalType": {
      "Type": "String",
      "Description": "The type of the object to which you want to attach the policy. Valid values: IMSUser: RAM user, IMSGroup: RAM user group, ServiceRole: RAM role"
    }
  },
  "Resources": {
    "ResourceManagerPolicyAttachment": {
      "Type": "ALIYUN::ResourceManager::PolicyAttachment",
      "Properties": {
        "PolicyType": {
          "Ref": "PolicyType"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "PolicyName": {
          "Ref": "PolicyName"
        },
        "PrincipalName": {
          "Ref": "PrincipalName"
        },
        "PrincipalType": {
          "Ref": "PrincipalType"
        }
      }
    }
  },
  "Outputs": {
    "PolicyType": {
      "Description": "The type of the policy",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "PolicyType"
        ]
      }
    },
    "Description": {
      "Description": "Policy description",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "Description"
        ]
      }
    },
    "ResourceGroupId": {
      "Description": "The ID of the resource group or the ID of the Alibaba Cloud account to which the resource group belongs.",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "ResourceGroupId"
        ]
      }
    },
    "AttachDate": {
      "Description": "Authorization time",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "AttachDate"
        ]
      }
    },
    "PolicyName": {
      "Description": "The name of the policy",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "PolicyName"
        ]
      }
    },
    "PrincipalName": {
      "Description": "The name of the object to which you want to attach the policy",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "PrincipalName"
        ]
      }
    },
    "PrincipalType": {
      "Description": "The type of the object to which you want to attach the policy. Valid values: IMSUser: RAM user, IMSGroup: RAM user group, ServiceRole: RAM role",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerPolicyAttachment",
          "PrincipalType"
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
  PolicyName:
    Description: The name of the policy
    Type: String
  PolicyType:
    Description: The type of the policy
    Type: String
  PrincipalName:
    Description: The name of the object to which you want to attach the policy
    Type: String
  PrincipalType:
    Description: 'The type of the object to which you want to attach the policy. Valid
      values: IMSUser: RAM user, IMSGroup: RAM user group, ServiceRole: RAM role'
    Type: String
  ResourceGroupId:
    Description: The ID of the resource group or the ID of the Alibaba Cloud account
      to which the resource group belongs.
    Type: String
Resources:
  ResourceManagerPolicyAttachment:
    Properties:
      PolicyName:
        Ref: PolicyName
      PolicyType:
        Ref: PolicyType
      PrincipalName:
        Ref: PrincipalName
      PrincipalType:
        Ref: PrincipalType
      ResourceGroupId:
        Ref: ResourceGroupId
    Type: ALIYUN::ResourceManager::PolicyAttachment
Outputs:
  AttachDate:
    Description: Authorization time
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - AttachDate
  Description:
    Description: Policy description
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - Description
  PolicyName:
    Description: The name of the policy
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - PolicyName
  PolicyType:
    Description: The type of the policy
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - PolicyType
  PrincipalName:
    Description: The name of the object to which you want to attach the policy
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - PrincipalName
  PrincipalType:
    Description: 'The type of the object to which you want to attach the policy. Valid
      values: IMSUser: RAM user, IMSGroup: RAM user group, ServiceRole: RAM role'
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - PrincipalType
  ResourceGroupId:
    Description: The ID of the resource group or the ID of the Alibaba Cloud account
      to which the resource group belongs.
    Value:
      Fn::GetAtt:
      - ResourceManagerPolicyAttachment
      - ResourceGroupId
```


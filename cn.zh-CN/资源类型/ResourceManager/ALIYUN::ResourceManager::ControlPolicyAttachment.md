# ALIYUN::ResourceManager::ControlPolicyAttachment

ALIYUN::ResourceManager::ControlPolicyAttachment类型用于绑定自定义管控策略。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::ControlPolicyAttachment",
  "Properties": {
    "TargetId": String,
    "PolicyId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TargetId|String|是|否|目标节点。|取值：-   Root ID：为Root节点绑定自定义策略。
-   资源夹ID：为资源夹绑定自定义策略。
-   成员账号UID：为成员账号绑定自定义策略。 |
|PolicyId|String|是|否|管控策略ID。|无|

## 返回值

Fn::GetAtt

-   PolicyType：管控策略类型。
-   Description：管控策略描述。
-   AttachDate：绑定管控策略的时间。
-   PolicyName：管控策略名称。
-   TargetId：目标节点。
-   PolicyId：管控策略ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TargetId": {
      "Type": "String",
      "Description": "TargetId"
    },
    "PolicyId": {
      "Type": "String",
      "Description": "PolicyId"
    }
  },
  "Resources": {
    "ResourceManagerControlPolicyAttachment": {
      "Type": "ALIYUN::ResourceManager::ControlPolicyAttachment",
      "Properties": {
        "TargetId": {
          "Ref": "TargetId"
        },
        "PolicyId": {
          "Ref": "PolicyId"
        }
      }
    }
  },
  "Outputs": {
    "PolicyType": {
      "Description": "PolicyType",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicyAttachment",
          "PolicyType"
        ]
      }
    },
    "Description": {
      "Description": "Description",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicyAttachment",
          "Description"
        ]
      }
    },
    "AttachDate": {
      "Description": "AttachDate",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicyAttachment",
          "AttachDate"
        ]
      }
    },
    "PolicyName": {
      "Description": "PolicyName",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicyAttachment",
          "PolicyName"
        ]
      }
    },
    "TargetId": {
      "Description": "TargetId",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicyAttachment",
          "TargetId"
        ]
      }
    },
    "PolicyId": {
      "Description": "PolicyId",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicyAttachment",
          "PolicyId"
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
  PolicyId:
    Description: PolicyId
    Type: String
  TargetId:
    Description: TargetId
    Type: String
Resources:
  ResourceManagerControlPolicyAttachment:
    Properties:
      PolicyId:
        Ref: PolicyId
      TargetId:
        Ref: TargetId
    Type: ALIYUN::ResourceManager::ControlPolicyAttachment
Outputs:
  AttachDate:
    Description: AttachDate
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicyAttachment
      - AttachDate
  Description:
    Description: Description
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicyAttachment
      - Description
  PolicyId:
    Description: PolicyId
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicyAttachment
      - PolicyId
  PolicyName:
    Description: PolicyName
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicyAttachment
      - PolicyName
  PolicyType:
    Description: PolicyType
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicyAttachment
      - PolicyType
  TargetId:
    Description: TargetId
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicyAttachment
      - TargetId
```


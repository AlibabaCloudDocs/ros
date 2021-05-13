# ALIYUN::ResourceManager::ControlPolicy

ALIYUN::ResourceManager::ControlPolicy类型用于创建自定义管控策略。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::ControlPolicy",
  "Properties": {
    "Description": String,
    "PolicyDocument": String,
    "ControlPolicyName": String,
    "EffectScope": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|管控策略描述。|长度为1~1024个字符，必须以英文字母开头。可包含英文字母、数字、下划线（\_）和短划线（-）。|
|PolicyDocument|String|是|是|管控策略内容。|最大长度为2048个字符。更多信息，请参见[管控策略语言]()和[自定义管控策略示例]()。 |
|ControlPolicyName|String|是|是|管控策略名称。|长度为1~128个字符，必须以英文字母开头，可包含英文字母、数字和短划线（-）。|
|EffectScope|String|是|否|管控策略的生效范围。|取值：RAM，表示该管控策略仅针对RAM用户或RAM角色生效。|

## 返回值

Fn::GetAtt

-   PolicyType：管控策略类型。
-   Description：管控策略描述。
-   AttachmentCount：管控策略被引用的次数。
-   PolicyDocument：管控策略内容。
-   ControlPolicyName：管控策略名称。
-   EffectScope：管控策略的生效范围。
-   PolicyId：管控策略ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description"
    },
    "PolicyDocument": {
      "Type": "String",
      "Description": "PolicyDocument"
    },
    "ControlPolicyName": {
      "Type": "String",
      "Description": "PolicyName"
    },
    "EffectScope": {
      "Type": "String",
      "Description": "EffectScope"
    }
  },
  "Resources": {
    "ResourceManagerControlPolicy": {
      "Type": "ALIYUN::ResourceManager::ControlPolicy",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "PolicyDocument": {
          "Ref": "PolicyDocument"
        },
        "ControlPolicyName": {
          "Ref": "ControlPolicyName"
        },
        "EffectScope": {
          "Ref": "EffectScope"
        }
      }
    }
  },
  "Outputs": {
    "PolicyType": {
      "Description": "PolicyType",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
          "PolicyType"
        ]
      }
    },
    "Description": {
      "Description": "Description",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
          "Description"
        ]
      }
    },
    "AttachmentCount": {
      "Description": "AttachmentCount",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
          "AttachmentCount"
        ]
      }
    },
    "PolicyDocument": {
      "Description": "PolicyDocument",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
          "PolicyDocument"
        ]
      }
    },
    "ControlPolicyName": {
      "Description": "PolicyName",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
          "ControlPolicyName"
        ]
      }
    },
    "EffectScope": {
      "Description": "EffectScope",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
          "EffectScope"
        ]
      }
    },
    "PolicyId": {
      "Description": "PolicyId",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerControlPolicy",
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
  ControlPolicyName:
    Description: PolicyName
    Type: String
  Description:
    Description: Description
    Type: String
  EffectScope:
    Description: EffectScope
    Type: String
  PolicyDocument:
    Description: PolicyDocument
    Type: String
Resources:
  ResourceManagerControlPolicy:
    Properties:
      ControlPolicyName:
        Ref: ControlPolicyName
      Description:
        Ref: Description
      EffectScope:
        Ref: EffectScope
      PolicyDocument:
        Ref: PolicyDocument
    Type: ALIYUN::ResourceManager::ControlPolicy
Outputs:
  AttachmentCount:
    Description: AttachmentCount
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - AttachmentCount
  ControlPolicyName:
    Description: PolicyName
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - ControlPolicyName
  Description:
    Description: Description
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - Description
  EffectScope:
    Description: EffectScope
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - EffectScope
  PolicyDocument:
    Description: PolicyDocument
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - PolicyDocument
  PolicyId:
    Description: PolicyId
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - PolicyId
  PolicyType:
    Description: PolicyType
    Value:
      Fn::GetAtt:
      - ResourceManagerControlPolicy
      - PolicyType
```


# ALIYUN::RAM::ManagedPolicy {#concept_48365_zh .concept}

ALIYUN::RAM::ManagedPolicy 类型用于创建 RAM 管理策略。

## 语法 {#section_jvv_krz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::ManagedPolicy",
  "Properties": {
    "PolicyName": String,
    "Description": String,
    "PolicyDocument": Map,
    "Users": List,
    "Groups": List,
    "Roles": List
  }
}
```

## 属性 {#section_stf_mrz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|string|是|否|指定策略名称。|最长 128 个字符。|
|Description|string|否|否|指定策略描述。|最长 1024 个字符。|
|PolicyDocument|map|否|否|指定策略详细定义。|无|
|Users|list|否|否|指定适用此策略的用户。|无|
|Groups|list|否|否|指定适用此策略的群组。|无|
|Roles|list|否|否|指定适用此策略的角色。|无|
|PolicyDocumentUnchecked|map|否|否|描述允许在哪些资源上执行哪些操作的策略文档。如果指定，PolicyDocument将被忽略。|无|

## PolicyDocument 语法 { .section}

```language-json
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
```

## PolicyDocument 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Version|string|否|否|指定策略版本。|无|
|Statement|list|否|否|指定策略具体的规则。|无|
|Action|list|否|否|指定策略针对的具体操作。|无|
|Resource|list|否|否|指定策略针对的具体资源。|无|
|Effect|string|否|否|指定允许或拒绝对 Resource 中定义的资源进行 Action 定义的操作。|无|

## 返回值 {#section_trw_5rz_lfb .section}

**Fn::GetAtt**

PolicyName：策略名称。

## 示例 {#section_xr5_wrz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RamPolicy": {
      "Type": "ALIYUN::RAM::ManagedPolicy",
      "Properties": {
        "PolicyName": "RosTest",
        "Description": "createdByRos",
        "PolicyDocument": {
          "Version": "1",
          "Statement": [
            {
              "Effect": "Allow",
              "Action": [ "oss:*" ],
              "Resource": ["acs:oss:*:*:*"]
            }
          ]
        },
        "Roles": ["RosRole"],
        "Groups": ["RosGroup"],
        "Users": ["RosUser"]
      }
    }
  },
  "Outputs": {
    "PolicyName": {
      "Value": {
        "Fn::GetAtt": ["RamPolicy","PolicyName"]
      }
    }
  }
}
```


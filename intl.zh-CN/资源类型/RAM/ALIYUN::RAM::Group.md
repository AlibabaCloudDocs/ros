# ALIYUN::RAM::Group {#concept_48361_zh .concept}

ALIYUN::RAM::Group 类型用于创建 RAM 用户群组。

## 语法 {#section_hpm_dgz_lfb .section}

```language-json
{
  "Type": "ALIYUN::RAM::Group",
  "Properties": {
    "GroupName": String,
    "Comments": String,
    "Policies": List
  }
}
```

## 属性 {#section_tcr_2gz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupName|string|是|否|群组名。|长度为 1-64 个字符，允许英文字母、数字，和连字符（-）。|
|Comments|string|否|否|群组备注。|备注最长 128 个字符。|
|Policies|list|否|否|群组策略。|无。|

## Policies 语法 { .section}

```language-json
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

## Policies 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|string|是|否|指定策略名称。|最长 128 个汉字或字符。|
|PolicyDocument|map|否|否|指定策略详细描述。|无|
|Version|string|否|否|指定策略版本。|无|
|Statement|list|否|否|指定策略具体的规则。|无|
|Action|list|否|否|指定策略针对的具体操作。|无|
|Resource|list|否|否|指定策略针对的具体资源。|无|
|Effect|string|否|否|允许或拒绝对某资源进行某种操作。|无|

## 返回值 {#section_ugh_lgz_lfb .section}

**Fn::GetAtt**

GroupName：群组名称。

## 示例 {#section_pbt_lgz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RamGroup": {
      "Type": "ALIYUN::RAM::Group",
      "Properties": {
      "GroupName": "RosTestGroup",
      "Comments": "createdByRos",
      "Policies": [
        {
          "PolicyName": "RosPolicy",
          "PolicyDocument": {
          "Version": "1",
          "Statement": [
            {
              "Effect": "Allow",
              "Action": [ "oss:*" ],
              "Resource": ["acs:oss:*:*:*"]
            }
          ]
        }
      ]
    }
  },
  "Outputs": {
    "GroupName": {
      "Value": {"Fn::GetAtt": ["RamGroup", "GroupName"]}
    }
  }
}			
```


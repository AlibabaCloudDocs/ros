# ALIYUN::MNS::Topic {#concept_188197 .concept}

ALIYUN::MNS::Topic类型用于发布消息的目的地。

## 语法 {#section_eqq_40b_m0n .section}

```language-json
{
  "Type": "ALIYUN::MNS::Topic",
  "Properties": {
    "LoggingEnabled": Boolean,
    "TopicName": String,
    "MaximumMessageSize": Integer
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TopicName|String|是|否|主题名称。| 同一账号同一Region下，主题名称不能重复，必须以英文字母开头，剩余名称可以是英文，数字，横划线，长度不超过256个字符。

 |
|MaximumMessageSize|Integer|否|否|发送到该Queue的消息体的最大长度，单位为Byte。|1024\(1KB\)-65536（64KB）范围内的某个整数值，默认值为65536（64KB）。|
|LoggingEnabled|Boolean|否|否|是否开启日志管理功能，True表示启用，False表示停用。|可选值：True/False，默认为False。|

## 返回值 {#section_1sg_fg0_ehd .section}

**Fn::GetAtt**

TopicUrl：所创建的主题URL。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Topic": {
      "Type": "ALIYUN::MNS::Topic",
      "Properties": {
        "TopicName": "test",
        "MaximumMessageSize": 2048,
        "LoggingEnabled": true
      }
    }
  },
  "Outputs": {
    "TopicUrl": {
      "Value": { "Fn::GetAtt": ["Topic", "TopicUrl"] }
    }
  }
}
```


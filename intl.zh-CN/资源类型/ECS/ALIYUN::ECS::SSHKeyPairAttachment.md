# ALIYUN::ECS::SSHKeyPairAttachment

ALIYUN::ECS::SSHKeyPairAttachment类型用于绑定SSH密钥对到ECS实例。

## 语法

```
{
  "Type": "ALIYUN::ECS::SSHKeyPairAttachment",
  "Properties": {
    "InstanceIds": List,
    "KeyPairName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceIds|List|是|是|要绑定的ECS实例ID列表|ID之间用英文逗号（,）分隔。 只支持Linux系统实例。|
|KeyPairName|String|是|否|SSH密钥对的名称|无|

## 返回值

Fn::GetAtt

无。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SSHKeyPairAttachment": {
      "Type": "ALIYUN::ECS::SSHKeyPairAttachment",
      "Properties": {
        "KeyPairName": "ssh_key_pai****",
        "InstanceIds": [
          'i-2zeiofnh20hj8fej****',
          'i-2zebt3kfvxm28y9o****'
        ]
      }
    }
  }
}
```


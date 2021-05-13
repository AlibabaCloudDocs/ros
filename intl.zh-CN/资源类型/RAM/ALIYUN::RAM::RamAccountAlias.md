# ALIYUN::RAM::RamAccountAlias

ALIYUN::RAM::RamAccountAlias类型用于创建账号别名。

## 语法

```
{
  "Type": "ALIYUN::RAM::RamAccountAlias",
  "Properties": {
    "AccountAlias": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AccountAlias|String|是|是|账号别名。|长度为3~32个字符，不能以短划线（-）开头或结尾，且不能有两个连续的短划线（-）。可包含小写英文字母、数字和短划线（-）。|

## 返回值

Fn::GetAtt

AccountAlias：账号别名。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AccountAlias": {
      "Type": "String",
      "Description": "The alias of the Alibaba Cloud account.\nThe alias must be 3 to 32 characters in length, and can contain lowercase letters,\ndigits, and hyphens (-).\nNote It cannot start or end with a hyphen (-), and cannot contain consecutive hyphens (-).",
      "AllowedPattern": "^(?!-)([a-z0-9]+|-(?!-))+(?!-)$",
      "MinLength": 3,
      "MaxLength": 32
    }
  },
  "Resources": {
    "RamAccountAlias": {
      "Type": "ALIYUN::RAM::RamAccountAlias",
      "Properties": {
        "AccountAlias": {
          "Ref": "AccountAlias"
        }
      }
    }
  },
  "Outputs": {
    "AccountAlias": {
      "Description": "The alias of the Alibaba Cloud account.",
      "Value": {
        "Fn::GetAtt": [
          "RamAccountAlias",
          "AccountAlias"
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
  AccountAlias:
    AllowedPattern: ^(?!-)([a-z0-9]+|-(?!-))+(?!-)$
    Description: 'The alias of the Alibaba Cloud account.

      The alias must be 3 to 32 characters in length, and can contain lowercase letters,

      digits, and hyphens (-).

      Note It cannot start or end with a hyphen (-), and cannot contain consecutive
      hyphens (-).'
    MaxLength: 32
    MinLength: 3
    Type: String
Resources:
  RamAccountAlias:
    Properties:
      AccountAlias:
        Ref: AccountAlias
    Type: ALIYUN::RAM::RamAccountAlias
Outputs:
  AccountAlias:
    Description: The alias of the Alibaba Cloud account.
    Value:
      Fn::GetAtt:
      - RamAccountAlias
      - AccountAlias
```


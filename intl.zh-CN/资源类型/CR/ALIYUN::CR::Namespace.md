# ALIYUN::CR::Namespace

ALIYUN::CR::Namespace类型用于创建一个新的命名空间。

## 语法

```
{
  "Type": "ALIYUN::CR::Namespace",
  "Properties": {
    "Namespace": String,
    "DefaultVisibility": String,
    "AutoCreate": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Namespace|String|是|否|命名空间名称。|长度为2~30个字符。不能以短划线（-）和下划线（\_）开头。可包含小写字母、数字、短划线（-）和下划线（\_）。|
|DefaultVisibility|String|否|是|默认的仓库属性。|取值： -   PUBLIC：公开。
-   PRIVATE：私有。 |
|AutoCreate|Boolean|否|是|是否自动创建仓库。|取值： -   true
-   false |

## 返回值

Fn::GetAtt

NamespaceId：命名空间ID。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AutoCreate": {
      "Type": "Boolean",
      "Description": "whether auto create repository",
      "AllowedValues": [
        true,
        false
      ],
      "Default": false
    },
    "DefaultVisibility": {
      "Type": "String",
      "Description": "repository default visibility, public or private",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ],
      "Default": "PRIVATE"
    },
    "Namespace": {
      "Type": "String",
      "Description": "domain name",
      "MinLength": 2,
      "MaxLength": 30
    }
  },
  "Resources": {
    "NameSpace": {
      "Type": "ALIYUN::CR::Namespace",
      "Properties": {
        "AutoCreate": {
          "Ref": "AutoCreate"
        },
        "DefaultVisibility": {
          "Ref": "DefaultVisibility"
        },
        "Namespace": {
          "Ref": "Namespace"
        }
      }
    }
  },
  "Outputs": {
    "NamespaceId": {
      "Description": "The namespace id",
      "Value": {
        "Fn::GetAtt": [
          "NameSpace",
          "NamespaceId"
        ]
      }
    }
  }
}
```


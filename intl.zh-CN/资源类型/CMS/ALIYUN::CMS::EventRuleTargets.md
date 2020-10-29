# ALIYUN::CMS::EventRuleTargets

ALIYUN::CMS::EventRuleTargets类型用于添加或者修改规则的发送目标。

## 语法

```
{
  "Type": "ALIYUN::CMS::EventRuleTargets",
  "Properties": {
    "FcParameters": List,
    "WebhookParameters": List,
    "MnsParameters": List,
    "ContactParameters": List,
    "RuleName": String,
    "SlsParameters": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FcParameters|List|否|是|函数计算相关参数。|列表最大长度为5。详情请参见[FcParameters属性](#section_j2r_zju_rgp)。 |
|WebhookParameters|List|否|是|WebHook参数。|列表最大长度为5。详情请参见[WebhookParameters属性](#section_hf2_7jv_68i)。 |
|MnsParameters|List|否|是|消息服务相关参数。|列表最大长度为5。详情请参见[MnsParameters属性](#section_1c6_h1c_atl)。 |
|ContactParameters|List|否|是|发送报警相关参数。|详情请参见[ContactParameters属性](#section_jc0_omu_zdi)。|
|RuleName|String|是|否|报警规则名称。|无|
|SlsParameters|List|否|是|日志服务相关参数。|列表最大长度为5。详情请参见[SlsParameters属性](#section_skk_awy_dwl)。 |

## FcParameters语法

```
"FcParameters": [
  {
    "Region": String,
    "ServiceName": String,
    "Id": String,
    "FunctionName": String
  }
]
```

## FcParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Region|String|否|是|函数服务对应的地域。|无|
|ServiceName|String|否|是|函数计算服务的服务名称。|无|
|Id|String|否|是|添加或修改规则的对象ID。|无|
|FunctionName|String|否|是|函数名称。|无|

## WebhookParameters语法

```
"WebhookParameters": [
  {
    "Url": String,
    "Protocol": String,
    "Id": String,
    "Method": String
  }
]
```

## WebhookParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Url|String|否|是|回调的URL。|无|
|Protocol|String|否|是|协议名。|无|
|Id|String|否|是|添加或修改规则的对象ID。|无|
|Method|String|否|是|HTTP回调的请求方法。|取值：-   GET
-   POST |

## MnsParameters语法

```
"MnsParameters": [
  {
    "Queue": String,
    "Region": String,
    "Id": String
  }
]
```

## MnsParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Queue|String|否|是|队列名称。|无|
|Region|String|否|是|消息服务的地域。|无|
|Id|String|否|是|添加或修改规则的对象ID。|无|

## ContactParameters语法

```
"ContactParameters": [
  {
    "ContactGroupName": String,
    "Id": String,
    "Level": String
  }
]
```

## ContactParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ContactGroupName|String|否|是|报警联系人分组名称。|无|
|Id|String|否|是|添加或修改规则的对象ID。|无|
|Level|String|否|是|报警通知级别。|取值：

-   2
-   3
-   4

通知方式：钉钉、Email。 |

## SlsParameters语法

```
"SlsParameters": [
  {
    "Project": String,
    "LogStore": String,
    "Region": String,
    "Id": String
  }
]
```

## SlsParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|否|是|日志服务对应的项目。|无|
|LogStore|String|否|是|日志服务对应的日志库。|无|
|Region|String|否|是|日志服务对应的地域。|无|
|Id|String|否|是|添加或修改规则的对象ID。|无|

## 返回值

Fn::GetAtt

无

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "EventRuleTargets": {
      "Type": "ALIYUN::CMS::EventRuleTargets",
      "Properties": {
        "SlsParameters": {
          "Ref": "SlsParameters"
        },
        "WebhookParameters": {
          "Ref": "WebhookParameters"
        },
        "MnsParameters": {
          "Ref": "MnsParameters"
        },
        "ContactParameters": {
          "Ref": "ContactParameters"
        },
        "RuleName": {
          "Ref": "RuleName"
        },
        "FcParameters": {
          "Ref": "FcParameters"
        }
      }
    }
  },
  "Parameters": {
    "SlsParameters": {
      "Type": "Json",
      "Description": "Parameters of SLS."
    },
    "WebhookParameters": {
      "Type": "Json",
      "Description": "Parameters of WebHook."
    },
    "MnsParameters": {
      "Type": "Json",
      "Description": "Parameters of MNS."
    },
    "ContactParameters": {
      "Type": "Json",
      "Description": "Parameters of Contact."
    },
    "RuleName": {
      "Type": "String",
      "Description": "The name of the alert rule."
    },
    "FcParameters": {
      "Type": "Json",
      "Description": "Parameters of FC."
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  EventRuleTargets:
    Type: ALIYUN::CMS::EventRuleTargets
    Properties:
      SlsParameters:
        Ref: SlsParameters
      WebhookParameters:
        Ref: WebhookParameters
      MnsParameters:
        Ref: MnsParameters
      ContactParameters:
        Ref: ContactParameters
      RuleName:
        Ref: RuleName
      FcParameters:
        Ref: FcParameters
Parameters:
  SlsParameters:
    Type: Json
    Description: Parameters of SLS.
  WebhookParameters:
    Type: Json
    Description: Parameters of WebHook.
  MnsParameters:
    Type: Json
    Description: Parameters of MNS.
  ContactParameters:
    Type: Json
    Description: Parameters of Contact.
  RuleName:
    Type: String
    Description: The name of the alert rule.
  FcParameters:
    Type: Json
    Description: Parameters of FC.      
```


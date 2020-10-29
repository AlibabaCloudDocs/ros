# ALIYUN::CMS::EventRuleTargets

ALIYUN::CMS::EventRuleTargets is used to add or modify the targets to which alert notifications are sent based on an event-triggered alert rule.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|FcParameters|List|No|Yes|The list of Function Compute parameters.|The list can contain a maximum of five parameters.For more information, see [FcParameters properties](#section_j2r_zju_rgp). |
|WebhookParameters|List|No|Yes|The list of Webhook parameters.|The list can contain a maximum of five parameters.For more information, see [WebhookParameters properties](#section_hf2_7jv_68i). |
|MnsParameters|List|No|Yes|The list of Message Service \(MNS\) parameters.|The list can contain a maximum of five parameters.For more information, see [MnsParameters properties](#section_1c6_h1c_atl). |
|ContactParameters|List|No|Yes|The list of contact parameters.|For more information, see [ContactParameters properties](#section_jc0_omu_zdi).|
|RuleName|String|Yes|No|The name of the event-triggered alert rule.|None|
|SlsParameters|List|No|Yes|The list of Log Service parameters.|The list can contain a maximum of five parameters.For more information, see [SlsParameters properties](#section_skk_awy_dwl). |

## FcParameters syntax

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

## FcParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Region|String|No|Yes|The region where the Function Compute service is deployed.|None|
|ServiceName|String|No|Yes|The name of the Function Compute service.|None|
|Id|String|No|Yes|The ID of the resource for which to add or modify the targets based on the event-triggered alert rule.|None|
|FunctionName|String|No|Yes|The name of the function.|None|

## WebhookParameters syntax

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

## WebhookParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Url|String|No|Yes|The callback URL.|None|
|Protocol|String|No|Yes|The name of the protocol.|None|
|Id|String|No|Yes|The ID of the resource for which to add or modify the targets based on the event-triggered alert rule.|None|
|Method|String|No|Yes|The request method of the HTTP callback.|Valid values:-   GET
-   POST |

## MnsParameters syntax

```
"MnsParameters": [
  {
    "Queue": String,
    "Region": String,
    "Id": String
  }
]
```

## MnsParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Queue|String|No|Yes|The name of the MNS queue.|None|
|Region|String|No|Yes|The region where MNS is deployed.|None|
|Id|String|No|Yes|The ID of the resource for which to add or modify the targets based on the event-triggered alert rule.|None|

## ContactParameters syntax

```
"ContactParameters": [
  {
    "ContactGroupName": String,
    "Id": String,
    "Level": String
  }
]
```

## ContactParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ContactGroupName|String|No|Yes|The name of the alert contact group.|None|
|Id|String|No|Yes|The ID of the resource for which to add or modify the targets based on the event-triggered alert rule.|None|
|Level|String|No|Yes|The level of the alert notification.|Valid values:

-   2
-   3
-   4

Alert notifications are sent by using DingTalk and emails. |

## SlsParameters syntax

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

## SlsParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Project|String|No|Yes|The name of the project in Log Service.|None|
|LogStore|String|No|Yes|The name of the Logstore in Log Service.|None|
|Region|String|No|Yes|The region where Log Service is deployed.|None|
|Id|String|No|Yes|The ID of the resource for which to add or modify the targets based on the event-triggered alert rule.|None|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

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

`YAML` format

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


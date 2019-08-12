# ALIYUN::ApiGateway::App {#concept_61468_zh .concept}

ALIYUN::ApiGateway::App can be used to create apps. An app is your identification to call a third-party API. If you want to call a third-party API, you must create an app.

## Syntax {#section_h1c_pzz_lfb .section}

```language-json
{
    "Type" : "ALIYUN::ApiGateway::App",
    "Properties" : {
         "Description" : String,
         "AppName" : String
    }
}

```

## Properties { .section}

|Name|Type|Required|Update allowed|Description|
|AppName|string|Yes|Yes|The app name which must be unique. It must contain 4 to 15 characters, including Chinese characters, English letters, numbers, and underscores \(\_\), and must begin with a Chinese character or an English letter|
|Description|string|No|Yes|App description，up to 180 characters|

## Response value { .section}

**Fn::GetAtt**

-   AppKey: the Key of the app.
-   AppSecret: the Secret of the app.
-   AppId: the app ID.

## Example { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "APP": {
      "Type": "ALIYUN::ApiGateway::App",
      "Properties": {
        "AppName": "my_test_app",
        "Description": "demo"
      }
    }
  }
}

```


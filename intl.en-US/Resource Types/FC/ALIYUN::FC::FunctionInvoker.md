# ALIYUN::FC::FunctionInvoker {#concept_186391 .concept}

ALIYUN::FC::FunctionInvoker is used to invoke a function.

## Syntax {#section_kob_3dx_ii2 .section}

``` {#codeblock_2bj_tl3_ejs .language-json}
{
  "Type": "ALIYUN::FC::FunctionInvoker",
  "Properties": {
    "Qualifier": String,
    "ServiceName": String,
    "ExecuteVersion": Integer,
    "Async": Boolean,
    "Event": String,
    "FunctionName": String
  }
}
```

## Properties {#section_hzr_gxr_88m .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ServiceName|String|Yes|Yes|The name of the service to which the function belongs.|The name must be 1 to 128 characters in length.|
|FunctionName|String|Yes|Yes|The name of the function.|None|
|Async|Boolean|No|Yes|Specifies whether to enable asynchronous function invocation. Default value: False.|None|
|Event|String|No|Yes|The event processed by the function. The parameter value is passed into the function as a UTF-8 encoded string. If the value is a binary string, encode it in Base64 before it is passed in.|None|
|Qualifier|String|No|Yes|The version of the service, which can be the version ID or alias name.|None|
|ExecuteVersion|Integer|No|Yes| The version of the identifier for the function to be invoked. If you set this parameter when creating the resource, the function is invoked. Otherwise, the function is not invoked.

 If the parameter value changes and the new value is valid when you update the resource, the function is invoked. Otherwise, the function is not invoked.

 |None|

## Response parameters {#section_118_83r_kqk .section}

**Fn::GetAtt**

ResultType: the type of the function invocation result. Valid values:

-   NoResult: No result is returned when the Async parameter is set to true.
-   Success: The execution succeeds when the Async parameter is set to false.
-   Failure: The execution fails when the Async parameter is set to false.

Result: the function invocation result, which depends on the ResultType parameter value. Valid values:

-   NoResult: null.
-   Success: the result returned by the invoked function. Users can interpret this response based on their function implementation. The returned result must be a UTF-8 encoded string. Otherwise, the function execution fails. If the result is a binary string, encode it in Base64 before it is returned.
-   Failure: the error message.

## Examples {#section_d5t_sdt_xy2 .section}

``` {#codeblock_0sg_90w_b31 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "FunctionInvoker": {
      "Type": "ALIYUN::FC::FunctionInvoker",
      "Properties": {
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "ExecuteVersion": {
          "Ref": "ExecuteVersion"
        },
        "Async": {
          "Ref": "Async"
        },
        "Event": {
          "Ref": "Event"
        },
        "Qualifier": {
          "Ref": "Qualifier"
        }
      }
    }
  },
  "Parameters": {
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
    },
    "ServiceName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Service name",
      "MaxLength": 128
    },
    "ExecuteVersion": {
      "Type": "Number",
      "Description": "If the property is not specified for creation and update, the function will not be invoked. The change of the property leads to the invocation of the function."
    },
    "Async": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Invocation type, Sync or Async. Defaults to Sync.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Event": {
      "Type": "String",
      "Description": "Event, binary type. This value is passed to function without any transformation. It\u2019s function\u2019s responsibility to interpret the value.\nUse Fn::Base64Decode to pass value if needed."
    },
    "Qualifier": {
      "Type": "String",
      "Description": "service version, which can be versionId or aliasName"
    }
  },
  "Outputs": {
    "ResultType": {
      "Description": "Result type:\nNoResult: Async invocation has no result.\nSuccess: Sync invocation succeeds.\nFailure: Sync invocation fails.",
      "Value": {
        "Fn::GetAtt": [
          "FunctionInvoker",
          "ResultType"
        ]
      }
    },
    "Result": {
      "Description": "Depends on result type:\nNoResult: Async invocation has no result.\nSuccess: The response of the function execution. It\u2019s in binary format. Users can interpret the data according to their function implementation.\nFailure: Error Message.",
      "Value": {
        "Fn::GetAtt": [
          "FunctionInvoker",
          "Result"
        ]
      }
    }
  }
}
```


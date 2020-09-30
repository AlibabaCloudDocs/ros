# ALIYUN::FC::FunctionInvoker

ALIYUN::FC::FunctionInvoker is used to invoke a function.

## Syntax

```
{
  "Type": "ALIYUN::FC::FunctionInvoker",
  "Properties": {
    "Qualifier": String,
    "ServiceName": String,
    "ExecuteVersion": Integer,
    "Async": Boolean,
    "Event": String,
    "FunctionName": String,
    "CheckError": Boolean,
    "ServiceRegionId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServiceName|String|Yes|Yes|The name of the service.|The name must be 1 to 128 characters in length.|
|FunctionName|String|Yes|Yes|The name of the function.|None|
|Async|Boolean|No|Yes|Specifies whether to enable asynchronous function invocation.|Default value: false. Valid values:-   true
-   false |
|Event|String|No|Yes|The event that is processed by the function.|The parameter value is passed into the function as a UTF-8 encoded string. If the value is a binary string, encode it in Base64 before it is passed in.|
|Qualifier|String|No|Yes|The version of the service.|Valid values: -   versionId
-   aliasName |
|ExecuteVersion|Integer|No|Yes|The version of the identifier for the function to be invoked. If you specify this parameter when you create the resource, the function is invoked. Otherwise, the function is not invoked.

If the parameter value changes and the new value is valid when you update the resource, the function is invoked. Otherwise, the function is not invoked.

|None|
|CheckError|Boolean|No|No|Specifies whether to check the results of the invocation.|Default value: false. Valid values: -   true

**Note:** If this parameter is set to true and the invocation fails, the resource fails to be created.

-   false |
|ServiceRegionId|String|No|No|The region ID of the function service.|None|

## Response parameters

Fn::GetAtt

-   ResultType:
    -   If Async is set to true and ResultType is set to NoResult, no result is returned.
    -   If Async is set to false and ResultType is set to Success, the invocation is successful.
    -   If Async is set to false and ResultType is set to Failure, the invocation fails.
-   Result:
    -   If ResultType is set to NoResult, the value of Result is null.
    -   If ResultType is set to Success, the value of Result is the function invocation result. Users can interpret this response based on their function implementation. The returned result must be a UTF-8 encoded string. Otherwise, the function invocation fails. If the result is a binary string, encode it in Base64 before it is returned.
    -   If ResultType is set to Failure, an error message is returned for Result.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
    },
    "ExecuteVersion": {
      "Type": "Number",
      "Description": "If the property is not specified for creation and update, the function will not be invoked. The change of the property leads to the invoke of the function."
    },
    "ServiceRegionId": {
      "Type": "String",
      "Description": "Which region service belongs to."
    },
    "ServiceName": {
      "Type": "String",
      "Description": "Service name",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Async": {
      "Type": "Boolean",
      "Description": "Invocation type, Sync or Async. Defaults to Sync.",
      "AllowedValues": [
        true,
        false
      ],
      "Default": false
    },
    "Event": {
      "Type": "String",
      "Description": "This value is passed to function as utf-8 encoded string.It’s function’s responsibility to interpret the value.\nIf the value needs to be binary, encode it via base64 before passing to this property."
    },
    "Qualifier": {
      "Type": "String",
      "Description": "service version, can be versionId or aliasName"
    },
    "CheckError": {
      "Type": "Boolean",
      "Description": "Whether check error for function invocation result.\nIf set true and function invocation result has error, the resource creation will be regard as failed.\nDefault is false",
      "AllowedValues": [
        true,
        false
      ]
    }
  },
  "Resources": {
    "FunctionInvoker": {
      "Type": "ALIYUN::FC::FunctionInvoker",
      "Properties": {
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "ExecuteVersion": {
          "Ref": "ExecuteVersion"
        },
        "ServiceRegionId": {
          "Ref": "ServiceRegionId"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Async": {
          "Ref": "Async"
        },
        "Event": {
          "Ref": "Event"
        },
        "Qualifier": {
          "Ref": "Qualifier"
        },
        "CheckError": {
          "Ref": "CheckError"
        }
      }
    }
  },
  "Outputs": {
    "ResultType": {
      "Description": "Result type:\nNoResult: Async invoke has no result.\nSuccess: Sync invoke succeeds.\nFailure: Sync invoke fails.",
      "Value": {
        "Fn::GetAtt": [
          "FunctionInvoker",
          "ResultType"
        ]
      }
    },
    "Result": {
      "Description": "Depends on result type:\nNoResult: Async invoke has no result.\nSuccess: The response of the function. The response should be utf-8 encoded string, otherwise ROS will report an error. If the response is binary, encode it via base64 before it is returned.\nFailure: Error Message.",
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  FunctionName:
    Type: String
    Description: Function name
  ExecuteVersion:
    Type: Number
    Description: >-
      If the property is not specified for creation and update, the function
      will not be invoked. The change of the property leads to the invoke of the
      function.
  ServiceRegionId:
    Type: String
    Description: Which region service belongs to.
  ServiceName:
    Type: String
    Description: Service name
    MinLength: 1
    MaxLength: 128
  Async:
    Type: Boolean
    Description: 'Invocation type, Sync or Async. Defaults to Sync.'
    AllowedValues:
      - true
      - false
    Default: false
  Event:
    Type: String
    Description: >-
      This value is passed to function as utf-8 encoded string.It’s function’s
      responsibility to interpret the value.

      If the value needs to be binary, encode it via base64 before passing to
      this property.
  Qualifier:
    Type: String
    Description: 'service version, can be versionId or aliasName'
  CheckError:
    Type: Boolean
    Description: >-
      Whether check error for function invocation result.

      If set true and function invocation result has error, the resource
      creation will be regard as failed.

      Default is false
    AllowedValues:
      - true
      - false
Resources:
  FunctionInvoker:
    Type: 'ALIYUN::FC::FunctionInvoker'
    Properties:
      FunctionName:
        Ref: FunctionName
      ExecuteVersion:
        Ref: ExecuteVersion
      ServiceRegionId:
        Ref: ServiceRegionId
      ServiceName:
        Ref: ServiceName
      Async:
        Ref: Async
      Event:
        Ref: Event
      Qualifier:
        Ref: Qualifier
      CheckError:
        Ref: CheckError
Outputs:
  ResultType:
    Description: |-
      Result type:
      NoResult: Async invoke has no result.
      Success: Sync invoke succeeds.
      Failure: Sync invoke fails.
    Value:
      'Fn::GetAtt':
        - FunctionInvoker
        - ResultType
  Result:
    Description: >-
      Depends on result type:

      NoResult: Async invoke has no result.

      Success: The response of the function. The response should be utf-8
      encoded string, otherwise ROS will report an error. If the response is
      binary, encode it via base64 before it is returned.

      Failure: Error Message.
    Value:
      'Fn::GetAtt':
        - FunctionInvoker
        - Result
```


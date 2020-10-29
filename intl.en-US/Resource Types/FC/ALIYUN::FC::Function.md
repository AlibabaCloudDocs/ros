# ALIYUN::FC::Function

ALIYUN::FC::Function is used to create a function. A function is an object that the system uses for scheduling and execution. Functions must be associated with services. All functions of a service share the same properties as the service, such as service authorizations and logging configurations.

## Syntax

```
{
  "Type": "ALIYUN::FC::Function",
  "Properties": {
    "Code": Map,
    "FunctionName": String,
    "ServiceName": String,
    "MemorySize": Integer,
    "InstanceConcurrency": Integer,
    "EnvironmentVariables": Map,
    "Initializer": String,
    "Handler": String,
    "Timeout": Integer,
    "InitializationTimeout": Integer,
    "CustomContainerConfig": Map,
    "AsyncConfiguration": Map,
    "CAPort": Integer,
    "Runtime": String,
    "Description": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Initializer|String|No|Yes|The entry point for Function Compute to initialize the created function.|The format is determined by the programming language.|
|InitializationTimeout|Integer|No|Yes|The timeout period for Function Compute to initialize the function.|Valid values: 1 to 300.Unit: seconds.

Default value: 3.

If the function is not initialized within the specified period, Function Compute terminates the initialization.|
|Code|Map|No|Yes|The code that contains the function invocation. The code must be packaged into a ZIP file.|For more information, see [Code properties](#section_ojd_4je_97q).|
|Description|String|No|Yes|The description of the function.|None|
|ServiceName|String|Yes|No|The name of the service.|The name must be 1 to 128 characters in length.|
|MemorySize|Integer|No|Yes|The memory size of the function.|Valid values: 128 to 3072. The value must be a multiple of 64.Unit: MB. |
|InstanceConcurrency|Integer|No|Yes|The maximum number of requests that can be concurrently processed by a single instance.|Valid values: 1 to 100.**Note:** Python functions do not support this parameter. |
|EnvironmentVariables|Map|No|Yes|The environment variables for the function.|None|
|Handler|String|Yes|Yes|The entry point for Function Compute to invoke the function.|For example, if you set Handler to index.handler when you create a Python function, Function Compute loads the handler function defined in the index.py file. The format is determined by the programming language.|
|Timeout|Integer|No|Yes|The timeout period for Function Compute to invoke the function.|Valid values: 1 to 600.Default value: 3.

Unit: seconds.

If the function is not invoked within the specified period, Function Compute terminates the invocation. |
|Runtime|String|Yes|Yes|The runtime environment of the function.|Valid values: nodejs6, nodejs8, nodejs10, nodejs12, python2.7, python3, java8, custom, and custom-container.|
|FunctionName|String|Yes|No|The name of the function.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or underscore \(\_\).|
|CustomContainerConfig|Map|No|Yes|The configurations of the runtime environment when Runtime is set to custom-container. If you specify this parameter, you can use a custom container image to invoke functions.|For more information, see [CustomContainerConfig properties](#section_w57_3u4_khz).|
|CAPort|Integer|No|Yes|The port on which the HTTP server is listening.|Default value: 9000.**Note:** This parameter takes effect only when the Runtime parameter is set to custom or custom-container. |
|AsyncConfiguration|Map|No|Yes|The asynchronous invocation configurations.|For more information, see [AsyncConfiguration properties](#section_8lq_7us_2xe).|

## Code syntax

```
"Code": {
  "OssBucketName": String,
  "OssObjectName": String,
  "ZipFile": String,
  "SourceCode": String
}
```

## Code properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OssBucketName|String|No|Yes|The name of the bucket where the function code ZIP file is stored.|None|
|OssObjectName|String|No|Yes|The name of the object where the function code ZIP file is stored.|None|
|ZipFile|String|No|Yes|The Base64-encoded ZIP file to be uploaded in the request body.|None|
|SourceCode|String|No|Yes|The source code of the function. Node.js, PHP, and Python code is supported.|The code can be up to 4,096 characters in length. ROS writes the value of this parameter into a UTF-8 encoded file that is named index. When the ZipFile, SourceCode, and OssBucketName \(or OssObjectName\) parameters are all specified, the three parameters are in descending order of priority.|

## CustomContainerConfig syntax

```
"CustomContainerConfig": {
  "Command": String,
  "Args": String,
  "Image": String
}
```

## CustomContainerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Command|String|No|Yes|The URL of the container image.|Example: `registry-vpc.cn-hangzhou.aliyuncs.com/fc-demo/helloworld:v1beta1`.|
|Args|String|No|Yes|The startup arguments of the container.|Example: `["-arg1", "value1"]`.|
|Image|String|Yes|Yes|The commands run by the container.|Example: `["/code/myserver"]`.|

## AsyncConfiguration syntax

```
"AsyncConfiguration": {
  "Destination": Map
  "MaxAsyncRetryAttempts": Integer,
  "MaxAsyncEventAgeInSeconds": Integer
}
```

## AsyncConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Destination|Map|No|No|The destination of the asynchronous invocation.|For more information, see [Destination property](#section_hbk_zbm_yp1).|
|MaxAsyncRetryAttempts|Integer|No|Yes|The maximum number of retries for the asynchronous invocation.|None|
|MaxAsyncEventAgeInSeconds|Integer|No|Yes|The maximum lifetime of messages.|None|

## Destination syntax

```
"Destination": {
  "OnSuccess": String,
  "OnFailure": String
}
```

## Destination property

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OnSuccess|String|No|Yes|Specifies the destination that Function Compute calls when the function is invoked.|None|
|OnFailure|String|No|Yes|Specifies the destination that Function Compute calls when invocation of the function fails due to a system error or an error of the function.|None|

## Response parameters

Fn::GetAtt

-   FunctionId: the unique ID generated by the system for each function.
-   ServiceName: the name of the service to which the function belongs.
-   ARN: the Alibaba Cloud Resource Name \(ARN\) of the function.
-   FunctionName: the name of the function.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "MemorySize": {
      "Type": "Number",
      "Description": "The amount of memory that is used to invoke the function. Unit: MB. Function Compute uses this value to allocate CPU resources proportionally. Defaults to 128 MB. It can be multiple of 64 MB and between 128 MB and 3072 MB.",
      "MinValue": 128,
      "MaxValue": 3072,
      "Default": 128
    },
    "Description": {
      "Type": "String",
      "Description": "Function description"
    },
    "Timeout": {
      "Type": "Number",
      "Description": "The maximum time duration a function can run, in seconds. After which Function Compute terminates the execution. Defaults to 3 seconds, and can be between 1 to 600 seconds.",
      "MinValue": 1,
      "MaxValue": 600,
      "Default": 3
    },
    "Handler": {
      "Type": "String",
      "Description": "The function execution entry point."
    },
    "CustomContainerConfig": {
      "Type": "Json",
      "Description": "Custom container runtime related configuration. After configuration, the function can be replaced with a custom container to execute the function"
    },
    "Code": {
      "Type": "Json",
      "Description": "The code that contains the function implementation."
    },
    "AsyncConfiguration": {
      "Type": "Json",
      "Description": "Configuration of asynchronous function calls"
    },
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
    },
    "CAPort": {
      "Type": "Number",
      "Description": "Custom runtime and custom container runtime dedicated fields, which represent the port that the started custom http server listens to. The default value is 9000",
      "Default": 9000
    },
    "Runtime": {
      "Type": "String",
      "Description": "The function runtime environment. Supporting nodejs6, nodejs8, nodejs10, nodejs12, python2.7, python3, java8, custom, custom-container and so on"
    },
    "EnvironmentVariables": {
      "Type": "Json",
      "Description": "The environment variable set for the function, you can get the value of the environment variable in the function."
    },
    "ServiceName": {
      "Type": "String",
      "Description": "Service name",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Initializer": {
      "Type": "String",
      "Description": "the entry point of the initializer"
    },
    "InitializationTimeout": {
      "Type": "Number",
      "Description": "the max execution time of the initializer, in second"
    },
    "InstanceConcurrency": {
      "Type": "Number",
      "Description": "Function instance concurrency. Value can be between 1 to 100.",
      "MinValue": 1,
      "MaxValue": 100
    }
  },
  "Resources": {
    "Function": {
      "Type": "ALIYUN::FC::Function",
      "Properties": {
        "MemorySize": {
          "Ref": "MemorySize"
        },
        "Description": {
          "Ref": "Description"
        },
        "Timeout": {
          "Ref": "Timeout"
        },
        "Handler": {
          "Ref": "Handler"
        },
        "CustomContainerConfig": {
          "Ref": "CustomContainerConfig"
        },
        "Code": {
          "Ref": "Code"
        },
        "AsyncConfiguration": {
          "Ref": "AsyncConfiguration"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "CAPort": {
          "Ref": "CAPort"
        },
        "Runtime": {
          "Ref": "Runtime"
        },
        "EnvironmentVariables": {
          "Ref": "EnvironmentVariables"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Initializer": {
          "Ref": "Initializer"
        },
        "InitializationTimeout": {
          "Ref": "InitializationTimeout"
        },
        "InstanceConcurrency": {
          "Ref": "InstanceConcurrency"
        }
      }
    }
  },
  "Outputs": {
    "FunctionId": {
      "Description": "The function ID",
      "Value": {
        "Fn::GetAtt": [
          "Function",
          "FunctionId"
        ]
      }
    },
    "FunctionName": {
      "Description": "The function name",
      "Value": {
        "Fn::GetAtt": [
          "Function",
          "FunctionName"
        ]
      }
    },
    "ServiceName": {
      "Description": "The service name",
      "Value": {
        "Fn::GetAtt": [
          "Function",
          "ServiceName"
        ]
      }
    },
    "ARN": {
      "Description": "The ARN for ALIYUN::ROS::CustomResource",
      "Value": {
        "Fn::GetAtt": [
          "Function",
          "ARN"
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
  MemorySize:
    Type: Number
    Description: >-
      The amount of memory that is used to invoke the function. Unit: MB. Function Compute
      uses this value to allocate CPU resources proportionally. Defaults to 128
      MB. It can be multiple of 64 MB and between 128 MB and 3072 MB.
    MinValue: 128
    MaxValue: 3072
    Default: 128
  Description:
    Type: String
    Description: Function description
  Timeout:
    Type: Number
    Description: >-
      The maximum time duration a function can run, in seconds. After which
      Function Compute terminates the execution. Defaults to 3 seconds, and can
      be between 1 to 600 seconds.
    MinValue: 1
    MaxValue: 600
    Default: 3
  Handler:
    Type: String
    Description: The function execution entry point.
  CustomContainerConfig:
    Type: Json
    Description: >-
      Custom container runtime related configuration. After configuration, the
      function can be replaced with a custom container to execute the function
  Code:
    Type: Json
    Description: The code that contains the function implementation.
  AsyncConfiguration:
    Type: Json
    Description: Configuration of asynchronous function calls
  FunctionName:
    Type: String
    Description: Function name
  CAPort:
    Type: Number
    Description: >-
      Custom runtime and custom container runtime dedicated fields, which
      represent the port that the started custom http server listens to. The
      default value is 9000
    Default: 9000
  Runtime:
    Type: String
    Description: >-
      The function runtime environment. Supporting nodejs6, nodejs8, nodejs10,
      nodejs12, python2.7, python3, java8, custom, custom-container and so on
  EnvironmentVariables:
    Type: Json
    Description: >-
      The environment variable set for the function, you can get the value of
      the environment variable in the function.
  ServiceName:
    Type: String
    Description: Service name
    MinLength: 1
    MaxLength: 128
  Initializer:
    Type: String
    Description: the entry point of the initializer
  InitializationTimeout:
    Type: Number
    Description: 'the max execution time of the initializer, in second'
  InstanceConcurrency:
    Type: Number
    Description: Function instance concurrency. Value can be between 1 to 100.
    MinValue: 1
    MaxValue: 100
Resources:
  Function:
    Type: 'ALIYUN::FC::Function'
    Properties:
      MemorySize:
        Ref: MemorySize
      Description:
        Ref: Description
      Timeout:
        Ref: Timeout
      Handler:
        Ref: Handler
      CustomContainerConfig:
        Ref: CustomContainerConfig
      Code:
        Ref: Code
      AsyncConfiguration:
        Ref: AsyncConfiguration
      FunctionName:
        Ref: FunctionName
      CAPort:
        Ref: CAPort
      Runtime:
        Ref: Runtime
      EnvironmentVariables:
        Ref: EnvironmentVariables
      ServiceName:
        Ref: ServiceName
      Initializer:
        Ref: Initializer
      InitializationTimeout:
        Ref: InitializationTimeout
      InstanceConcurrency:
        Ref: InstanceConcurrency
Outputs:
  FunctionId:
    Description: The function ID
    Value:
      'Fn::GetAtt':
        - Function
        - FunctionId
  FunctionName:
    Description: The function name
    Value:
      'Fn::GetAtt':
        - Function
        - FunctionName
  ServiceName:
    Description: The service name
    Value:
      'Fn::GetAtt':
        - Function
        - ServiceName
  ARN:
    Description: 'The ARN for ALIYUN::ROS::CustomResource'
    Value:
      'Fn::GetAtt':
        - Function
        - ARN
```


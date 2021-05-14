# ALIYUN::FC::Function

ALIYUN::FC::Function is used to create a function. Functions must be associated with services. All functions of a service share the same properties as the service, such as service authorizations and logging configurations.

## Syntax

```
{
  "Type": "ALIYUN::FC::Function",
  "Properties": {
    "Code": Map,
    "FunctionName": String,
    "ServiceName": String,
    "InstanceType": String,
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
|Initializer|String|No|Yes|The handler used by Function Compute to initialize the function.|The format is determined by the programming language.|
|InitializationTimeout|Integer|No|Yes|The timeout period for Function Compute to initialize the function.|Valid values: 1 to 300. Unit: seconds.

Default value: 3.

If the function is not initialized within the specified period, Function Compute terminates the initialization.|
|Code|Map|No|Yes|The code of the function. The code must be packaged into a ZIP file.|For more information, see the [Code properties](#section_ojd_4je_97q) section in this topic.|
|InstanceType|String|No|Yes|The type of the function instance.|Valid values:-   e1: elastic instance
-   c1: performance instance |
|Description|String|No|Yes|The description of the function.|None|
|ServiceName|String|Yes|No|The name of the service.|The name must be 1 to 128 characters in length.|
|MemorySize|Integer|No|Yes|The memory size of the function.|-   Valid values: 128 to 3072. The value must be a multiple of 64.
-   Valid values for a performance instance: 4096, 8192, 16384, and 32768.

Unit: MB. |
|InstanceConcurrency|Integer|No|Yes|The number of requests that a function can process at a time.|Valid values: 1 to 100 **Note:** Python functions do not support this parameter. |
|EnvironmentVariables|Map|No|Yes|The environment variables for the function.|None|
|Handler|String|Yes|Yes|The handler that is used by Function Compute to invoke the function.|For example, if you set Handler to index.handler when you create a Python function, Function Compute loads the handler function defined in the index.py file. The format is determined by the programming language.|
|Timeout|Integer|No|Yes|The timeout period for Function Compute to invoke the function.|Valid values: 1 to 600. Default value: 3.

Unit: seconds.

If the function is not invoked within the specified period, Function Compute terminates the invocation. |
|Runtime|String|Yes|Yes|The runtime environment of the function.|Valid values: nodejs6, nodejs8, nodejs10, nodejs12, python2.7, python3, java8, custom, and custom-container.|
|FunctionName|String|Yes|No|The name of the function.|The name must be 1 to 128 characters in length. and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or underscore \(\_\).|
|CustomContainerConfig|Map|No|Yes|The configurations of the runtime environment when Runtime is set to custom-container. If you specify this parameter, you can use a custom container image to invoke functions.|For more information, see the [CustomContainerConfig properties](#section_w57_3u4_khz) section in this topic.|
|CAPort|Integer|No|Yes|The port on which the HTTP server is listening.|Default value: 9000. **Note:** This parameter is valid only when the Runtime parameter is set to custom or custom-container. |
|AsyncConfiguration|Map|No|Yes|The asynchronous invocation configurations.|For more information, see the [AsyncConfiguration properties](#section_8lq_7us_2xe) section in this topic.|

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
  "Image": String,
  "AccelerationType": String
}
```

## CustomContainerConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Command|String|No|Yes|The command to be run to start the container.|Example: `["/code/myserver"]`.|
|Args|String|No|Yes|The startup arguments of the container.|Example: `["-arg1", "value1"]`.|
|Image|String|Yes|Yes|The URL of the container image.|Example: `registry-vpc.cn-hangzhou.aliyuncs.com/fc-demo/helloworld:v1beta1`.|
|AccelerationType|String|No|Yes|Specifies whether to enable image pull acceleration.|Default value: None. Valid values:-   Default: Image pull acceleration is enabled.
-   None: Image pull acceleration is disabled. |

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
|Destination|Map|No|No|The destination for asynchronous invocation.|For more information, see the [Destination properties](#section_hbk_zbm_yp1) section in this topic.|
|MaxAsyncRetryAttempts|Integer|No|Yes|The maximum number of retries for the asynchronous invocation.|None|
|MaxAsyncEventAgeInSeconds|Integer|No|Yes|The maximum lifetime of messages.|None|

## Destination syntax

```
"Destination": {
  "OnSuccess": String,
  "OnFailure": String
}
```

## Destination properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OnSuccess|String|No|Yes|The destination that Function Compute invokes when the function is executed.|None|
|OnFailure|String|No|Yes|The destination that Function Compute invokes when the function fails to be executed due to a system error or an error of the function.|None|

## Response parameters

Fn::GetAtt

-   FunctionId: the unique ID generated by the system for each function.
-   ServiceName: the name of the service.
-   ARN: the Alibaba Cloud Resource Name \(ARN\) of the function.
-   FunctionName: the name of the function.
-   ServiceId: the function service ID.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "MemorySize": {
      "Type": "Number",
      "Description": "The amount of memory that’s used to run function, in MB. Function Compute uses this value to allocate CPU resources proportionally. Defaults to 128 MB. It can be multiple of 64 MB and between 128 MB and 3072 MB.",
      "MinValue": 128,
      "MaxValue": 32768,
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
    "CAPort": {
      "Type": "Number",
      "Description": "Custom runtime and custom container runtime dedicated fields, which represent the port that the started custom http server listens to. The default value is 9000",
      "Default": 9000
    },
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
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
    },
    "InstanceType": {
      "Type": "String",
      "Description": "Instance type. Value:e1: flexible instance. Memory size between 128 and 3072c1: performance instance. Memory size allow values are 4096, 8192, 16384 and 32768",
      "AllowedValues": [
        "e1",
        "c1"
      ]
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
        "CAPort": {
          "Ref": "CAPort"
        },
        "FunctionName": {
          "Ref": "FunctionName"
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
        },
        "InstanceType": {
          "Ref": "InstanceType"
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
    },
    "ServiceId": {
      "Description": "The service ID",
      "Value": {
        "Fn::GetAtt": [
          "Function",
          "ServiceId"
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
  AsyncConfiguration:
    Description: Configuration of asynchronous function calls
    Type: Json
  CAPort:
    Default: 9000
    Description: Custom runtime and custom container runtime dedicated fields, which
      represent the port that the started custom http server listens to. The default
      value is 9000
    Type: Number
  Code:
    Description: The code that contains the function implementation.
    Type: Json
  CustomContainerConfig:
    Description: Custom container runtime related configuration. After configuration,
      the function can be replaced with a custom container to execute the function
    Type: Json
  Description:
    Description: Function description
    Type: String
  EnvironmentVariables:
    Description: The environment variable set for the function, you can get the value
      of the environment variable in the function.
    Type: Json
  FunctionName:
    Description: Function name
    Type: String
  Handler:
    Description: The function execution entry point.
    Type: String
  InitializationTimeout:
    Description: the max execution time of the initializer, in second
    Type: Number
  Initializer:
    Description: the entry point of the initializer
    Type: String
  InstanceConcurrency:
    Description: Function instance concurrency. Value can be between 1 to 100.
    MaxValue: 100
    MinValue: 1
    Type: Number
  InstanceType:
    AllowedValues:
    - e1
    - c1
    Description: 'Instance type. Value:e1: flexible instance. Memory size between
      128 and 3072c1: performance instance. Memory size allow values are 4096, 8192,
      16384 and 32768'
    Type: String
  MemorySize:
    Default: 128
    Description: "The amount of memory that\u2019s used to run function, in MB. Function\
      \ Compute uses this value to allocate CPU resources proportionally. Defaults\
      \ to 128 MB. It can be multiple of 64 MB and between 128 MB and 3072 MB."
    MaxValue: 32768
    MinValue: 128
    Type: Number
  Runtime:
    Description: The function runtime environment. Supporting nodejs6, nodejs8, nodejs10,
      nodejs12, python2.7, python3, java8, custom, custom-container and so on
    Type: String
  ServiceName:
    Description: Service name
    MaxLength: 128
    MinLength: 1
    Type: String
  Timeout:
    Default: 3
    Description: The maximum time duration a function can run, in seconds. After which
      Function Compute terminates the execution. Defaults to 3 seconds, and can be
      between 1 to 600 seconds.
    MaxValue: 600
    MinValue: 1
    Type: Number
Resources:
  Function:
    Properties:
      AsyncConfiguration:
        Ref: AsyncConfiguration
      CAPort:
        Ref: CAPort
      Code:
        Ref: Code
      CustomContainerConfig:
        Ref: CustomContainerConfig
      Description:
        Ref: Description
      EnvironmentVariables:
        Ref: EnvironmentVariables
      FunctionName:
        Ref: FunctionName
      Handler:
        Ref: Handler
      InitializationTimeout:
        Ref: InitializationTimeout
      Initializer:
        Ref: Initializer
      InstanceConcurrency:
        Ref: InstanceConcurrency
      InstanceType:
        Ref: InstanceType
      MemorySize:
        Ref: MemorySize
      Runtime:
        Ref: Runtime
      ServiceName:
        Ref: ServiceName
      Timeout:
        Ref: Timeout
    Type: ALIYUN::FC::Function
Outputs:
  ARN:
    Description: The ARN for ALIYUN::ROS::CustomResource
    Value:
      Fn::GetAtt:
      - Function
      - ARN
  FunctionId:
    Description: The function ID
    Value:
      Fn::GetAtt:
      - Function
      - FunctionId
  FunctionName:
    Description: The function name
    Value:
      Fn::GetAtt:
      - Function
      - FunctionName
  ServiceId:
    Description: The service ID
    Value:
      Fn::GetAtt:
      - Function
      - ServiceId
  ServiceName:
    Description: The service name
    Value:
      Fn::GetAtt:
      - Function
      - ServiceName
```

For more examples, visit [FunctionInvoker.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/JSON/FunctionInvoker.json) and [FunctionInvoker.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/YAML/FunctionInvoker.yml). In the examples, the ALIYUN::FC::Service, ALIYUN::FC::Function, ALIYUN::FC::FunctionInvoker, ALIYUN::FC::Trigger, ALIYUN::FC::Version, ALIYUN::FC::Alias, and ALIYUN::FC::ProvisionConfig resource types are involved.


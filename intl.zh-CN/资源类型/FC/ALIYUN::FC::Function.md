# ALIYUN::FC::Function

ALIYUN::FC::Function类型用于创建函数。函数必须从属于服务，一个服务下的所有函数都共享该服务的属性，例如：授权、日志设置等。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Initializer|String|否|是|初始化函数执行的入口。|具体格式和语言相关。|
|InitializationTimeout|Integer|否|是|初始化函数运行的超时时间。|取值范围：1~300。单位：秒。

默认值：3。

初始化函数时，如果超该时间，则终止执行。|
|Code|Map|否|是|指定Code ZIP包。|更多信息，请参见[Code属性](#section_ojd_4je_97q)。|
|InstanceType|String|否|是|函数实例类型。|取值：-   e1：弹性实例。
-   c1：性能实例。 |
|Description|String|否|是|函数的描述。|无|
|ServiceName|String|是|否|服务名称。|长度为1~128个字符。|
|MemorySize|Integer|否|是|函数的内存规格。|取值：-   弹性实例：128~3072，必须是64的倍数。
-   性能实例：4096、8192、16384、32768。

单位：MB。 |
|InstanceConcurrency|Integer|否|是|实例并发度。|取值范围：1~100。**说明：** Python函数实例不支持该参数。 |
|EnvironmentVariables|Map|否|是|函数设置的环境变量。|无|
|Handler|String|是|是|函数执行的入口。|以Python为例，创建函数时指定的Handler为index.handler，文件名为index.py，入口函数为handler。具体格式和语言相关。|
|Timeout|Integer|否|是|函数运行的超时时间。|取值范围：1~600。默认值：3。

单位：秒。

运行函数时，如果超出该时间，则终止执行。 |
|Runtime|String|是|是|函数的运行环境。|目前支持nodejs6、nodejs8、nodejs10、nodejs12、python2.7、python3、java8、custom、custom-container。|
|FunctionName|String|是|否|函数名称。|长度为1~128个字符。以英文字母或下划线（\_）开头，可以包含英文字母、下划线（\_）、数字和短划线（-）。|
|CustomContainerConfig|Map|否|是|Runtime取值为custom-container时的配置，配置后可以使用自定义容器镜像执行函数。|更多信息，请参见[CustomContainerConfig属性](#section_w57_3u4_khz)。|
|CAPort|Integer|否|是|自定义HTTP Server监听的端口。|默认为9000。**说明：** Runtime取值为custom或custom-container时该参数生效。 |
|AsyncConfiguration|Map|否|是|异步调用配置。|更多信息，请参见[AsyncConfiguration属性](#section_8lq_7us_2xe)。|

## Code语法

```
"Code": {
  "OssBucketName": String,
  "OssObjectName": String,
  "ZipFile": String,
  "SourceCode": String
}
```

## Code属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OssBucketName|String|否|是|函数Code ZIP包的存储空间名称。|无|
|OssObjectName|String|否|是|Code ZIP包的对象名。|无|
|ZipFile|String|否|是|在请求体中上传的Code ZIP包的Base64编码。|无|
|SourceCode|String|否|是|函数源码（目前支持Node.js、PHP、Python）。|最长为4096个字符。ROS会将参数值写入一个UTF-8编码的名为index的文件。当同时传入ZipFile、SourceCode和OssBucketName&OssObjectName时，优先级依次为：ZipFile\>SourceCode\>OssBucketName&OssObjectName。|

## CustomContainerConfig语法

```
"CustomContainerConfig": {
  "Command": String,
  "Args": String,
  "Image": String,
  "AccelerationType": String
}
```

## CustomContainerConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Command|String|否|是|容器启动命令。|示例值：`["/code/myserver"]`。|
|Args|String|否|是|容器启动参数。|示例值：`["-arg1", "value1"]`。|
|Image|String|是|是|容器镜像地址。|示例值：`registry-vpc.cn-hangzhou.aliyuncs.com/fc-demo/helloworld:v1beta1`。|
|AccelerationType|String|否|是|是否开启镜像加速。|取值：-   Default：开启镜像加速。
-   None（默认值）：关闭镜像加速。 |

## AsyncConfiguration语法

```
"AsyncConfiguration": {
  "Destination": Map
  "MaxAsyncRetryAttempts": Integer,
  "MaxAsyncEventAgeInSeconds": Integer
}
```

## AsyncConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Destination|Map|否|否|异步调用目标。|更多信息，请参见[Destination属性](#section_hbk_zbm_yp1)。|
|MaxAsyncRetryAttempts|Integer|否|是|重试次数。|无|
|MaxAsyncEventAgeInSeconds|Integer|否|是|消息最大存活时长。|无|

## Destination语法

```
"Destination": {
  "OnSuccess": String,
  "OnFailure": String
}
```

## Destination属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OnSuccess|String|否|是|当函数执行成功时，函数计算将调用该配置对应的目标。|无|
|OnFailure|String|否|是|当函数执行失败（系统错误或函数内部错误）时，函数计算将调用该配置对应的目标。|无|

## 返回值

Fn::GetAtt

-   FunctionId：系统为每个函数生成的唯一ID。
-   ServiceName：服务名称。
-   ARN：函数的ARN。
-   FunctionName：函数名。
-   ServiceId：函数服务ID。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建函数服务、创建函数、执行函数、触发函数执行、发布版本、创建别名和创建预留实例的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/JSON/FunctionInvoker.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/FC/YAML/FunctionInvoker.yml)。


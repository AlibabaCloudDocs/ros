# ALIYUN::FC::Function

ALIYUN::FC::Function类型是用于系统调度和运行的单位。函数必须从属于服务，一个服务下的所有函数都共享该服务的属性，例如授权、日志设置。

## 语法

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
    "Runtime": String,
    "Description": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Initializer|String|否|是|初始化函数执行的入口。|具体格式和语言相关。|
|InitializationTimeout|Integer|否|是|初始化函数运行的超时时间。|单位：秒。取值：1~300。默认值：3。初始化函数时，如果超出这个时间，则终止执行。|
|Code|Map|是|是|指定code zip包。|无。|
|Description|String|否|是|函数的简短描述。|无。|
|ServiceName|String|是|否|服务名称。|长度为1~128个字符。|
|MemorySize|Integer|否|是|函数的内存规格。|取值范围：128~1536，必须是64的倍数。 单位：MB。 |
|InstanceConcurrency|Integer|否|是|实例并发度。python函数实例不支持该参数。|取值范围：1~100。|
|EnvironmentVariables|Map|否|是|函数设置的环境变量。|无。|
|Handler|String|是|是|函数执行的入口。|以python为例，创建函数时指定的Handler为index.handler， 文件名为index.py，入口函数为handler。具体格式和语言相关。|
|Timeout|Integer|否|是|函数运行的超时时间。|取值范围：1~300。 默认值：3。

 单位：秒。

 运行函数时，如果超出这个时间，则终止执行。 |
|Runtime|String|是|是|函数的运行环境。|目前支持nodejs6、nodejs8、python2.7、python3、java8。|
|FunctionName|String|是|否|函数名称。|以英文字母或下划线开头，可以包含数字和中划线，长度限制为1~128个字符。|

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
|OssBucketName|String|否|是|函数code zip包的存储空间名称。|无。|
|OssObjectName|String|否|是|code zip包的对象名。|无。|
|ZipFile|String|否|是|在请求体中上传的code zip包的Base64编码。|无。|
|SourceCode|String|否|是|函数源码（目前支持Node.js、PHP、Python）。|最大长度为4096个字符。ROS会将参数值写入一个UTF-8编码的名为index的文件。当同时传入ZipFile、SourceCode和OssBucketName&OssObjectName时，优先级依次为：ZipFile\>SourceCode\>OssBucketName&OssObjectName。|

## 返回值

Fn::GetAtt

-   FunctionId：系统为每个函数生成的唯一ID。
-   ServiceName：服务名。
-   ARN：函数的ARN。
-   FunctionName：函数名。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ServiceName": {
      "Type": "String",
      "Description": "FC ServiceName",
      "Default": "fvt-ros-test"
    },
    "SourceCode": {
      "Type": "String",
      "Description": "Function SourceCode",
      "Default": "def handler(event, context):\n\treturn 'Hello World!'"
    },
    "Handler": {
      "Type": "String",
      "Description": "Handler",
      "Default": "index.handler"
    },
    "Runtime": {
      "Type": "String",
      "Description": "Runtime",
      "Default": "python3"
    },
    "FunctionName": {
      "Type": "String",
      "Description": "Function Name",
      "Default": "PythonFunc"
    }
  },
  "Resources": {
    "Service": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        }
      }
    },
    "Function": {
      "DependsOn": "Service",
      "Type": "ALIYUN::FC::Function",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Code": {
          "SourceCode": {
            "Ref": "SourceCode"
          }
        },
        "Handler": {
          "Ref": "Handler"
        },
        "Runtime": {
          "Ref": "Runtime"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        }
      }
    }
  },
  "Outputs": {
    "FunctionId": {
      "Value": {
        "Fn::GetAtt": [
          "Function", "FunctionId"
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
  ServiceName:
    Type: String
    Description: FC ServiceName
    Default: fvt-ros-test
  SourceCode:
    Type: String
    Description: Function SourceCode
    Default: "def handler(event, context):\n\treturn 'Hello World!'"
  Handler:
    Type: String
    Description: Handler
    Default: index.handler
  Runtime:
    Type: String
    Description: Runtime
    Default: python3
  FunctionName:
    Type: String
    Description: Function Name
    Default: PythonFunc
Resources:
  Service:
    Type: ALIYUN::FC::Service
    Properties:
      ServiceName:
        Ref: ServiceName
  Function:
    DependsOn: Service
    Type: ALIYUN::FC::Function
    Properties:
      ServiceName:
        Ref: ServiceName
      Code:
        SourceCode:
          Ref: SourceCode
      Handler:
        Ref: Handler
      Runtime:
        Ref: Runtime
      FunctionName:
        Ref: FunctionName
Outputs:
  FunctionId:
    Value:
      Fn::GetAtt:
      - Function
      - FunctionId
```


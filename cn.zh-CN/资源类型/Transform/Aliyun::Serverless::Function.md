# Aliyun::Serverless::Function

Aliyun::Serverless::Function类型用于创建FC函数。

## 语法

```
{
  "Type": "Aliyun::Serverless::Function",
  "Properties": {
    "Handler": String,
    "Runtime": String,
    "CodeUri": String,
    "Initializer": String,
    "Description": String,
    "MemorySize": Integer,
    "Timeout": Integer,
    "InitializationTimeout": Integer,
    "EnvironmentVariables": Map,
    "InstanceConcurrency": Integer,
    "Events": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Handler|String|是|是|函数执行的入口。|无|
|Runtime|String|是|是|函数的运行环境。|取值：-   nodejs6
-   nodejs8
-   nodejs10
-   nodejs12
-   python2.7
-   python3
-   java8
-   php7.2
-   dotnetcore2.1 |
|CodeUri|String|是|是|代码位置。|OSS地址或项目中代码路径。|
|Initializer|String|否|是|初始化函数执行的入口。|具体格式和语言相关。|
|InitializationTimeout|Integer|否|是|初始化函数运行的超时时间。|取值范围：1~300。单位：秒。

默认值：3。|
|Description|String|否|是|函数的描述。|无|
|MemorySize|Integer|否|是|每次执行函数分配的内存大小。|取值范围：128~1536。**说明：** 必须是64的倍数。

单位：MB。

默认值：128。|
|InstanceConcurrency|Integer|否|是|实例并发度。|取值范围：1~100。**说明：** python函数实例不支持该参数。 |
|EnvironmentVariables|Map|否|是|为函数设置的环境变量。|无|
|Timeout|Integer|否|是|函数运行的超时时间。|取值范围：1~300。单位：秒。

默认值：3。 |
|Events|Map|否|是|定义触发此函数的事件。|详情请参见[事件源](https://github.com/alibaba/funcraft/blob/master/docs/specs/2018-04-03-zh-cn.md#%E4%BA%8B%E4%BB%B6%E6%BA%90%E7%B1%BB%E5%9E%8B)。。|

## 返回值

Fn::GetAtt

-   FunctionId：系统为每个函数生成的唯一ID。
-   ServiceName：服务名。
-   ARN：函数的ARN。
-   FunctionName：函数名。

## 示例

`JSON`格式

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Parameters": {
    "CodeUri": {
      "Type": "String"
    }
  },
  "Resources": {
    "MyService": {
      "Type": "Aliyun::Serverless::Service",
      "Properties": {},
      "MyFunction": {
        "Type": "Aliyun::Serverless::Function",
        "Properties": {
          "Handler": "index.handler",
          "CodeUri": {
            "Ref": "CodeUri"
          },
          "Description": "Hello world with python2.7!",
          "Runtime": "python2.7",
          "Timeout": 300
        }
      }
    }
  },
  "Outputs": {
    "MyServiceId": {
      "Value": {
        "Fn::GetAtt": [
          "MyService",
          "ServiceId"
        ]
      }
    },
    "ServiceName": {
      "Value": {
        "Fn::GetAtt": [
          "MyService",
          "ServiceName"
        ]
      }
    },
    "FunctionName": {
      "Value": {
        "Fn::GetAtt": [
          "MyServiceMyFunction",
          "FunctionName"
        ]
      }
    },
    "FunctionId": {
      "Value": {
        "Fn::GetAtt": [
          "MyServiceMyFunction",
          "FunctionId"
        ]
      }
    },
    "ARN": {
      "Value": {
        "Fn::GetAtt": [
          "MyServiceMyFunction",
          "ARN"
        ]
      }
    },
    "FunctionServiceName": {
      "Value": {
        "Fn::GetAtt": [
          "MyServiceMyFunction",
          "ServiceName"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Parameters:
  CodeUri:
    Type: String
Resources:
  MyService:
    Type: 'Aliyun::Serverless::Service'
    Properties: {}
    MyFunction:
      Type: 'Aliyun::Serverless::Function'
      Properties:
        Handler: index.handler
        CodeUri:
          Ref: CodeUri
        Description: Hello world with python2.7!
        Runtime: python2.7
        Timeout: 300
Outputs:
  MyServiceId:
    Value:
      'Fn::GetAtt':
        - MyService
        - ServiceId
  ServiceName:
    Value:
      'Fn::GetAtt':
        - MyService
        - ServiceName
  FunctionName:
    Value:
      'Fn::GetAtt':
        - MyServiceMyFunction
        - FunctionName
  FunctionId:
    Value:
      'Fn::GetAtt':
        - MyServiceMyFunction
        - FunctionId
  ARN:
    Value:
      'Fn::GetAtt':
        - MyServiceMyFunction
        - ARN
  FunctionServiceName:
    Value:
      'Fn::GetAtt':
        - MyServiceMyFunction
        - ServiceName
```


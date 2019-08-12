# ALIYUN::FC::Function {#concept_186309 .concept}

ALIYUN::FC::Function类型用于系统调度和运行的单位。函数必须从属于服务，一个服务下的所有函数都共享该服务的属性，例如授权、日志设置。

## 语法 {#section_hql_byd_50u .section}

``` {#codeblock_xp3_70f_ubq .language-json}
{
  "Type": "ALIYUN::FC::Function",
  "Properties": {
    "Code": Map,
    "FunctionName": String,
    "ServiceName": String,
    "MemorySize": Integer,
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

## 属性 {#section_u0w_4t0_4q7 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Initializer|String|否|是|初始化 function 执行的入口，具体格式和语言相关。|无。|
|InitializationTimeout|Integer|否|是|初始化 function 运行的超时时间，单位为秒，最小1秒，最长5分钟，默认3秒。初始化 function 超过这个时间后会被终止执行。|无。|
|Code|Map|是|是|指定code zip包。|无。|
|Description|String|否|是|function的简短描述。|无。|
|ServiceName|String|是|否|service名称。|长度为1-128字符。|
|MemorySize|Integer|否|是|function的内存规格，单位为MB。|最小为128MB，最大1536MB，为64MB的倍数。|
|EnvironmentVariables|Map|否|是| 为函数设置的环境变量，可以在函数中获取环境变量的值。

 |无。|
|Handler|String|是|是| function执行的入口，具体格式和语言相关。

 |无。|
|Timeout|Integer|否|是| function运行的超时时间，单位为秒，默认3秒。function超过这个时间后会被终止执行。

 |最小1秒，最长5分钟。|
|Runtime|String|是|是|function的运行环境。|目前支持nodejs6, nodejs8, python2.7, python3, java8。|
|FunctionName|String|是|否|function名称。|无。|

## Code语法 {#section_9kv_jqv_s5t .section}

``` {#codeblock_vi2_eqr_9lu .language-json}
"Code": {
  "OssBucketName": String,
  "OssObjectName": String,
  "ZipFile": String
}
```

## Code属性 {#section_ojd_4je_97q .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OssBucketName|String|否|是|function code包的bucket name。|无。|
|OssObjectName|String|否|是|code zip包的object name。|无。|
|ZipFile|String|否|是|直接在request body中上传code zip包的base64编码。|无。|

## 返回值 {#section_m3p_8er_v6r .section}

**Fn::GetAtt**

FunctionId：系统为每个Function生成的唯一ID。

## 示例 {#section_3j7_mlf_htb .section}

``` {#codeblock_q0n_1l2_mpy .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Function": {
      "Type": "ALIYUN::FC::Function",
      "Properties": {
        "Code": {
          "Ref": "Code"
        },
        "Description": {
          "Ref": "Description"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "MemorySize": {
          "Ref": "MemorySize"
        },
        "EnvironmentVariables": {
          "Ref": "EnvironmentVariables"
        },
        "Handler": {
          "Ref": "Handler"
        },
        "Timeout": {
          "Ref": "Timeout"
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
  "Parameters": {
    "Code": {
      "Type": "Json",
      "Description": "The code that contains the function implementation."
    },
    "Description": {
      "Type": "String",
      "Description": "Function description"
    },
    "ServiceName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Service name",
      "MaxLength": 128
    },
    "MemorySize": {
      "Default": 128,
      "Type": "Number",
      "Description": "The amount of memory that\u2019s used to run function, in MB. Function Compute uses this value to allocate CPU resources proportionally. Defaults to 128 MB. It can be multiple of 64 MB and between 128 MB and 3072 MB.",
      "MaxValue": 1536,
      "MinValue": 128
    },
    "EnvironmentVariables": {
      "Type": "Json",
      "Description": "The environment variable set for the function, you can get the value of the environment variable in the function."
    },
    "Handler": {
      "Type": "String",
      "Description": "The function execution entry point."
    },
    "Timeout": {
      "Default": 3,
      "Type": "Number",
      "Description": "The maximum time duration a function can run, in seconds. After which Function Compute terminates the execution. Defaults to 3 seconds, and can be between 1 to 300 seconds.",
      "MaxValue": 300,
      "MinValue": 1
    },
    "Runtime": {
      "Type": "String",
      "Description": "The function runtime environment. Supporting nodejs6, nodejs8, python2.7, python3, java8",
      "AllowedValues": [
        "nodejs6",
        "nodejs8",
        "python2.7",
        "python3",
        "java8"
      ]
    },
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
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
    }
  }
}
```


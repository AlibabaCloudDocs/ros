# ALIYUN::ECS::Command {#concept_vbb_2ss_qgb .concept}

ALIYUN::ECS::Command类型用于新建[云助手](https://www.alibabacloud.com/help/doc-detail/64601.htm)命令。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_y9l_vqj_3h0 .language-json}
{
  "Type": "ALIYUN::ECS::Command",
  "Properties": {
    "Name": String,
    "WorkingDir": String,
    "CommandContent": String,
    "Timeout": Integer,
    "Type": String,
    "Description": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|命令名称，支持全字符集。长度不得超过 30 个字符。|无|
|WorkingDir|String|否|是|您创建的命令在 ECS 实例中运行的目录。|无|
|CommandContent|String|否|否| 命令 Base64 编码后的内容。

 当您传入请求参数 `Type` 后，必须同时传入该参数。

 该参数的值必须使用 Base64 编码后传输，且脚本内容的大小在 Base64 编码之后不能超过 16 KB。

 |无|
|Timeout|Integer|否|是| 您创建的命令在 ECS 实例中执行时最大的超时时间，单位为秒。

 当因为某种原因无法运行您创建的命令时，会出现超时现象；超时后，会强制终止命令进程，即取消命令的 PID。

 默认值：3600

 |无|
|Type|String|是|否| 命令的类型。

 取值范围： -   RunBatScript：创建一个在 Windows 实例中运行的 Bat 脚本
-   RunPowerShellScript：创建一个在 Windows 实例中运行的 PowerShell 脚本
-   RunShellScript：创建一个在 Linux 实例中运行的 Shell 脚本

 |无|
|Description|String|否|是|命令描述，支持全字符集。长度不得超过100个字符。|无|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   CommandId: 命令 ID。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_ngp_e83_u7r}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "WorkingDir": {
      "Type": "String",
      "Description": "The path where command will be executed in the instance."
    },
    "CommandContent": {
      "Type": "String",
      "Description": "The content of command. Content requires base64 encoding. Maximum size support 16KB."
    },
    "Type": {
      "Type": "String",
      "Description": "The type of command."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of command."
    },
    "Timeout": {
      "Type": "Number",
      "Description": "Total timeout when the command is executed in the instance. Input the time unit as second. Default is 3600s."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of command."
    }
  },
  "Resources": {
    "Command": {
      "Type": "ALIYUN::ECS::Command",
      "Properties": {
        "WorkingDir": {
          "Ref": "WorkingDir"
        },
        "CommandContent": {
          "Ref": "CommandContent"
        },
        "Type": {
          "Ref": "Type"
        },
        "Description": {
          "Ref": "Description"
        },
        "Timeout": {
          "Ref": "Timeout"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "CommandId": {
      "Description": "The id of command created.",
      "Value": {
        "Fn::GetAtt": [
          "Command",
          "CommandId"
        ]
      }
    }
  }
}
```


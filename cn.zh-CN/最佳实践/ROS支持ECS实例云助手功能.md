# ROS支持ECS实例云助手功能 {#concept_88451_zh .task}

本文为您介绍资源编排服务（ROS）支持的ECS实例云助手功能。

进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm)。

ROS新增以下两种资源类型，支持ECS实例云助手功能：

-   [ALIYUN::ECS::Command](https://ros.console.aliyun.com/?#/resourceType/detail/ALIYUN::ECS::Command/metadata) （用于创建云助手命令）
-   [ALIYUN::ECS::Invocation](https://ros.console.aliyun.com/#/resourceType/detail/ALIYUN::ECS::Invocation/metadata) （用于执行云助手命令）

通过以上ROS资源类型，您可以便捷的创建脚本，对运行中的一台或多台实例执行bat/PowerShell（Windows 实例）脚本或者Shell脚本（Linux 实例）。您也可以设置命令的执行周期，使实例维持在某种状态、获取实例监控以及日志信息或者守护进程等。[云助手概述](../../../../cn.zh-CN/运维与监控/云助手/云助手概述.md#)不会主动发起任何操作，所有的操作都在您的可控范围内。

## 创建云助手命令 {#section_2nk_3wq_k8q .section}

下例为您介绍如何通过ROS模板创建云助手命令。

``` {#codeblock_tmi_s05_qx9 .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "MyCommand": {
      "Type": "ALIYUN::ECS::Command",
      "Properties": {
        'Name': 'my-command',
        'Type': 'RunShellScript',
        'Description': 'my-command-description',
        'CommandContent': 'ZWNobyAxMjM='
      }
    }
  },
  "Outputs": {
    "CommandId": {
        "Value" : {"Fn::GetAtt": ["MyCommand", "CommandId"]}
    }
  }
}                    
```

在本例中，`Type`（资源类型）设置为`ALIYUN::ECS::Command`。`Properties`的设置如下：

-   `Name`表示命令名称。此处设置为`my-command`。
-   `Type`表示命令类型。此处设置为`RunShellScript`。
-   `Description`表示命令描述。此处设置为`my-command-description`。
-   `CommandContent`表示命令脚本Base64编码后的内容，大小不能超过16KB。此处设置为`ZWNobyAxMjM=`（echo 123 Base64 encoded）。

最后，通过`Outputs`标签返回新建命令的`CommandId`。

**说明：** 目前，云助手支持以下三种脚本：

-   Windows实例适用的Bat脚本（RunBatScript）
-   Windows实例适用的PowerShell脚本（RunPowerShellScript）
-   Linux实例适用的Shell脚本（RunShellScript）

## 执行云助手命令 {#section_r1g_9il_wni .section}

下例为您介绍如何通过ROS模板执行云助手命令。

``` {#codeblock_jzy_kko_v1u .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "MyCommand": {
      "Type": "ALIYUN::ECS::Command",
      "Properties": {
        'Name': 'my-command',
        'Type': 'RunShellScript',
        'Description': 'my-command-description',
        'CommandContent': 'ZWNobyAxMjM='
      }
    },
    "MyInvocation": {
      "Type": "ALIYUN::ECS::Invocation",
      "Properties": {
        'CommandId': { "Fn::GetAtt" : [ "MyCommand", "CommandId" ] },
        'InstanceIds': [
            "i-2zefq1f3ynnrr89qkzg9"
        ],
        'Timed': true,
        'Frequency': '0/10 0/1 * * * ?'
      }
    }
  },
  "Outputs": {
    "CommandId": {
        "Value" : {"Fn::GetAtt": ["MyCommand", "CommandId"]}
    },
    "InvokeId": {
        "Value" : {"Fn::GetAtt": ["MyInvocation", "InvokeId"]}
    }
  }
}            
```

在本例中，`Type`（资源类型）设置为`ALIYUN::ECS::Invocation`。`Properties`的设置如下：

-   `CommandId`表示命令ID。此处使用`Fn::GetAtt`方法从`MyCommand`中获取`CommandId`。
-   `InstanceIds`表示命令执行的实例ID列表。最多支持20台实例。实例需要为专有网络运行中的实例。
-   `Timed`表示命令是否周期执行。
-   `Frequency`表示命令执行周期。该参数取值遵循Cron表达式。详情请参见[Cron表达式](https://help.aliyun.com/knowledge_detail/64769.html)。

最后，通过`Outputs`标签返回新建命令的`CommandId`和`InvokeId`。

## 创建云助手资源栈 {#section_lyt_7l9_r32 .section}

1.  2.  单击左侧导航栏中的**资源栈管理**。
3.  单击右上角的**新建资源栈**。
4.  在**选择地域（region）**下拉列表中，选择您即将创建的资源的所属地域。
5.  在**模板源**下拉列表中，选择**直接输入**。
6.  填写**模板数据**。代码如下。 

    ``` {#codeblock_m52_xil_j8x .language-json}
    {
      "ROSTemplateFormatVersion" : "2015-09-01",
      "Resources" : {
        "MyCommand": {
          "Type": "ALIYUN::ECS::Command",
          "Properties": {
            'Name': 'my-command',
            'Type': 'RunShellScript',
            'Description': 'my-command-description',
            'CommandContent': 'ZWNobyAxMjM='
          }
        }
      },
      "Outputs": {
        "CommandId": {
            "Value" : {"Fn::GetAtt": ["MyCommand", "CommandId"]}
        }
      }
    }                    
    ```

7.  单击**下一步**。
8.  在资源栈配置页面，填写**栈名**和**创建超时（分钟）**。
9.  单击**创建**。


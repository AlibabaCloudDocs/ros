# ROS支持ECS实例云助手功能 {#concept_88451_zh .concept}

ROS新增如下两种资源类型，支持ECS实例云助手功能：

-   [ALIYUN::ECS::Command](https://ros.console.aliyun.com/?#/resourceType/detail/ALIYUN::ECS::Command/metadata) （创建命令）
-   [ALIYUN::ECS::Invocation](https://ros.console.aliyun.com/#/resourceType/detail/ALIYUN::ECS::Invocation/metadata) （执行命令）

通过以上ROS资源类型，您可以便捷的创建脚本，然后对运行中的一台或多台实例执行 bat/PowerShell（Windows 实例）脚本或者 Shell 脚本（Linux 实例）。

您也可以设置命令的执行周期，使实例维持在某种状态、获取实例监控以及日志信息或者守护进程等。[云助手](https://www.alibabacloud.com/help/doc-detail/64601.htm)不会主动发起任何操作，所有的操作都在您的可控范围内。

## 资源类型介绍 {#section_ldn_4xc_lfb .section}

ROS在云助手的API上进行了封装，提供了创建命令和执行命令两种资源类型。下面介绍如何使用这两种资源类型：

1.  **创建云助手命令** 

    下例介绍如何通过ROS模板创建一条命令。

    ``` {#codeblock_ezy_xs9_r8d .language-json}
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

    在这个例子里，`Type`（资源类型）设置为`ALIYUN::ECS::Command`，`Properties`里的设置如下：

    -   `Name`表示命令名称，此处设置为`my-command`。
    -   `Type`表示命令类型，此处设置为`RunShellScript`。
    -   `Description`表示命令描述，此处设置为`my-command-description`。
    -   `CommandContent`表示命令脚本Base64编码后的内容，大小不能超过16KB。此处设置为`ZWNobyAxMjM=` \(echo 123 Base64 encoded\)。
    最后，通过`Outputs`标签返回新建命令的`CommandId`。

    目前，云助手支持如下三种脚本：

    -   Windows 实例适用的 Bat 脚本（RunBatScript）
    -   Windows 实例适用的 PowerShell 脚本（RunPowerShellScript）
    -   Linux 实例适用的 Shell 脚本（RunShellScript）
2.  **执行云助手命令** 

    下例介绍如何通过ROS模板执行命令。

    ``` {#codeblock_5da_w62_j3n .language-json}
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

    在这个例子里，`Type`（资源类型）设置为`ALIYUN::ECS::Invocation`，`Properties`里的设置如下：

    -   `CommandId`表示命令ID，此处使用Fn::GetAtt方法从MyCommand中获取CommandId。
    -   `InstanceIds`表示命令执行的实例ID列表，最多支持20台实例。实例需要为专有网络运行中的实例。
    -   `Timed`表示命令是否周期执行。
    -   `Frequency`表示命令执行周期，该参数取值遵循Cron表达式。具体请参见[Cron表达式](https://www.alibabacloud.com/help/faq-detail/64769.htm)。
    最后，通过`Outputs`标签返回新建命令的`CommandId`和`InvokeId`。


## 创建云助手资源栈 {#section_985_que_j04 .section}

1.  登录 [资源编排控制台](http://ros.console.aliyun.com) 。
2.  单击左侧导航栏中的 **资源栈管理**。
3.  在资源栈管理页面，单击右上角的**新建资源栈**。
4.  填入模板名称、描述、模板数据等，然后单击**创建**即可。

如果执行命令失败，整个资源栈的资源将自动回滚。


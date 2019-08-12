# ROS support for the cloud assistant to manage ECS instances {#concept_88451_zh .concept}

This topic describes two new resource types: ALIYUN::ECS::Command and ALIYUN::ECS::Invocation. These resource types are provided by ROS for the cloud assistant, which is a client that enables you to manage your ECS instances more securely.

-   [ALIYUN::ECS::Command](https://ros.console.aliyun.com/?#/resourceType/detail/ALIYUN::ECS::Command/metadata): Creates a command.
-   [ALIYUN::ECS::Invocation](https://ros.console.aliyun.com/#/resourceType/detail/ALIYUN::ECS::Invocation/metadata): Runs a command.

You can use these ROS resource types to compile scripts and run these scripts on one or more ECS instances at a time. Specifically, you can run Bat or PowerShell scripts on ECS instances on which Windows is installed, or run Shell scripts on ECS instances on which Linux is installed.

Additionally, by using this client, you can specify the intervals at which a command is run. By doing so, you can keep your ECS instances in a specific state, while also obtaining the monitoring and log information from the ECS instance or implementing a daemon process. The [cloud assistant](https://www.alibabacloud.com/help/doc-detail/64601.htm) does not initiate any operation, allowing all operations to be in your control.

## Resource types {#section_ldn_4xc_lfb .section}

ROS is encapsulated by using the APIs in the cloud assistant to provide these two resource types.

1.  **Create a cloud assistant command** 

    The following example shows how to create a cloud assistant command by using an ROS resource stack template:

    ``` {#codeblock_ezy_xs9_r8d}
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

    In this example, the `Type` parameter is set to `ALIYUN::ECS::Command`. The options in the `Properties` parameter are as follows:

    -   `Name`: the name of the command. Value: `my-command`.
    -   `Type`: the type of the command. Value: `RunShellScript`.
    -   `Description`: the description of the command. Value: `my-command-description`.
    -   `CommandContent`: the Base64-encoded content of the command. The content size cannot exceed 16 KB. In this option, the `ZWNobyAxMjM` field indicates the Base64 code that is obtained by using the echo 123 command.
    The `CommandId` is returned in the `Outputs` tag.

    The cloud assistant supports the following three types of scripts:

    -   Bat script for ECS instances on which Windows is installed: `RunBatScript`
    -   PowerShell script for ECS instances on which Windows is installed: `RunPowerShellScript`
    -   Shell script for ECS instances on which Linux is installed: `RunShellScript`
2.  **Run a cloud assistant command** 

    The following example shows how to run a cloud assistant command by using an ROS resource stack template:

    ``` {#codeblock_5da_w62_j3n}
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

    In this example, the `Type` parameter is set to `ALIYUN::ECS::Invocation`. The options in the `Properties` parameter are as follows:

    -   `CommandId`: the ID of the command. The system calls the `Fn::GetAtt` built-in function to obtain the value of this option.
    -   `InstanceIds`: the IDs of the ECS instances on which the command is run. Up to 20 ECS instance IDs are allowed. The ECS instances must run in Virtual Private Clouds \(VPCs\).
    -   `Timed`: Specifies whether to run the command periodically.
    -   `Frequency`: the interval at which the command is run. Set this option following Cron expressions. For more information, see [Cron expressions](https://www.alibabacloud.com/help/faq-detail/64769.htm).
    The `CommandId` and `InvokeId` of the command are returned in the `Outputs` tag.


## Create a cloud assistant resource stack {#section_9j4_yc5_dmx .section}

1.  Log on to the [ROS console](https://partners-intl.console.aliyun.com/#/ros).
2.  In the left-side navigation pane, click **Stack Management**.
3.  In the upper right area of the displayed page, click **New Resource Stack**.
4.  Enter the template region, source, and data. Then click **Next**

If the cloud assistant resource stack failed to be created, the system automatically rolls back the resources of the entire stack.


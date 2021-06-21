# Automatically activate one or more cloud services

Alibaba Cloud Resource Orchestration Service \(ROS\) supports automated activation of one or more cloud services.

Before you activate a cloud service, you must know the billing method of the cloud service.

## Cloud services that can be automatically activated

For more information, see the valid values of the ServiceName parameter in [ALIYUN::ROS::AutoEnableService](/intl.en-US/Resource Types/ROS/ALIYUN::ROS::AutoEnableService.md).

## Activate a single cloud service

The following example shows how to activate a single cloud service. Log Service is used in the example.

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where you want to create the stack from the drop-down list.

4.  On the Stacks page, click **Create Stack** and select **Use New Resources \(Standard\)** from the drop-down list.

5.  In the Select Template step, select an existing template. Set **Template Import Method** to **Enter Template Content**, enter template content in the JSON format, and then click **Next**.

    In the following sample template, the ServiceName parameter is set to SLS and is referenced by the ALIYUN::ROS::AutoEnableService resource type to automatically activate Log Service.

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Parameters": {
        "ServiceName": {
          "Type": "String",
          "Default": "SLS"
        }
      },
      "Resources": {
        "AutoEnableService": {
          "Type": "ALIYUN::ROS::AutoEnableService",
          "Properties": {
            "ServiceName": {
              "Ref": "ServiceName"
            }
          }
        }
      }
    }
    ```

6.  In the Configure Template Parameters step, set **Stack Name**.

7.  Click **Create**.

    After the stack is created, you can log on to the [Log Service console](https://sls.console.aliyun.com) to check whether Log Service is activated.


## Activate multiple cloud services

The following example shows how to activate multiple cloud services. Log Service and Object Storage Service \(OSS\) are used in the example.

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where you want to create the stack from the drop-down list.

4.  On the Stacks page, click **Create Stack** and select **Use New Resources \(Standard\)** from the drop-down list.

5.  In the Select Template step, select an existing template. Set **Template Import Method** to **Enter Template Content**, enter template content in the JSON format, and then click **Next**.

    In the following sample template, the ServiceName parameter is set to SLS and OSS, and is referenced by ALIYUN::ROS::AutoEnableService in conjunction with the Count, Fn:Select, and Fn:Index functions. This way, Log Service and OSS are automatically activated.

    For more information about these functions, see [Functions](/intl.en-US/Template/Template syntax/Functions.md).

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Parameters": {
        "ServiceName": {
          "Type": "Json",
          "Default": ["SLS", "OSS"]
        }
      },
      "Resources": {
        "AutoEnableService": {
          "Type": "ALIYUN::ROS::AutoEnableService",
          "Properties": {
            "ServiceName": {
              "Fn::Select": [{ "Ref": "ALIYUN::Index" }, { "Ref": "ServiceName" }]
            }
          },
          "Count": {
            "Fn::Length": { "Ref": "ServiceName" }
          }
        }
      }
    }
    ```

6.  In the Configure Template Parameters step, set **Stack Name**.

7.  Click **Create**.

    After the stack is created, you can log on to the [Log Service console](https://sls.console.aliyun.com) and the [OSS console](https://oss.console.aliyun.com/) to check whether Log service and OSS are activated.



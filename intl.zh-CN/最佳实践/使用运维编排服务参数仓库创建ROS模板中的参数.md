# 使用运维编排服务参数仓库创建ROS模板中的参数

当您需要多次查询ROS模板中某个参数时，可以将参数值存储在阿里云运维编排服务OOS（Operation Orchestration Service）的参数仓库中，然后在ROS模板中输入该参数名称即可。

OOS参数仓库中可以存储普通参数或加密参数，加密参数可以将保存的值通过KMS服务进行加密。本文以创建一组ECS实例为例，为您介绍使用OOS参数仓库创建参数，并编写ROS模板引用这些参数的方法。本示例将会创建以下参数：

|参数|参数名称|参数种类|参数类型|参数值|
|--|----|----|----|---|
|ImageId|my\_image|普通参数|String|centos\_7\_9\_x64\_20G\_alibase\_2020\*\*\*\*.vhd|
|SecurityGroupIds|security\_group\_ids|普通参数|StringList|sg-group1,sg-group2|
|Password|Password|加密参数|Secret|MyPassword1|

关于参数的更多信息，请参见[ALIYUN::ECS::InstanceGroup](/intl.zh-CN/资源类型/ECS/ALIYUN::ECS::InstanceGroup.md)。

**说明：** 创建参数时，您需要选择与资源栈相同的地域。例如：您将使用模板在**华东1（杭州）**创建资源栈，则需要将参数存储到相同地域。

## 步骤一：在运维编排控制台创建参数

1.  登录[运维编排控制台](https://oos.console.aliyun.com/cn-qingdao/overview)。

2.  在页面左上角的地域下拉列表，选择参数的所在地域。

    参数的所在地域需要和资源栈所在地域相同，本示例为**华东1（杭州）**。

3.  在左侧导航栏，单击**参数仓库**。

4.  创建普通参数ImageId。

    1.  在参数仓库页面，单击**普通参数**，然后单击**创建普通参数**。

    2.  在创建普通参数页面，配置**参数名称**和**值**，选择**参数类型**。

        本示例中，您需要进行如下配置：

        -   **参数名称**：my\_image。
        -   **参数类型**：String。
        -   **值**：centos\_7\_9\_x64\_20G\_alibase\_2020\*\*\*\*.vhd。
    3.  单击**创建**。

        创建完成后，您可以在**普通参数**页签，单击ImageId参数名称，在**描述**页签查看名称、版本、类型、值等信息。

5.  创建普通参数SecurityGroupIds。

    1.  在参数仓库页面，单击**普通参数**，然后单击**创建普通参数**。

    2.  在创建普通参数页面，配置**参数名称**和**值**，选择**参数类型**。

        本示例中，您需要进行如下配置：

        -   **参数名称**：security\_group\_ids。
        -   **参数类型**：StringList。
        -   **值**：sg-group1,sg-group2。
    3.  单击**创建**。

        创建完成后，您可以在**普通参数**页签，单击SecurityGroupIds参数名称，在**描述**页签查看名称、版本、类型、值等信息。

6.  创建加密参数Password。

    1.  在参数仓库页面，单击**加密参数**，然后单击**创建加密参数**。

    2.  在创建加密参数页面，配置**参数名称**和**值**，选择**KMS密钥ID**。

        本示例中，您需要进行如下配置：

        -   **参数名称**：Password。
        -   **KMS密钥ID**：Default Service CMK。
        -   **值**：MyPassword1。
    3.  单击**创建**。

        创建完成后，您可以在**加密参数**页签，单击Password参数名称，在**描述**页签单击**值**右侧的**显示**，获取Password取值。

        ![加密参数](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8165371161/p232882.png)


## 步骤二：编写ROS模板

当您创建参数后，可以编写ROS模板，在Parameters或Resources中引用参数：

-   在Parameters中引用

    您需要将Type设置为ALIYUN::OOS::Parameter::Value （普通参数）或ALIYUN::OOS::SecretParameter::Value（加密参数）。

    例如：您可以通过如下代码引用普通参数ImageId的最新版本取值。

    ```
    "Parameters": {
      "ImageId":{
        "Type":"ALIYUN::OOS::Parameter::Value",
        "Default": "my_image"
      }
    }
    ```

    您也可以将参数设置为my\_image:1，表示引用版本1的取值。

-   在Resources中引用

    您可以在Resource的Properties中引用参数，格式为：`{{resolve:<参数类型>:<参数名称>:<参数版本号>}}`。

    -   参数类型（必填）

        存储参数的服务。取值：

        -   oos：普通参数。
        -   oos-secret：加密参数。
    -   参数名称（必填）

        参数的名称。

    -   参数版本号（选填）

        参数的版本，若不填写则为最新版本。

    例如：您可以通过如下代码引用普通参数ImageId的最新版本取值、加密参数Password版本2的取值。

    ```
    "Resources": {
      "ECS": {
        "Type": "ALIYUN::ECS::Instance",
        "Properties": {
          "ImageId": "{{resolve:oos:my_image}}",
          "Password": "{{resolve:oos-secret:Password:2}}",
          ...
        }
      }
    }
    ```


模板中引用参数时支持大部分函数。更多信息，请参见[函数（Functions）](/intl.zh-CN/模板/模板语法/函数（Functions）.md)。不支持的函数为：Ref、Fn::GetAtt、Fn::GetStackOutput、Fn::Calculate。

本示例中模板如下：

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceType": {
      "Type": "String",
      "Default": "ecs.c6.large"
    },
    "ImageId": {
      "Type": "ALIYUN::OOS::Parameter::Value",
      "Default": "my_image"
    },
    "Vpc": {
      "Type": "String"
    },
    "VSwitch": {
      "Type": "String"
    }
  },
  "Resources": {
    "ECS": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "ImageId": {
          "Ref": "ImageId"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "VpcId": {
          "Ref": "Vpc"
        },
        "VSwitchId": {
          "Ref": "VSwitch"
        },
        "SecurityGroupIds": "{{resolve:oos:security_group_ids:1}}",
        "Password": "{{resolve:oos-secret:Password}}",
        "MaxAmount": 1
      }
    }
  },
  "Outputs": {
    "InstanceIds": {
      "Value": {
        "Fn::GetAtt": [
          "ECS",
          "InstanceIds"
        ]
      }
    }
  }
}
```

ROS模板引用的参数会基于OOS参数类型进行转换。当前OOS参数支持String和StringList类型，如果引用了StringList类型参数，ROS会将其转换为List类型在模板中使用。例如：类型为StringList的参数SecurityGroupIds，值为sg-group1,sg-group2。当您创建ALIYUN::ECS::InstanceGroup资源时，SecurityGroupIds取值将解析为\["sg-group1", "sg-group2"\]。

## 步骤三：在资源编排控制台创建资源栈

在资源编排控制台使用步骤二中的示例模板创建资源栈，创建一组ECS实例。具体操作，请参见[创建资源栈](/intl.zh-CN/资源栈/创建资源栈.md)。

资源栈创建成功后，您可以在资源编排控制台左侧菜单栏单击**资源栈**，在**资源栈列表**页面找到目标资源栈并单击资源栈名称，在资源栈详情页单击**参数**页签查看参数及取值，验证模板参数引用是否正确。


# 基于Conditions在不同操作系统创建IPv4和IPv6双栈云服务器

通过创建或更新资源栈，ROS支持设置不同的条件，从而在不同的操作系统中创建IPv4和IPv6双栈云服务器。

## 背景信息

当您创建绑定IPv4和IPv6地址的ECS服务器时，需要单独创建IPv6网关，开通IPv6公网带宽并配置公网地址，并且对于不同操作系统的配置方式存在差异，这将增加您的使用成本和出错概率。此时您可以使用模板示例，在不同的操作系统中创建IPv4和IPv6双栈云服务器。

条件（Conditions）由Fn::And、Fn::Or、Fn::Not和Fn::Equals中的一个或多个函数定义，根据您在创建或更新资源栈时，指定的输入参数值进行计算。在每个条件中，都可以引用其他条件、参数值或映射。本文以创建绑定IPv4和IPv6双栈云服务器为例为您介绍。关于模板示例的更多信息，请参见[创建绑定IPv4和IPv6双栈云服务器](https://rosnext.console.aliyun.com/cn-beijing/samples/Ecs_Ipv6_Instance)。

在模板中根据Parameters的InstanceImageId参数是否以centos开头做为判断条件，在Conditions对象中使用Fn::Equals、Fn::Select、Fn::Split函数对所选择的InstanceImageId做数据处理与逻辑判断。代码示例如下：

```
{
  "Parameters": {
    "InstanceImageId": {
      "Type": "String",
      "Default": "centos_7",
      "Description": {
        "zh-cn": "镜像ID, <br>Linux系统请选择：<font color='red'><b>centos_7</b></font> <br>Windows系统请选择：<font color='red'><b>win2008r2；win2012r2；win2016</b></font>",
        "en": "Image ID，<br>Linux System Select：<font color='red'><b>centos_7</b></font> <br>Windows System Select：<font color='red'><b>win2008r2；win2012r2；win2016</b></font>"
      },
      "Label": {
        "zh-cn": "镜像",
        "en": "Image"
      }
    }
  },
  "Conditions": {
    "CreateLinux": {
      "Fn::Equals": [
        "centos",
        {
          "Fn::Select": [
            "0",
            {
              "Fn::Split": [
                "_",
                {
                  "Ref": "InstanceImageId"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

创建ECS初始化UserData时，使用Fn::If函数判断Conditions对象CreateLinux，实现选择不同操作系统执行不同初始化命令的需求，然后创建IPv4和IPv6双栈云服务器。代码示例如下：

```
{
          "Fn::If": [
            "CreateLinux",
            {
              "Fn::Replace": [
                {
                  "ros-notify": {
                    "Fn::GetAtt": [
                      "WaitConditionHandle",
                      "CurlCli"
                    ]
                  }
                },
                {
                  "Fn::Join": [
                    "",
                    [
                      "#!/bin/sh",
                      " \n",
                      "cd /opt \n",
                      "wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6 \n",
                      "chmod +x ./ecs-utils-ipv6 \n",
                      "./ecs-utils-ipv6 \n",
                      "ros-notify -d \"{\\\"Data\\\" : \\\"SUCCESS\\\", \\\"Status\\\" : \\\"SUCCESS\\\"}\" \n"
                    ]
                  ]
                }
              ]
            },
            {
              "Fn::Replace": [
                {
                  "ros-notify": {
                    "Fn::GetAtt": [
                      "WaitConditionHandle",
                      "PowerShellCurlCli"
                    ]
                  }
                },
                {
                  "Fn::Join": [
                    "",
                    [
                      "[powershell]\r\n",
                      "New-Item -Path \"C:\\set_ipv6\" -Force -type directory\r\n",
                      "cd C:\\set_ipv6 \r\n",
                      "$install_dir=\"C:\\set_ipv6\" \r\n",
                      "$install_path = \"$install_dir\\ecs-utils-ipv6.exe\" \r\n",
                      "$tool_url = 'http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/64/ecs-utils-ipv6.exe' \r\n",
                      "Invoke-WebRequest -uri $tool_url -OutFile $install_path \r\n",
                      "Unblock-File $install_path \r\n",
                      "Start-Process -FilePath \"$install_path\" -ArgumentList \"--noenterkey\" -NoNewWindow \r\n",
                      "ros-notify\r\n"
                    ]
                  ]
                }
              ]
            }
          ]
        }
```

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，选择**模板** \> **模板示例**。

3.  查找模板**创建绑定IPv4/IPv6双栈的云服务器**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**专有网络IPv4网段**|专有网络的IPv4网段。推荐使用以下网段：    -   10.0.0.0/8
    -   172.16.0.0/12
    -   192.168.0.0/16
更多信息，请参见[专有网络和交换机概述](/cn.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|192.168.0/16|
    |**交换机IPv4网段**|专有网络下交换机的IPv4网段。更多信息，请参见[专有网络和交换机概述](/cn.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|192.168.0.0/24|
    |**交换机可用区**|专有网络下的交换机可用区ID。|华北1可用区C|
    |**镜像**|ECS实例的镜像ID。可选择Linux（Centos）系列镜像或Windows系列镜像。更多信息，请参见[镜像概述](/cn.zh-CN/镜像/镜像概述.md)。

|centos\_7|
    |**实例规格**|ECS实例规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**系统盘空间**|ECS实例的系统盘空间。取值范围：40~500

单位：GB

|40|
    |**分配IPv4公网IP**|是否为ECS实例分配IPv4公网地址。    -   选中方框：分配公网地址。
    -   不选中方框：不分配公网地址。
|选中方框|
    |**IPv6公网带宽的计费方式**|IPv6公网带宽的计费方式。取值：    -   PayByTraffic：按流量计费。
    -   PayByBandwidth：按带宽计费。
|PayByTraffic|
    |**IPv6网关公网带宽**|IPv6网关的公网带宽。取值范围：1~5000

单位：Mbps

|10|
    |**IPv6网关的规格**|IPv6网关的规格。取值：    -   Small：免费版。
    -   Medium：企业版。
    -   Large：企业增强版。
|Small|
    |**系统盘类型**|ECS实例的系统盘类型。取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/cn.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**实例密码**|ECS实例的登录密码。|Test\_12\*\*\*\*|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取EcsInstanceIpv6Address，管理IPv6云服务器。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，并绑定IPv4和IPv6地址。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |
    |ALIYUN::VPC::Ipv6Gateway|1|创建一个IPv6网关。|IPv6网关是专有网络的一个IPv6互联网流量网关。一个VPC仅允许创建一个IPv6网关。|
    |ALIYUN::ECS::VPC|1|创建一个交换机，用于管理单个可用区下的实例。|无|
    |ALIYUN::ECS::VSwitch|1|创建一个安全组，用于在云端划分安全域。|无|

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



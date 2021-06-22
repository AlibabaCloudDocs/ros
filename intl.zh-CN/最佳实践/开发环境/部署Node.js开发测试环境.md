# 部署Node.js开发测试环境

资源编排服务ROS（Resource Orchestration Service）支持通过创建资源栈的方式一键部署Node.js开发测试环境。

模板示例[部署Node.js开发测试环境](https://rosnext.console.aliyun.com/cn-beijing/samples/Nodejs_Single_Instance)基于Centos7系统创建ECS实例并安装Node.js相关应用。使用模板创建资源栈成功后即可获取WebsiteURL，登录Node.js测试页面。

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，选择**模板** \> **模板示例**。

3.  查找模板**部署Node.js开发测试环境**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**VPC名称**|专有网络名称。更多信息，请参见[专有网络和交换机概述](/intl.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|DefaultVPCTest|
    |**VPC网段**|专有网络IP地址段。更多信息，请参见[专有网络和交换机概述](/intl.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|192.168.0/16|
    |**交换机网段**|交换机IP地址段。必须为专有网络子网段。更多信息，请参见[专有网络和交换机概述](/intl.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|192.168.1.0/24|
    |**可用区**|ECS可用区ID。|华北1可用区C|
    |**镜像ID**|ECS镜像ID。默认使用centos\_7。更多信息，请参见[镜像概述](/intl.zh-CN/镜像/镜像概述.md)。

|centos\_7|
    |**ECS实例名称**|ECS实例的名称。更多信息，请参见[实例概述](/intl.zh-CN/实例/实例概述.md)。

|DefaultECSInstanceTest|
    |**ECS实例规格**|ECS实例的规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**系统盘类型**|ECS系统盘的类型。取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/intl.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**ECS实例密码**|ECS实例的密码。|Test\_12\*\*\*\*|
    |**Node.js地址**|Node.js安装包下载地址。|https://nodejs.org/dist/v6.9.5/node-v6.9.5-linux-x64.tar.xz|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取WebsiteURL。

8.  访问WebsiteURL，登录Node.js测试页面。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于部署Node.js开发环境。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |
    |ALIYUN::ECS::VPC|1|创建一个专有网络，用于增强云上网络的安全性。|无|
    |ALIYUN::ECS::VSwitch|1|创建一个交换机，用于管理单个可用区下的实例。|无|

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



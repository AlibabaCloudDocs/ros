# 安装LAMP环境

资源编排服务ROS（Resource Orchestration Service）支持通过创建资源栈的方式一键安装LAMP环境。

LAMP（Linux+Apache+MySQL+PHP）网站架构是目前国际流行的Web框架，包括Linux操作系统、Apache网络服务器、MySQL数据库和PHP编程语言，所有组成产品均为开源软件。LAMP环境具有通用、跨平台、高性能、低价格的特点。

模板示例[部署LAMP（Linux+Apache+MySQL+PHP）环境](https://rosnext.console.aliyun.com/cn-beijing/samples/LAMP_Basic)在已有专有网络、交换机和安全组等资源的基础上，默认创建Centos系统并安装Apache、MySQL、PHP等必要软件。使用模板创建资源栈成功后即可获取ApacheWebURL，登录Apache管理控制台。

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏选择**模板** \> **模板示例**。

3.  查找模板**部署LAMP\(Linux+Apache+MySQL+PHP\)环境**。

4.  单击右上角的**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**现有VPC的实例ID**|VPC实例ID。关于如何创建和查看VPC实例，请参见[使用专有网络](/intl.zh-CN/专有网络和交换机/使用专有网络.md)。

|vpc-bp1m6fww66xbntjyc\*\*\*\*|
    |**网络交换机ID**|专有网络下的交换机ID。关于如何创建和查看交换机，请参见[使用交换机](/intl.zh-CN/专有网络和交换机/使用交换机.md)。

|vsw-bp183p93qs667muql\*\*\*\*|
    |**交换机可用区**|专有网络下的交换机可用区ID。|华东1可用区K|
    |**镜像**|ECS镜像ID。默认使用centos\_7。更多信息，请参见[镜像概述](/intl.zh-CN/镜像/镜像概述.md)。

|centos\_7|
    |**实例规格**|ECS实例的规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**系统盘类型**|ECS系统盘的类型。取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/intl.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**实例密码**|ECS实例的密码。|Test\_12\*\*\*\*|
    |**数据库名称**|RDS MySQL数据库名称。更多信息，请参见[RDS MySQL数据库概述](/intl.zh-CN/RDS MySQL 数据库/概述.md)。

|MyDatabase|
    |**数据库用户名**|RDS MySQL数据库用户名。|DefaultUser|
    |**数据库用户密码**|RDS MySQL数据库用户密码。|Test\_23\*\*\*\*|
    |**数据库管理员用户密码**|RDS MySQL数据库管理员用户密码。|Test\_34\*\*\*\*|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取ApacheWebURL。

8.  访问ApacheWebURL，登录Apache管理控制台。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于安装LAMP服务。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



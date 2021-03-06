# 安装Spark单机版

资源编排服务ROS（Resource Orchestration Service）支持通过创建资源栈的方式安装Spark单机版。

Apache Spark是专为大规模数据处理设计的通用计算引擎。Spark将Scala用作其应用程序框架，启用了内存分布数据集，除了能够提供交互式查询外，还可以迭代优化工作负载。

模板示例[Spark单机版（已有VPC）](https://rosnext.console.aliyun.com/cn-beijing/samples/Existing_Vpc_Single_Spark?accounttraceid=b750b4b4558b43cda74f1beab616dab8uecb)在已有专有网络、交换机和安全组等资源的基础上，创建一台ECS实例并绑定弹性公网IP（EIP）。模板示例中使用的软件版本如下：

-   Java JDK（Java Development Kit）：1.8.0
-   Hadoop（分布式系统基础架构）：2.7.7
-   Scala（编程语言）：2.12.1
-   Spark（计算引擎）：2.1.0

使用模板创建资源栈成功后即可获取SparkWebSiteURL，登录Spark管理控制台。如需通过外网访问SparkWebSiteURL，请在安全组添加入方向8088和8080访问规则。具体操作，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，选择**模板** \> **模板示例**。

3.  查找模板**Spark 单机版\(已有VPC\)**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**现有VPC的实例ID**|VPC实例ID。关于如何创建和查询VPC实例，请参见[使用专有网络](/intl.zh-CN/专有网络和交换机/使用专有网络.md)。

|vpc-bp1m6fww66xbntjyc\*\*\*\*|
    |**交换机可用区**|专有网络下的交换机可用区ID。|华东1可用区K|
    |**网络交换机ID**|专有网络下的交换机ID。关于如何创建和查询交换机，请参见[使用交换机](/intl.zh-CN/专有网络和交换机/使用交换机.md)。

|vsw-bp183p93qs667muql\*\*\*\*|
    |**业务安全组ID**|ECS安全组ID。关于如何查询安全组ID，请参见[查询安全组](/intl.zh-CN/安全/安全组/管理安全组/查询安全组.md)。

|sg-bp15ed6xe1yxeycg7o\*\*\*\*|
    |**实例规格**|ECS实例规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**镜像ID**|ECS镜像ID，默认使用centos\_7。更多信息，请参见[镜像概述](/intl.zh-CN/镜像/镜像概述.md)。

|centos\_7|
    |**实例密码**|ECS实例密码。|Test\_12\*\*\*\*|
    |**磁盘类型**|取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/intl.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**系统盘空间**|实例系统盘大小。取值范围：40~500

单位：GB

|40|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取SparkWebSiteURL。

8.  访问SparkWebSiteURL，登录Spark管理控制台。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于安装Spark单机版。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



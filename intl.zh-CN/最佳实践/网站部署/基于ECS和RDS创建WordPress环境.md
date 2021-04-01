# 基于ECS和RDS创建WordPress环境

本文为您介绍如何使用ROS模板示例基于ECS和RDS创建WordPress环境。

WordPress是一款使用PHP语言和MySQL数据库开发的博客平台。您可以使用ROS的模板示例[基于ECS和RDS创建WordPress环境](https://rosnext.console.aliyun.com/cn-beijing/samples/Wordpress_Instance)，创建CentOS 7系统的ECS实例和RDS MySQL数据库实例，搭建WordPress环境。

## 创建资源栈

1.  登录[ROS控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，选择**模板** \> **模板示例**。

3.  查找模板**基于ECS和RDS创建WordPress环境**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|
    |--|--|
    |VPC CIDR Block|VPC网段。|
    |VSwitch Availability Zone|交换机可用区ID。|
    |VSwitch CIDR Block|交换机网段，必须为专有网络子网段。|
    |Instance Type|ECS实例规格。|
    |Image|镜像ID，默认使用centos\_7。|
    |Instance Password|ECS实例密码。|
    |DB Instance Class|RDS实例规格。|
    |Engine|数据库引擎类型及版本。|
    |DB Instance Storage|数据库存储空间。|
    |DB Name|RDS MySQL数据库名称。|
    |DB Username|RDS MySQL数据库账号。|
    |DB Password|RDS MySQL数据库密码。|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取WordPressUrl。

    ![WordPress](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5154046161/p253673.png)

8.  访问WordPressUrl，登录WordPress管理控制台。


## 查看资源

1.  登录[ROS控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于部署WordPress服务。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。
    -   单台价格：0.62元/小时。
    -   公网流量费用：0.80元/GB。 |
    |ALIYUN::ECS::VPC|1|创建一个专有网络，用于保证网络的安全性。|无|
    |ALIYUN::ECS::VSwitch|1|在专有网络下创建一个交换机，用于管理单个可用区下的实例。|无|
    |ALIYUN::RDS::DBInstance|1|创建一个RDS MySQL数据库，用于存储WordPress的服务数据。|实例规格、存储空间参数会影响成本。    -   存储空间：5GB。
    -   默认规格： rds.mysql.t1.small（1 核 1GB）。 |



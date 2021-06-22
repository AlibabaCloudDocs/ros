# 部署Java Web开发测试环境

资源编排服务ROS（Resource Orchestration Service）支持通过创建资源栈的方式一键部署Java Web开发测试环境。

ROS模板示例[部署Java Web开发测试环境](https://rosnext.console.aliyun.com/cn-beijing/samples/Java_Web_Single_Instance)基于Centos7系统创建ECS实例并安装Tomcat与JDK（Java Development Kit）应用。Tomcat作为免费开源的Web应用服务器，具有技术先进、性能稳定的优点。使用模板创建资源栈成功后即可获取WebsiteURL，登录Tomcat管理控制台。

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，选择**模板** \> **模板示例**。

3.  查找模板**部署Java Web开发测试环境**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**专有网络网段**|专有网络IP地址段。更多信息，请参见[专有网络和交换机概述](/cn.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|192.168.0/16|
    |**交换机网段**|交换机IP地址段。必须为专有网络子网段。更多信息，请参见[专有网络和交换机概述](/cn.zh-CN/专有网络和交换机/专有网络和交换机概述.md)。

|192.168.1.0/24|
    |**ECS镜像ID**|ECS的镜像ID。默认使用centos\_7。更多信息，请参见[镜像概述](/cn.zh-CN/镜像/镜像概述.md)。

|centos\_7|
    |**ECS实例规格**|ECS实例的规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**ECS系统盘规格**|ECS系统盘的规格。取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/cn.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**ECS实例密码**|ECS实例的密码。|Test\_12\*\*\*\*|
    |**Tomcat下载地址**|Tomcat官方下载地址。|http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.41/bin/apache-tomcat-8.5.41.tar.gz|
    |**Tomcat安装目录**|Tomcat的安装目录。|/usr/local/tomcat/apache-tomcat-8.5.41|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取WebsiteURL。

8.  访问WebsiteURL，登录Tomcat管理控制台。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于部署Java Web开发测试环境。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |
    |ALIYUN::ECS::VPC|1|创建一个专有网络，用于增强云上网络的安全性。|无|
    |ALIYUN::ECS::VSwitch|1|创建一个交换机，用于管理单个可用区下的实例。|无|

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



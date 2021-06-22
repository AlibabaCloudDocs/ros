# 安装Etcd单机版

资源编排服务ROS（Resource Orchestration Service）支持通过创建资源栈的方式安装Etcd单机版。

Etcd是一个分布式键值对存储系统，用于保存关键数据。通过分布式锁、Leader选举和写屏障（write barriers）来实现可靠的分布式协作。

模板示例[Etcd单机版-已有专有网络VPC](https://rosnext.console.aliyun.com/cn-beijing/samples/Existing_Vpc_Docker_Single_Etcd?accounttraceid=2c2ee7e0b96840ca86798e9990ca4f3ciyzs)在已有专有网络、交换机和安全组等资源的基础上，将Etcd应用部署在Centos7操作系统中。

使用模板创建资源栈成功后即可获取EtcdServerWebUrl，登录Etcd管理控制台。如需通过外网访问EtcdServerWebUrl，请在安全组添加入方向8000访问规则。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，选择**模板** \> **模板示例**。

3.  查找模板**Etcd 单机版- 已有专有网络VPC**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**交换机可用区**|专有网络下的交换机可用区ID。|华北1可用区C|
    |**现有VPC的实例ID**|VPC实例ID。关于如何创建和查询VPC实例，请参见[使用专有网络](/cn.zh-CN/专有网络和交换机/使用专有网络.md)。

|vpc-bp1m6fww66xbntjyc\*\*\*\*|
    |**网络交换机ID**|专有网络下的交换机ID。关于如何创建和查询交换机，请参见[使用交换机](/cn.zh-CN/专有网络和交换机/使用交换机.md)。

|vsw-bp183p93qs667muql\*\*\*\*|
    |**业务安全组ID**|ECS安全组ID。关于如何查询安全组ID，请参见[查询安全组](/cn.zh-CN/安全/安全组/管理安全组/查询安全组.md)。

|sg-bp15ed6xe1yxeycg7o\*\*\*\*|
    |**实例规格**|ECS实例规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**系统盘类型**|取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/cn.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**系统盘空间**|系统盘大小。取值范围：40~500

单位：GB

|40|
    |**实例密码**|ECS实例密码。|Test\_12\*\*\*\*|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取EtcdServerWebUrl。

8.  访问EtcdServerWebUrl，登录Etcd管理控制台。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于安装Etcd单机版。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



# 安装Kafka集群版

资源编排服务ROS（Resource Orchestration Service）支持通过创建资源栈的方式安装Kafka集群版。

Apache Kafka是一个开源流处理平台，使用Scala和Java语言编写。Kafka作为一种高吞吐量的分布式发布订阅消息系统，可以处理消费者模式网站中的所有动作流数据。

模板示例[Kafka 集群版-已有专有网络VPC](https://rosnext.console.aliyun.com/cn-beijing/solutions/Existing_Vpc_Cluster_Kafka?isSolution=true)在已有专有网络、交换机和安全组等资源的基础上，创建多台ECS实例。其中一台ECS实例绑定弹性公网IP（EIP）作为管理节点，其他ECS实例使用弹性伸缩进行管理。模板示例中使用的软件版本如下：

-   Java JDK（Java Development Kit）：1.8.0
-   Scala（编程语言）：2.12
-   Kafka（计算引擎）：0.10.2.2

模板示例中的Kafka数据存储在数据盘中，默认路径为：`/home/software/`。默认Kafka bin目录路径为：`/home/software/kafka/bin`。

使用模板创建资源栈成功后即可获取KafkaManagerUrl，登录Kafka管理控制台。如需通过外网访问KafkaManagerUrl，请在安全组添加入方向9000访问规则。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

## 步骤一：创建资源栈

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**解决方案中心**。

3.  查找模板**Kafka 集群版 - 已有专有网络VPC**。

4.  单击**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，并设置以下参数。

    |参数|说明|示例|
    |--|--|--|
    |**现有VPC的实例ID**|VPC实例ID。关于如何创建和查询VPC实例，请参见[使用专有网络](/cn.zh-CN/专有网络和交换机/使用专有网络.md)。

|vpc-bp1m6fww66xbntjyc\*\*\*\*|
    |**交换机可用区**|专有网络下的交换机可用区ID。|华北1可用区C|
    |**网络交换机ID**|专有网络下的交换机ID。关于如何创建和查询交换机，请参见[使用交换机](/cn.zh-CN/专有网络和交换机/使用交换机.md)。

|vsw-bp183p93qs667muql\*\*\*\*|
    |**业务安全组ID**|ECS安全组ID。关于如何查询安全组ID，请参见[查询安全组](/cn.zh-CN/安全/安全组/管理安全组/查询安全组.md)。

|sg-bp15ed6xe1yxeycg7o\*\*\*\*|
    |**实例规格**|ECS实例规格。请选用有效的实例规格。更多信息，请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。

|ecs.c5.large|
    |**实例密码**|ECS实例密码。|Test\_12\*\*\*\*|
    |**公网IP带宽值**|公网IP带宽。单位：Mbps

|5|
    |**磁盘类型**|取值：    -   cloud\_efficiency：高效云盘。
    -   cloud\_ssd：SSD云盘。
    -   cloud\_essd：ESSD云盘。
    -   cloud：普通云盘。
    -   ephemeral\_ssd：本地SSD盘。
更多信息，请参见[云盘概述](/cn.zh-CN/块存储/块存储介绍/云盘概述.md)。

|cloud\_efficiency|
    |**数据盘空间**|实例数据盘大小。取值范围：20~32,786

单位：GB

|20|
    |**Kafka监听端口**|请使用1000以上的端口号。默认值：9092

|9092|
    |**消息保留时间**|消息最长保留时间。默认值：24

单位：小时

|24|
    |**Topic规格**|Topic数量。默认值：50

|50|
    |**实例数量**|Kafka集群数量。取值范围：3~10

|3|

6.  单击**创建**。

7.  在**资源栈信息**页签查看资源栈状态。资源栈创建成功后，单击**输出**，获取KafkaManagerUrl。

8.  访问KafkaManagerUrl，登录Kafka管理控制台。


## 步骤二：查看资源

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**资源栈**。

3.  在资源栈列表页面，单击目标资源栈名称。

4.  单击**资源**页签，查看资源信息。

    本示例中，资源信息如下表所示。

    |资源|数量|资源说明|规格说明|
    |--|--|----|----|
    |ALIYUN::ECS::Instance|1|创建一台云服务器，用于安装Kafka Master服务。|    -   总数量：1台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |
    |ALIYUN::ESS::ScalingGroup|2|创建两个弹性伸缩组，用于安装Kafka Slave服务。弹性伸缩组会根据您设置的伸缩规则自动为您调整弹性计算资源大小，以满足您业务需求的变化。

|    -   总数量：2台。
    -   实例规格：ecs.c5.large。
    -   磁盘类别：高效云盘。
    -   系统盘空间：40GB。
    -   分配公网IP：是。 |
    |ALIYUN::RAM::Role|1|创建一个RAM角色，用于颁发短时有效的访问令牌（STS令牌），使其成为一种更安全的授予访问权限的方法。|无|
    |ALIYUN::VPC::EIP|1|创建一个弹性公网IP，用于绑定ECS实例，以便通过外网访问ECS实例。|无|
    |ALIYUN::OOS::Template|1|创建一个运维编排模板，用于创建生命周期挂钩。关于生命周期挂钩的更多信息，请参见[生命周期挂钩](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/生命周期挂钩和OOS模板最佳实践概述.md)。

|无|

    **说明：** 资源收费情况，请参见官网报价或各产品定价文档。



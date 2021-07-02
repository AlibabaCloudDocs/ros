# Estimate resource prices

Some resources used in templates incur charges. You can query the prices of resources in a template by using the Resource Orchestration Service \(ROS\) console or calling an API operation.

## Methods

You can estimate resource prices by using one of the following methods:

-   ROS console: If the resources of a template used to create a stack support price query, ROS provides the estimated prices in the **Check and Confirm** step of the Use New Resources \(Standard\) or Use Existing Resources \(Resource Import\) wizard. The prices provided are for reference only. The actual prices are subject to changes.
-   API: You can call the [GetTemplateEstimateCost](/intl.en-US/API Reference/Template operations/GetTemplateEstimateCost.md) operation to query resource prices.

## Supported resource types

**Note:** The billing method of a resource is determined by the corresponding parameter in the template. For example, if you set the InstanceChargeType parameter in the ALIYUN::ECS::Instance resource type to PrePaid, created Elastic Compute Service \(ECS\) instances are billed on a subscription basis.

|Alibaba Cloud service|Resource type|
|---------------------|-------------|
|Cloud Enterprise Network \(CEN\)|[ALIYUN::CEN::CenBandwidthPackage](/intl.en-US/Resource Types/CEN/ALIYUN::CEN::CenBandwidthPackage.md)|
|PolarDB-X|[ALIYUN::DRDS::DrdsInstance](/intl.en-US/Resource Types/DRDS/ALIYUN::DRDS::DrdsInstance.md)|
|Elastic Container Instance \(ECI\)|[ALIYUN::ECI::ContainerGroup](/intl.en-US/Resource Types/ECI/ALIYUN::ECI::ContainerGroup.md)|
|ECS|-   [ALIYUN::ECS::DedicatedHost](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::DedicatedHost.md)
-   [ALIYUN::ECS::Disk](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::Disk.md)
-   [ALIYUN::ECS::Instance](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::Instance.md)
-   [ALIYUN::ECS::PrepayInstance](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::PrepayInstance.md) |
|Elastic High Performance Computing \(E-HPC\)|[ALIYUN::EHPC::Cluster](/intl.en-US/Resource Types/EHPC/ALIYUN::EHPC::Cluster.md)|
|Alibaba Cloud Elasticsearch|[ALIYUN::ElasticSearch::Instance](/intl.en-US/Resource Types/Elasticsearch/ALIYUN::ElasticSearch::Instance.md)|
|Alibaba Cloud E-MapReduce \(EMR\)|[ALIYUN::EMR::Cluster](/intl.en-US/Resource Types/EMR/ALIYUN::EMR::Cluster.md)|
|Alibaba Cloud Marketplace|[ALIYUN::MarketPlace::Order](/intl.en-US/Resource Types/MarketPlace/ALIYUN::MarketPlace::Order.md)|
|ApsaraDB for Memcache|[ALIYUN::Memcache::Instance]()|
|ApsaraDB for MongoDB|-   [ALIYUN::MONGODB::Instance](/intl.en-US/Resource Types/MongoDB/ALIYUN::MONGODB::Instance.md)
-   [ALIYUN::MONGODB::ServerlessInstance](/intl.en-US/Resource Types/MongoDB/ALIYUN::MONGODB::ServerlessInstance.md)
-   [ALIYUN::MONGODB::ShardingInstance](/intl.en-US/Resource Types/MongoDB/ALIYUN::MONGODB::ShardingInstance.md) |
|PolarDB|[ALIYUN::POLARDB::DBCluster](/intl.en-US/Resource Types/ApsaraDB for POLARDB/ALIYUN::POLARDB::DBCluster.md)|
|ApsaraDB for Redis|[ALIYUN::REDIS::Instance](/intl.en-US/Resource Types/Redis/ALIYUN::REDIS::Instance.md)|
|ApsaraDB RDS|-   [ALIYUN::RDS::DBInstance](/intl.en-US/Resource Types/RDS/ALIYUN::RDS::DBInstance.md)
-   [ALIYUN::RDS::PrepayDBInstance](/intl.en-US/Resource Types/RDS/ALIYUN::RDS::PrepayDBInstance.md)
-   [ALIYUN::RDS::ReadOnlyDBInstance](/intl.en-US/Resource Types/RDS/ALIYUN::RDS::ReadOnlyDBInstance.md) |
|ROS|[ALIYUN::ROS::Stack](/intl.en-US/Resource Types/ROS/ALIYUN::ROS::Stack.md)|
|Serverless App Engine \(SAE\)|[ALIYUN::SAE::Application](/intl.en-US/Resource Types/SAE/ALIYUN::SAE::Application.md)|
|Server Load Balancer \(SLB\)|[ALIYUN::SLB::LoadBalancer](/intl.en-US/Resource Types/SLB/ALIYUN::SLB::LoadBalancer.md)|
|Virtual Private Cloud \(VPC\)|-   [ALIYUN::VPC::CommonBandwidthPackage](/intl.en-US/Resource Types/VPC/ALIYUN::VPC::CommonBandwidthPackage.md)
-   [ALIYUN::VPC::CustomerGateway](/intl.en-US/Resource Types/VPC/ALIYUN::VPC::CustomerGateway.md)
-   [ALIYUN::VPC::EIP](/intl.en-US/Resource Types/VPC/ALIYUN::VPC::EIP.md)
-   [ALIYUN::VPC::NatGateway](/intl.en-US/Resource Types/VPC/ALIYUN::VPC::NatGateway.md)
-   [ALIYUN::VPC::Ipv6Gateway](/intl.en-US/Resource Types/VPC/ALIYUN::VPC::Ipv6Gateway.md)
-   [ALIYUN::VPC::VpnGateway](/intl.en-US/Resource Types/VPC/ALIYUN::VPC::VpnGateway.md) |


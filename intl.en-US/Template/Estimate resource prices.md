# Estimate resource prices

Some resources used in templates incur charges. You can query the prices of resources in a template by using the ROS console or API operations.

## Methods

You can estimate resource prices by using one of the following methods:

-   ROS console: If the resources of a template used to create a stack support price query, ROS provides the estimated prices in the **Check and Confirm** step of the Use New Resources \(Standard\) or Use Existing Resources \(Resource Import\) wizard. The prices provided are for reference only. The actual prices are subject to changes.
-   API: You can call the [GetTemplateEstimateCost](/intl.en-US/API Reference/Template operations/GetTemplateEstimateCost.md) operation to query the resource prices.

## Supported resource types

|Alibaba Cloud service|Resource type|
|---------------------|-------------|
|Cloud Enterprise Network \(CEN\)|ALIYUN::CEN::CenBandwidthPackage|
|PolarDB-X|ALIYUN::DRDS::DrdsInstance|
|Elastic Container Instance \(ECI\)|ALIYUN::ECI::ContainerGroup|
|Elastic Compute Service \(ECS\)|-   ALIYUN::ECS::DedicatedHost
-   ALIYUN::ECS::Disk
-   ALIYUN::ECS::ImageMarket
-   ALIYUN::ECS::Instance
-   ALIYUN::ECS::PrepayInstance |
|Elastic High Performance Computing \(E-HPC\)|ALIYUN::EHPC::Cluster|
|Elasticsearch|ALIYUN::ElasticSearch::Instance|
|E-MapReduce \(EMR\)|ALIYUN::EMR::Cluster|
|Alibaba Cloud Marketplace|ALIYUN::MarketPlace::Order|
|ApsaraDB for Memcache|ALIYUN::Memcache::Instance|
|ApsaraDB for MongoDB|-   ALIYUN::MONGODB::Instance
-   ALIYUN::MONGODB::PrepayInstance
-   ALIYUN::MONGODB::ServerlessInstance
-   ALIYUN::MONGODB::ShardingInstance |
|PolarDB|ALIYUN::PolarDB::DBCluster|
|ApsaraDB for Redis|ALIYUN::REDIS::Instance|
|ApsaraDB RDS|-   ALIYUN::RDS::DBInstance
-   ALIYUN::RDS::PrepayDBInstance
-   ALIYUN::RDS::ReadOnlyDBInstance |
|Resource Orchestration Service \(ROS\)|-   ALIYUN::ROS::ResourcePackage
-   ALIYUN::ROS::Stack |
|Serverless App Engine \(SAE\)|ALIYUN::SAE::Application|
|Server Load Balancer \(SLB\)|ALIYUN::SLB::LoadBalancer|
|Virtual Private Cloud \(VPC\)|-   ALIYUN::VPC::CommonBandwidthPackage
-   ALIYUN::VPC::CustomerGateway
-   ALIYUN::VPC::EIP
-   ALIYUN::VPC::NatGateway
-   ALIYUN::VPC::Ipv6Gateway
-   ALIYUN::VPC::VpnGateway |


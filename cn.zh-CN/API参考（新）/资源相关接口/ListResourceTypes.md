# ListResourceTypes {#doc_api_ROS_ListResourceTypes .reference}

查询支持的资源类型列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ROS&api=ListResourceTypes&type=RPC&version=2019-09-10)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListResourceTypes|系统规定参数。取值：ListResourceTypes。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B288A0BE-D927-4888-B0F7-B35EF84B6E6|请求ID。

 |
|ResourceTypes| |\{"ResourceTypes":\["ALIYUN::ECS::Instance","ALIYUN::RDS::Instance"\]\}|资源类型数组。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ros.aliyuncs.com/?Action=ListResourceTypes
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListResourceTypesResponse>
       <RequestId type="string">B288A0BE-D927-4888-B0F7-B35EF84B6E6F</RequestId>
       <ResourceTypes class="array">
              <ResourceType type="string">ALIYUN::ACTIONTRAIL::Trail</ResourceType>
              <ResourceType type="string">ALIYUN::ACTIONTRAIL::TrailLogging</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::Api</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::App</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::Authorization</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::CustomDomain</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::Deployment</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::Group</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::Signature</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::SignatureBinding</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::StageConfig</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::TrafficControl</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::TrafficControlBinding</ResourceType>
              <ResourceType type="string">ALIYUN::ApiGateway::VpcAccessConfig</ResourceType>
              <ResourceType type="string">ALIYUN::BSS::WaitOrder</ResourceType>
              <ResourceType type="string">ALIYUN::CDN::Domain</ResourceType>
              <ResourceType type="string">ALIYUN::CDN::DomainConfig</ResourceType>
              <ResourceType type="string">ALIYUN::CEN::CenBandwidthLimit</ResourceType>
              <ResourceType type="string">ALIYUN::CEN::CenBandwidthPackage</ResourceType>
              <ResourceType type="string">ALIYUN::CEN::CenBandwidthPackageAssociation</ResourceType>
              <ResourceType type="string">ALIYUN::CEN::CenInstance</ResourceType>
              <ResourceType type="string">ALIYUN::CEN::CenInstanceAttachment</ResourceType>
              <ResourceType type="string">ALIYUN::CEN::RouteEntry</ResourceType>
              <ResourceType type="string">ALIYUN::CS::App</ResourceType>
              <ResourceType type="string">ALIYUN::CS::Cluster</ResourceType>
              <ResourceType type="string">ALIYUN::DEBUG::Apple</ResourceType>
              <ResourceType type="string">ALIYUN::DEBUG::Dummy</ResourceType>
              <ResourceType type="string">ALIYUN::DEBUG::Failure</ResourceType>
              <ResourceType type="string">ALIYUN::DEBUG::Secret</ResourceType>
              <ResourceType type="string">ALIYUN::DEBUG::Update</ResourceType>
              <ResourceType type="string">ALIYUN::DNS::Domain</ResourceType>
              <ResourceType type="string">ALIYUN::DNS::DomainGroup</ResourceType>
              <ResourceType type="string">ALIYUN::DNS::DomainRecord</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::AutoSnapshotPolicy</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::BandwidthPackage</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::Command</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::CopyImage</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::CustomImage</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::DedicatedHost</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::DeploymentSet</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::Disk</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::DiskAttachment</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::ForwardEntry</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::Instance</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::InstanceClone</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::InstanceGroup</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::InstanceGroupClone</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::Invocation</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::JoinSecurityGroup</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::LaunchTemplate</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::NatGateway</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::NetworkInterface</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::NetworkInterfaceAttachment</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::NetworkInterfacePermission</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::PrepayInstance</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::PrepayInstanceGroupClone</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::Route</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SNatEntry</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SSHKeyPair</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SSHKeyPairAttachment</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SecurityGroup</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SecurityGroupClone</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SecurityGroupEgress</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::SecurityGroupIngress</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::Snapshot</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::VPC</ResourceType>
              <ResourceType type="string">ALIYUN::ECS::VSwitch</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::AlarmTask</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::AlarmTaskEnable</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::LifecycleHook</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::ScalingConfiguration</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::ScalingGroup</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::ScalingGroupEnable</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::ScalingRule</ResourceType>
              <ResourceType type="string">ALIYUN::ESS::ScheduledTask</ResourceType>
              <ResourceType type="string">ALIYUN::FC::Function</ResourceType>
              <ResourceType type="string">ALIYUN::FC::FunctionInvoker</ResourceType>
              <ResourceType type="string">ALIYUN::FC::Service</ResourceType>
              <ResourceType type="string">ALIYUN::FC::Trigger</ResourceType>
              <ResourceType type="string">ALIYUN::KMS::Alias</ResourceType>
              <ResourceType type="string">ALIYUN::KMS::Key</ResourceType>
              <ResourceType type="string">ALIYUN::MEMCACHE::Instance</ResourceType>
              <ResourceType type="string">ALIYUN::MNS::Queue</ResourceType>
              <ResourceType type="string">ALIYUN::MNS::Subscription</ResourceType>
              <ResourceType type="string">ALIYUN::MNS::Topic</ResourceType>
              <ResourceType type="string">ALIYUN::MONGODB::Instance</ResourceType>
              <ResourceType type="string">ALIYUN::MONGODB::PrepayInstance</ResourceType>
              <ResourceType type="string">ALIYUN::MarketPlace::Image</ResourceType>
              <ResourceType type="string">ALIYUN::MarketPlace::Order</ResourceType>
              <ResourceType type="string">ALIYUN::NAS::AccessGroup</ResourceType>
              <ResourceType type="string">ALIYUN::NAS::AccessRule</ResourceType>
              <ResourceType type="string">ALIYUN::NAS::FileSystem</ResourceType>
              <ResourceType type="string">ALIYUN::NAS::MountTarget</ResourceType>
              <ResourceType type="string">ALIYUN::OSS::Bucket</ResourceType>
              <ResourceType type="string">ALIYUN::OTS::Instance</ResourceType>
              <ResourceType type="string">ALIYUN::OTS::VpcBinder</ResourceType>
              <ResourceType type="string">ALIYUN::PVTZ::Zone</ResourceType>
              <ResourceType type="string">ALIYUN::PVTZ::ZoneRecord</ResourceType>
              <ResourceType type="string">ALIYUN::PVTZ::ZoneVpcBinder</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::AccessKey</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::AttachPolicyToRole</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::Group</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::ManagedPolicy</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::Role</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::User</ResourceType>
              <ResourceType type="string">ALIYUN::RAM::UserToGroupAddition</ResourceType>
              <ResourceType type="string">ALIYUN::RDS::Account</ResourceType>
              <ResourceType type="string">ALIYUN::RDS::AccountPrivilege</ResourceType>
              <ResourceType type="string">ALIYUN::RDS::DBInstance</ResourceType>
              <ResourceType type="string">ALIYUN::RDS::DBInstanceParameterGroup</ResourceType>
              <ResourceType type="string">ALIYUN::RDS::DBInstanceSecurityIps</ResourceType>
              <ResourceType type="string">ALIYUN::RDS::PrepayDBInstance</ResourceType>
              <ResourceType type="string">ALIYUN::REDIS::Instance</ResourceType>
              <ResourceType type="string">ALIYUN::REDIS::PrepayInstance</ResourceType>
              <ResourceType type="string">ALIYUN::ROS::Stack</ResourceType>
              <ResourceType type="string">ALIYUN::ROS::WaitCondition</ResourceType>
              <ResourceType type="string">ALIYUN::ROS::WaitConditionHandle</ResourceType>
              <ResourceType type="string">ALIYUN::SAG::ACL</ResourceType>
              <ResourceType type="string">ALIYUN::SAG::ACLAssociation</ResourceType>
              <ResourceType type="string">ALIYUN::SAG::ACLRule</ResourceType>
              <ResourceType type="string">ALIYUN::SAG::CloudConnectNetwork</ResourceType>
              <ResourceType type="string">ALIYUN::SAG::SmartAccessGatewayBinding</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::AccessControl</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::BackendServerAttachment</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::BackendServerToVServerGroupAddition</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::Certificate</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::DomainExtension</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::Listener</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::LoadBalancer</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::LoadBalancerClone</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::MasterSlaveServerGroup</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::Rule</ResourceType>
              <ResourceType type="string">ALIYUN::SLB::VServerGroup</ResourceType>
              <ResourceType type="string">ALIYUN::SLS::ApplyConfigToMachineGroup</ResourceType>
              <ResourceType type="string">ALIYUN::SLS::MachineGroup</ResourceType>
              <ResourceType type="string">ALIYUN::UIS::Uis</ResourceType>
              <ResourceType type="string">ALIYUN::UIS::UisConnection</ResourceType>
              <ResourceType type="string">ALIYUN::UIS::UisNode</ResourceType>
              <ResourceType type="string">ALIYUN::VPC::EIP</ResourceType>
              <ResourceType type="string">ALIYUN::VPC::EIPAssociation</ResourceType>
              <ResourceType type="string">ALIYUN::VPC::PeeringRouterInterfaceBinding</ResourceType>
              <ResourceType type="string">ALIYUN::VPC::PeeringRouterInterfaceConnection</ResourceType>
              <ResourceType type="string">ALIYUN::VPC::RouterInterface</ResourceType>
              <ResourceType type="string">ALIYUN::VPC::SnatEntry</ResourceType>
       </ResourceTypes>
</ListResourceTypesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B288A0BE-D927-4888-B0F7-B35EF84B6E6F",
	"ResourceTypes":[
		"ALIYUN::ACTIONTRAIL::Trail",
		"ALIYUN::ACTIONTRAIL::TrailLogging",
		"ALIYUN::ApiGateway::Api",
		"ALIYUN::ApiGateway::App",
		"ALIYUN::ApiGateway::Authorization",
		"ALIYUN::ApiGateway::CustomDomain",
		"ALIYUN::ApiGateway::Deployment",
		"ALIYUN::ApiGateway::Group",
		"ALIYUN::ApiGateway::Signature",
		"ALIYUN::ApiGateway::SignatureBinding",
		"ALIYUN::ApiGateway::StageConfig",
		"ALIYUN::ApiGateway::TrafficControl",
		"ALIYUN::ApiGateway::TrafficControlBinding",
		"ALIYUN::ApiGateway::VpcAccessConfig",
		"ALIYUN::BSS::WaitOrder",
		"ALIYUN::CDN::Domain",
		"ALIYUN::CDN::DomainConfig",
		"ALIYUN::CEN::CenBandwidthLimit",
		"ALIYUN::CEN::CenBandwidthPackage",
		"ALIYUN::CEN::CenBandwidthPackageAssociation",
		"ALIYUN::CEN::CenInstance",
		"ALIYUN::CEN::CenInstanceAttachment",
		"ALIYUN::CEN::RouteEntry",
		"ALIYUN::CS::App",
		"ALIYUN::CS::Cluster",
		"ALIYUN::DEBUG::Apple",
		"ALIYUN::DEBUG::Dummy",
		"ALIYUN::DEBUG::Failure",
		"ALIYUN::DEBUG::Secret",
		"ALIYUN::DEBUG::Update",
		"ALIYUN::DNS::Domain",
		"ALIYUN::DNS::DomainGroup",
		"ALIYUN::DNS::DomainRecord",
		"ALIYUN::ECS::AutoSnapshotPolicy",
		"ALIYUN::ECS::BandwidthPackage",
		"ALIYUN::ECS::Command",
		"ALIYUN::ECS::CopyImage",
		"ALIYUN::ECS::CustomImage",
		"ALIYUN::ECS::DedicatedHost",
		"ALIYUN::ECS::DeploymentSet",
		"ALIYUN::ECS::Disk",
		"ALIYUN::ECS::DiskAttachment",
		"ALIYUN::ECS::ForwardEntry",
		"ALIYUN::ECS::Instance",
		"ALIYUN::ECS::InstanceClone",
		"ALIYUN::ECS::InstanceGroup",
		"ALIYUN::ECS::InstanceGroupClone",
		"ALIYUN::ECS::Invocation",
		"ALIYUN::ECS::JoinSecurityGroup",
		"ALIYUN::ECS::LaunchTemplate",
		"ALIYUN::ECS::NatGateway",
		"ALIYUN::ECS::NetworkInterface",
		"ALIYUN::ECS::NetworkInterfaceAttachment",
		"ALIYUN::ECS::NetworkInterfacePermission",
		"ALIYUN::ECS::PrepayInstance",
		"ALIYUN::ECS::PrepayInstanceGroupClone",
		"ALIYUN::ECS::Route",
		"ALIYUN::ECS::SNatEntry",
		"ALIYUN::ECS::SSHKeyPair",
		"ALIYUN::ECS::SSHKeyPairAttachment",
		"ALIYUN::ECS::SecurityGroup",
		"ALIYUN::ECS::SecurityGroupClone",
		"ALIYUN::ECS::SecurityGroupEgress",
		"ALIYUN::ECS::SecurityGroupIngress",
		"ALIYUN::ECS::Snapshot",
		"ALIYUN::ECS::VPC",
		"ALIYUN::ECS::VSwitch",
		"ALIYUN::ESS::AlarmTask",
		"ALIYUN::ESS::AlarmTaskEnable",
		"ALIYUN::ESS::LifecycleHook",
		"ALIYUN::ESS::ScalingConfiguration",
		"ALIYUN::ESS::ScalingGroup",
		"ALIYUN::ESS::ScalingGroupEnable",
		"ALIYUN::ESS::ScalingRule",
		"ALIYUN::ESS::ScheduledTask",
		"ALIYUN::FC::Function",
		"ALIYUN::FC::FunctionInvoker",
		"ALIYUN::FC::Service",
		"ALIYUN::FC::Trigger",
		"ALIYUN::KMS::Alias",
		"ALIYUN::KMS::Key",
		"ALIYUN::MEMCACHE::Instance",
		"ALIYUN::MNS::Queue",
		"ALIYUN::MNS::Subscription",
		"ALIYUN::MNS::Topic",
		"ALIYUN::MONGODB::Instance",
		"ALIYUN::MONGODB::PrepayInstance",
		"ALIYUN::MarketPlace::Image",
		"ALIYUN::MarketPlace::Order",
		"ALIYUN::NAS::AccessGroup",
		"ALIYUN::NAS::AccessRule",
		"ALIYUN::NAS::FileSystem",
		"ALIYUN::NAS::MountTarget",
		"ALIYUN::OSS::Bucket",
		"ALIYUN::OTS::Instance",
		"ALIYUN::OTS::VpcBinder",
		"ALIYUN::PVTZ::Zone",
		"ALIYUN::PVTZ::ZoneRecord",
		"ALIYUN::PVTZ::ZoneVpcBinder",
		"ALIYUN::RAM::AccessKey",
		"ALIYUN::RAM::AttachPolicyToRole",
		"ALIYUN::RAM::Group",
		"ALIYUN::RAM::ManagedPolicy",
		"ALIYUN::RAM::Role",
		"ALIYUN::RAM::User",
		"ALIYUN::RAM::UserToGroupAddition",
		"ALIYUN::RDS::Account",
		"ALIYUN::RDS::AccountPrivilege",
		"ALIYUN::RDS::DBInstance",
		"ALIYUN::RDS::DBInstanceParameterGroup",
		"ALIYUN::RDS::DBInstanceSecurityIps",
		"ALIYUN::RDS::PrepayDBInstance",
		"ALIYUN::REDIS::Instance",
		"ALIYUN::REDIS::PrepayInstance",
		"ALIYUN::ROS::Stack",
		"ALIYUN::ROS::WaitCondition",
		"ALIYUN::ROS::WaitConditionHandle",
		"ALIYUN::SAG::ACL",
		"ALIYUN::SAG::ACLAssociation",
		"ALIYUN::SAG::ACLRule",
		"ALIYUN::SAG::CloudConnectNetwork",
		"ALIYUN::SAG::SmartAccessGatewayBinding",
		"ALIYUN::SLB::AccessControl",
		"ALIYUN::SLB::BackendServerAttachment",
		"ALIYUN::SLB::BackendServerToVServerGroupAddition",
		"ALIYUN::SLB::Certificate",
		"ALIYUN::SLB::DomainExtension",
		"ALIYUN::SLB::Listener",
		"ALIYUN::SLB::LoadBalancer",
		"ALIYUN::SLB::LoadBalancerClone",
		"ALIYUN::SLB::MasterSlaveServerGroup",
		"ALIYUN::SLB::Rule",
		"ALIYUN::SLB::VServerGroup",
		"ALIYUN::SLS::ApplyConfigToMachineGroup",
		"ALIYUN::SLS::MachineGroup",
		"ALIYUN::UIS::Uis",
		"ALIYUN::UIS::UisConnection",
		"ALIYUN::UIS::UisNode",
		"ALIYUN::VPC::EIP",
		"ALIYUN::VPC::EIPAssociation",
		"ALIYUN::VPC::PeeringRouterInterfaceBinding",
		"ALIYUN::VPC::PeeringRouterInterfaceConnection",
		"ALIYUN::VPC::RouterInterface",
		"ALIYUN::VPC::SnatEntry"
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ROS)查看更多错误码。

访问[公共错误码](~~131033~~)查看更多错误码。


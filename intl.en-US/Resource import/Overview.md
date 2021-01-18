# Overview

You can import existing resources to Resource Orchestration Service \(ROS\) for centralized resource management and orchestration.

## Resource types that support resource import

For information about resource types that support resource import, see [Resource types that support drift detection and resource import](/intl.en-US/Drift detection/Resource types that support drift detection and resource import.md).

## Methods

The following table describes the methods that you can use to import resources to ROS.

|Method|Description|
|------|-----------|
|[t2005814.md\#]()|If you want to import resources to a new stack, you can use this method to create a stack that contains the imported resources.|
|[t2005872.md\#]()|If you want to import resources to an existing stack, you can use this method to import the resources to the stack.|

## Usage notes

When you import a resource, take note of the following items:

-   You must make sure that the template content is correct.
    -   The template must contain both the resources that are already part of the stack and the resources that you want to import. Before you import resources, you must create the resources. To prevent the resources that you want to import from being unexpectedly deleted, set `DeletionPolicy` to `Retain`.
    -   The resource type must support the properties and values of the resources that you want to import.
    -   The required properties for each resource type must be specified in the template.
-   You must obtain the resource identifier property and its value. For information about how to obtain resource identifier properties, see [t2005481.md\#]().
-   After resources are imported, we recommend that you perform drift detection on the resources. This way, you can make sure that the template configuration matches the actual configuration. For more information, see [Detect drift on a stack](/intl.en-US/Drift detection/Detect drift on a stack.md).
-   You must import resources within ROS limits. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).
-   You cannot import the same resource of a following resource type to multiple stacks.

    |Alibaba Cloud service|Resource type|
    |---------------------|-------------|
    |API Gateway|    -   ALIYUN::ApiGateway::Api
    -   ALIYUN::ApiGateway::App
    -   ALIYUN::ApiGateway::Group |
    |Alibaba Cloud DNS \(DNS\)|ALIYUN::DNS::DomainRecord|
    |Elastic Compute Service \(ECS\)|    -   ALIYUN::ECS::Snapshot
    -   ALIYUN::ECS::VPC
    -   ALIYUN::ECS::VSwitch |
    |Auto Scaling|    -   ALIYUN::ESS::ScalingConfiguration
    -   ALIYUN::ESS::ScalingRule |
    |Function Compute|    -   ALIYUN::FC::CustomDomain
    -   ALIYUN::FC::Function
    -   ALIYUN::FC::Service
    -   ALIYUN::FC::Trigger |
    |ApsaraDB for MongoDB|ALIYUN::MONGODB::Instance|
    |Apsara File Storage NAS \(NAS\)|ALIYUN::NAS::FileSystem|
    |ApsaraDB RDS|ALIYUN::RDS::DBInstance|
    |ApsaraDB for Redis|ALIYUN::REDIS::Instance|
    |Server Load Balancer \(SLB\)|ALIYUN::SLB::MasterSlaveServerGroup|
    |Log Service|ALIYUN::SLS::Project|
    |Virtual Private Cloud \(VPC\)|    -   ALIYUN::VPC::NatGateway
    -   ALIYUN::VPC::SnatEntry |


## Status codes

The following table lists the status codes for resource import.

-   Stack status codes

    |Status code|Description|
    |-----------|-----------|
    |IMPORT\_CREATE\_IN\_PROGRESS|A stack is being created by importing resources.|
    |IMPORT\_CREATE\_FAILED|A stack failed to be created by importing resources.|
    |IMPORT\_CREATE\_COMPLETE|A stack is created by importing resources.|
    |IMPORT\_CREATE\_ROLLBACK\_IN\_PROGRESS|A stack failed to be created by importing resources. A rollback is being performed.|
    |IMPORT\_CREATE\_ROLLBACK\_FAILED|A stack failed to be created by importing resources. A rollback failed to be performed.|
    |IMPORT\_CREATE\_ROLLBACK\_COMPLETE|A stack failed to be created by importing resources. A rollback is performed.|
    |IMPORT\_UPDATE\_IN\_PROGRESS|The stack is being updated by importing resources.|
    |IMPORT\_UPDATE\_FAILED|The stack failed to be updated by importing resources.|
    |IMPORT\_UPDATE\_COMPLETE|The stack is updated by importing resources.|
    |IMPORT\_UPDATE\_ROLLBACK\_IN\_PROGRESS|The stack failed to be updated by importing resources. A rollback is being performed.|
    |IMPORT\_UPDATE\_ROLLBACK\_FAILED|The stack failed to be updated by importing resources. A rollback failed to be performed.|
    |IMPORT\_UPDATE\_ROLLBACK\_COMPLETE|The stack failed to be updated by importing resources. A rollback is performed.|

-   Resource status codes

    |Status code|Description|
    |-----------|-----------|
    |IMPORT\_IN\_PROGRESS|The resource is being imported.|
    |IMPORT\_FAILED|The resource failed to be imported.|
    |IMPORT\_COMPLETE|The resource is imported.|



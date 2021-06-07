# What is ROS?

Resource Orchestration Service \(ROS\) is a service provided by Alibaba Cloud to simplify the management of cloud computing resources. You can author stack templates based on the template specifications defined in ROS. Within a template, you can define required cloud computing resources such as Elastic Compute Service \(ECS\) and ApsaraDB RDS instances, and the dependencies between resources. The ROS engine automatically creates and configures all resources in a stack based on a template, which makes automatic deployment and O&M possible.

The following figure shows the implementation principle of ROS.

![description](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2599398951/p96410.png)

ROS provides the following features:

-   Free service hosting: ROS provides a managed and serverless O&M service that enables the automatic execution of O&M tasks. You can define Alibaba Cloud resources and configure parameters, describe the dependencies between resources, and then create a stack to manage a group of resources.
-   Resource deployment across accounts and regions: You can use a single ROS template to implement automatic deployment in multiple Alibaba Cloud accounts across regions. You can also use a single ROS template to deploy development, testing, and production environments. Different requirements of the environments are met based on the parameters specified in the template. For example, you can use the same template to deploy 2 ECS instances in the testing environment and 20 ECS instances in the production environment.
-   Standardized deployment: ROS allows you to implement repeated deployment and save deployment costs by standardizing deployment environments, minimizing differences between environments, and building environment configurations into templates.
-   Visual presentation of results: You can use the ROS console or API operations to view the deployment status of all resources that are deployed by using ROS. This eliminates the need to manually check the deployment process.
-   Drift detection: You can use the drift detection feature to identify the configuration changes in your resources that are beyond the control of ROS. You can then take corrective measures to resynchronize resources with their template definitions.
-   Service integration: ROS is integrated with Resource Access Management \(RAM\) to provide unified authentication. This eliminates the need to establish a separate user authentication system. ROS is also integrated with ActionTrail to allow you to review all O&M operations on Alibaba Cloud services, including operations on ROS.


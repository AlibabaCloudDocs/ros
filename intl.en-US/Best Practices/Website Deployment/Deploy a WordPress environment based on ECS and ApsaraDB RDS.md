# Deploy a WordPress environment based on ECS and ApsaraDB RDS

This topic describes how to use a sample template in Resource Orchestration Service \(ROS\) to deploy a WordPress environment based on Elastic Compute Service \(ECS\) and ApsaraDB RDS.

WordPress is a blog platform that is developed in the PHP programming language and paired with a MySQL database. You can use a [sample template](https://rosnext.console.aliyun.com/cn-beijing/samples/Wordpress_Instance) to deploy a WordPress environment based on ECS and ApsaraDB RDS. The ECS and ApsaraDB RDS instances are created on the CentOS 7 operating system.

## Create a stack

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, choose **Templates** \> **Sample Templates**.

3.  Find the **Create a WordPress Environment Based on ECS and ApsaraDB for RDS** template.

4.  Click **Create Stack**.

5.  In the Configure Template Parameters step of the Use New Resources \(Standard\) wizard, set **Stack Name** and the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |VPC CIDR Block|The CIDR block of the virtual private cloud \(VPC\).|
    |VSwitch Availability Zone|The zone ID of the vSwitch.|
    |VSwitch CIDR Block|The CIDR block of the vSwitch, which must be within the range of the CIDR block of the VPC.|
    |Instance Type|The instance type of the ECS instance.|
    |Image|The ID of the image. The default value is centos\_7.|
    |Instance Password|The password that is used to log on to the ECS instance.|
    |DB Instance Class|The instance type of the ApsaraDB RDS instance.|
    |Engine|The database engine and engine version.|
    |DB Instance Storage|The storage capacity of the ApsaraDB RDS instance.|
    |DB Name|The name of the ApsaraDB RDS for MySQL database.|
    |DB Username|The username that is used to log on to the ApsaraDB RDS for MySQL database.|
    |DB Password|The password that is used to log on to the ApsaraDB RDS for MySQL database.|

6.  Click **Create**.

7.  View the stack status on the **Stack Information** tab of the stack management page. After the stack is created, click the **Outputs** tab and obtain the WordPress URL on the tab.

8.  Open the URL and log on to the WordPress console.


## View resources

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  On the Stacks page, click the stack that you created.

4.  On the stack management page, click the **Resources** tab to view the resource list.

    The following table describes the resource information in this example.

    |Resource type|Quantity|Description|Specifications|
    |-------------|--------|-----------|--------------|
    |ALIYUN::ECS::Instance|1|Creates an ECS instance to deploy the WordPress service.|A single instance of the following specifications is created:    -   InstanceType: ecs.c5.large
    -   SystemDiskCategory: cloud\_efficiency
    -   SystemDiskSize: 40
    -   AllocatePublicIP: true |
    |ALIYUN::ECS::VPC|1|Creates a VPC to ensure network security.|None|
    |ALIYUN::ECS::VSwitch|1|Creates a vSwitch in the VPC to manage instances within a zone.|None|
    |ALIYUN::RDS::DBInstance|1|Creates an ApsaraDB RDS for MySQL instance to store data of the WordPress service.|The cost depends on the instance type and storage capacity.     -   DBInstanceStorage: 5
    -   DBInstanceClass: rds.mysql.t1.small \(1 core, 1 GB memory\) |



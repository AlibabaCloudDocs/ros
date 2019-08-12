# What is ROS? {#concept_28852_zh .concept}

Alibaba Cloud Resource Orchestration Service \(ROS\) is a service that helps you simplify the cloud computing resource management and automate O&M. After compiling a resource stack template, define what cloud resources you need, the dependency between the resources, and the resource configurations. With the orchestration engine, ROS can automatically create and configure all resources for automatic deployment, operation, and maintenance according to your template. An orchestration template is a text file in JSON format that you can read and edit at any time. You can compile your template in JSON directly, or you can use **Visual Editor** in the ROS console to compile the template more visually. You can control the template version with tools such as SVN or Git. You can also enable IAC \(Infrastructure as Code\) using API, SDK, and other methods to integrate the orchestration capabilities of ROS into your own applications.

The resource orchestration template also provides a standard delivery method for resources and applications. You can use the template to deliver integrated systems and solutions that include cloud resources and applications. Independent software vendors \(ISV\) can use such delivery method to easily integrate Alibaba Cloud resources with their own software systems for consistent delivery.

ROS manages cloud resources in groups. A group of resources is a resource stack. Therefore, cloud resources can be created, deleted, modified, and cloned in groups. In DevOps practices, you can easily clone, develop, and test the environments, simplifying the overall migration and scaling of applications.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23163/156264357144675_en-US.png)


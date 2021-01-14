# How do I specify images for ECS resources?

This topic describes how to use Resource Orchestration Service \(ROS\) to specify images for ECS resources.

An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [Alibaba Cloud official website](https://account.alibabacloud.com/register/intl_register.htm).

If you use one of the following resource types to create ECS instances, you must specify images for the instances.

-   [ALIYUN::ECS::Instance](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::Instance.md)
-   [ALIYUN::ECS::InstanceClone](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::InstanceClone.md)
-   [ALIYUN::ECS::InstanceGroup](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::InstanceGroup.md)
-   [ALIYUN::ECS::InstanceGroupClone](/intl.en-US/Resource Types/ECS/ALIYUN::ECS::InstanceGroupClone.md)

You can use one of the following methods to set the ImageId parameter in a stack template:

-   Specify an image ID.
-   Specify an image by fuzzy match.
-   Select an image by using the AssociationProperty parameter.

## Specify an image ID

If you have the ID of the image that you want to use, specify the ImageId parameter in the template.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  Click the **Public Image** tab.

    Find the target image ID on the Public Image tab and record it for later use.

4.  In the ROS template, set the ImageId parameter to the image ID.

    For more information about template creation, see [Create a template](/intl.en-US/Template/Template management/Create a template.md).

    ```
    "ImageId": { "Type": "String", "Description": "Image Id, represents the image resource to startup one ECS instance", "Default": "centos_7_04_64_20G_alibase_201701015.vhd" },
    ```


## Specify an image by fuzzy match

If you do not need specific versions of CentOS or Ubuntu images, you can use fuzzy match to specify an image ID. ROS uses the value you enter to find the best match.

ROS uses the following rules to find a match:

-   If you specify only the operating system of images, such as CentOS, Windows, or Ubuntu, ROS matches the latest 64-bit image version.
-   If you specify a major version of an operating system, ROS matches the latest 64-bit version of the system based on the major version. For example, if you enter CentOS\_6, ROS matches the latest 64-bit version of CentOS 6. If you enter Ubutun\_14, ROS matches the latest 64-bit version of Ubutun\_14. If you enter Win2008r2, ROS matches the latest 64-bit version of Windows Server 2008 R2.
-   If you use an asterisk \(\*\) to replace a part of the image ID, such as `centos_6_09_64_20G_alibase*.vhd`, ROS matches the latest centos\_6\_09\_64\_20G\_alibase public image version. Fuzzy match is used in the sample templates. In many cases, the image ID is set to CentOS\_7 or Ubuntu\_14.

Examples

```
"ImageId": {
   "Type": "String",
   "Description": "ECS Image",
   "Label": "ECS Image",
   "Default": "cent****"
 },
```

## Select an image by using the AssociationProperty parameter

Include AssociationProperty as part of your image ID definition when you declare it as a parameter in the Parameters section. Then, ROS lists the images within a region that you can select when you create the ECS instance.

AssociationProperty is used in the following example:

```
   "ImageId": {
      "AssociationProperty":"ALIYUN::ECS::Instance:ImageId",
      "Type" : "String",
      "Default": "centos_7_04_64_20G_alibase_20170****.vhd",
      "Description": "IDs of available images"
    }            
```

In addition to the available image IDs, ROS displays the default image ID, or indicates whether the values specified by AllowedValues are available. Select the appropriate image ID to create ECS instances.


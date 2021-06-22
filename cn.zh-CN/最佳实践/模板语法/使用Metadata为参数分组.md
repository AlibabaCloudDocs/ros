# 使用Metadata为参数分组

当您使用资源编排服务ROS（Resource Orchestration Service）创建资源栈管理多种资源时，需分别配置多种资源对应的参数，这些参数在配置时可能相互干扰。此时您可以使用元数据（Metadata）为不同资源的参数分组，以便在控制台集中配置参数。

## 背景信息

Metadata用于对Parameters中定义的参数进行分组，并且可以为每一组分别定义标签。本文以Harbor集群版解决方案为例，为您介绍如何使用Metadata为不同资源的参数进行分组。关于Harbor集群版解决方案的更多信息，请参见[Harbor集群版解决方案](https://rosnext.console.aliyun.com/cn-beijing/solutions/Existing_Vpc_Docker_Cluster_Harbor?isSolution=true&accounttraceid=a965b1f0d0cb4d5cad371a67f91a789fnuzn)。

Harbor集群中共分为以下5类配置：

-   基础资源配置
-   Harbor配置
-   DB配置
-   Redis配置
-   SLB配置

您可以将不同的配置参数加入对应分组的Parameters中，实现参数分组。Metadata代码段如下：

```
{
  "Metadata": {
    "ALIYUN::ROS::Interface": {
      "ParameterGroups": [
        {
          "Parameters": [
            "VSwitchZoneId",
            "VPC",
            "VSwitch",
            "SecurityGroup"
          ],
          "Label": {
            "default": {
              "zh-cn": "基础资源配置（必填）",
              "en": "Infrastructure Configuration"
            }
          }
        },
        {
          "Parameters": [
            "ClusterAmount",
            "InstanceType",
            "SystemDiskCategory",
            "SystemDiskSize",
            "Password",
            "HarborAdminPassword"
          ],
          "Label": {
            "default": {
              "zh-cn": "Harbor配置",
              "en": "Harbor Configuration"
            }
          }
        },
        {
          "Parameters": [
            "DBInstanceEngineAndVersion",
            "DBInstanceClass",
            "DBInstanceStorage",
            "DBUser",
            "DBPassword"
          ],
          "Label": {
            "default": {
              "zh-cn": "DB配置",
              "en": "DB Configuration"
            }
          }
        },
        {
          "Parameters": [
            "RedisInstanceClass",
            "EvictionPolicy",
            "RedisPassword"
          ],
          "Label": {
            "default": {
              "zh-cn": "Redis配置",
              "en": "Redis Configuration"
            }
          }
        },
        {
          "Parameters": [
            "LoadBalancerSpec",
            "Bandwidth"
          ],
          "Label": {
            "default": {
              "zh-cn": "SLB配置",
              "en": "SLB Configuration"
            }
          }
        }
      ],
      "TemplateTags": [
        "Creates one ECS(Harbor) instance - Existing Vpc"
      ]
    }
  }
}
```

## 操作步骤

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏，单击**解决方案中心**。

3.  查找模板**Harbor 集群版- 已有专有网络VPC**。

4.  单击右上角的**创建资源栈**。

5.  在配置模板参数页面，输入**资源栈名称**，完成**基础资源配置**、**Harbor配置**、**DB配置**、**Redis配置**和**SLB配置**。

6.  单击**创建**。



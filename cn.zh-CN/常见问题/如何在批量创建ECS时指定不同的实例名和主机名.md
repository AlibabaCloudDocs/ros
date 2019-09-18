# 如何在批量创建ECS时指定不同的实例名和主机名 {#concept_66939_zh .concept}

资源类型ALIYUN::ECS::InstanceGroup可用于批量创建ECS实例。

创建ECS实例时，您可以通过InstanceName和HostName属性指定实例名称和主机名称。在资源编排服务（ROS）中，您可以通过以下方式为每个ECS实例设置不同的实例名称和主机名称：name\_prefix\[begin\_number,bits\]name\_suffix。

实例名称或者主机名由三部分组成：

-   name\_pefix：指定实例名或者主机名的前缀。此项为必填项。
-   \[begin\_number,bits\]：每一个实例名和主机名变化的地方。begin\_number指定实例名和主机名从某个数字开始。bits表示每一个数字占多少位。

    这个字段必须满足以下要求才能被正确解析：

    -   整个字段中不能有空格。
    -   bits取值范围为\[1, 4\]。
    -   begin\_number取值范围为\[0, 9999\]。
    bits取值规则：

    -   如果只指定begin\_number，则bits会默认取值4。
    -   如果只指定\[\]或者\[,\]，则begin\_number从0开始取值，bits会默认取值4。
    -   如果指定的begin\_number位数大于bits所指定的位数，例如\[1234,1\]，begin\_number的值（1234）属于\[0，9999\]的范围，则bits实际会取值为4。
-   name\_suffix：指定实例名或主机名的后缀。此项为可选项。

示例

``` {#codeblock_89m_m13_snl}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "ImageId" : "CentOs*",
        "InstanceType": "ecs.n4.large",
        "Password": "Test1234",
        "MinAmount": 2,
        "MaxAmount": 2,
        "SecurityGroupId": "sg-2zedcm7ep5quses05fs4",
        "SystemDiskCategory": "cloud_efficiency",
        "IoOptimized": "optimized",
        "InstanceName": "my.test-[1114]",
        "HostName": "host[]"
      }
    }
  }
}
		
```

根据上面的模板，ROS会批量创建两个ECS实例。

-   两个ECS的实例名分别是：my.test-1114和my.test-1115。
-   两个ECS的主机名分别是：host0000和host0001。

**说明：** 即使是通过上面的方式指定实例名称和主机名称，最终解析出来的名字必须符合InstanceName和HostName的定义规则。如果不符合规则，则模板会验证失败。


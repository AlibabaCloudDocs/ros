# 如何在批量创建ECS时指定不同的实例名和主机名 {#concept_66939_zh .concept}

资源类型: [ALIYUN::ECS::InstanceGroup](../../../../intl.zh-CN/资源类型/ECS/ALIYUN::ECS::InstanceGroup.md#) 可以用于批量创建 ECS 实例。

创建 ECS 实例的时候，可以通过 InstanceName 和 HostName 属性指定实例名称和主机名称。在资源编排服务中，可以通过以下方式来给每个 ECS 实例设置不同的实例名称和主机名称：name\_prefix\[begin\_number,bits\]name\_suffix

如上所示，实例名称或者主机名由三部分组成：

-   name\_pefix：指定实例名或者主机名的前缀。这一部分是必需的。
-   \[begin\_number,bits\]：每一个实例名和主机名变化的地方。begin\_number 指定实例名和主机名从某个数字开始；bits 表示每一个数字占多少位。

    这个字段必须满足下面的要求才能被正确解析：

    -   整个字段中不能有空格。
    -   bits 取值范围为 \[1, 4\]。
    -   begin\_number 取值范围为 \[0, 9999\]。
    bits 取值规则：

    -   如果只指定 begin\_number，则 bits 会默认取值 4。
    -   如果只指定 \[\] 或者 \[,\]，则 begin\_number 从 0 开始取值，bits 会默认取值 4。
    -   如果指定的 begin\_number 位数大于 bits 所指定的位数，如 \[1234,1\]，begin\_number 的值（1234）属于 \[0，9999\] 的范围，则 bits 实际会取值为 4。
-   name\_suffix：指定实例名或主机名的后缀，非必选。

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

根据上面的模板，资源编排会批量创建两个 ECS 实例。

-   两个 ECS 的实例名分别是：my.test-1114 和 my.test-1115。
-   两个 ECS 的主机名分别是： host0000 和 host0001。

**说明：** 即使是通过上面的方式指定实例名称和主机名称，最终解析出来的名字必须符合 InstanceName 和 HostName 的定义规则。如果不符合规则，则模板会验证失败。


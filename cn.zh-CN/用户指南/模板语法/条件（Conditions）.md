# 条件（Conditions） {#concept_53069_zh .concept}

每一个条件项由 Fn::And、Fn::Or、Fn::Not、或Fn::Equals 定义。根据您在创建或更新资源栈时，指定的输入参数值进行计算。在每个条件中，都可以引用其他条件、参数值或映射。在模板的 Resources 和 Outputs 部分，将条件与资源和资源属性关联起来。条件和资源的关联通过两种方式实现：Fn::If 函数或者资源的 Condition 字段。

## 语法 {#section_ehn_drw_kfb .section}

每个条件由条件名和条件本身对组成。其中条件名是字符串类型。条件是由 Fn::And、Fn::Or、Fn::Not、或Fn::Equals 定义。在本条件中还可以引用其他条件，多个条件用逗号隔开，每个条件名不能重复。

## 示例 {#section_o3p_drw_kfb .section}

以下示例如何设置 Conditions。

``` {#codeblock_z4w_szm_k03 .language-json}
"Conditions" : {
       "DevEnv": {"Fn::Equals": ["Dev", {"Ref": "EnvType"}]},
       "UTEnv": {"Fn::Equals": ["UT", {"Ref": "EnvType"}]},
       "PREEnv": {"Fn::Not": {"Fn::Or": ["DevEnv", "UTEnv"]}},
       "ProdEnv": {"Fn::And": [{"Fn::Equals": ["Prod", {"Ref": "EnvType"}]}, "PREEnv"]}
}
			
```

以下示例如何关联 Conditions 和 Resources。本示例中，设置根据 EnvType 参数值决定是否给 ECS instance 创建数据盘 和 OSS bucket。

``` {#codeblock_a13_ah0_5w8 .language-json}
{
    "ROSTemplateFormatVersion":"2015-09-01",
    "Parameters":{
        "EnvType":{
            "Default":"pre",
            "Type":"String"
        }
    },
    "Conditions":{
        "CreateProdRes":{
            "Fn::Equals":[
                "prod",
                {
                    "Ref":"EnvType"
                }
            ]
        }
    },
    "Resources":{
        "WebServer":{
            "Type":"ALIYUN::ECS::Instance",
            "Properties":{
                "DiskMappings":{
                    "Fn::If":[
                        "CreateProdRes",
                        [
                            {
                                "Category":"cloud_efficiency",
                                "DiskName":"FirstDataDiskName",
                                "Size":40
                            },
                            {
                                "Category":"cloud_ssd",
                                "DiskName":"SecondDataDiskName",
                                "Size":40
                            }
                        ],
                        {
                            "Ref":"ALIYUN::NoValue"
                        }
                    ]
                },
                "VpcId":"vpc-2zew9pxh2yirtzqxdboi1",
                "SystemDiskCategory":"cloud_efficiency",
                "SecurityGroupId":"sg-2zece6wcqriejf1v91sr",
                "SystemDiskSize":40,
                "ImageId":"centos_6_8_64_40G_base_20170222.vhd",
                "IoOptimized":"optimized",
                "VSwitchId":"vsw-2zed9txvy7h2srqo6jmgq",
                "InstanceType":"ecs.n1.medium"
            }
        }，
        "OssBucket": {
            "Type": "ALIYUN::OSS::Bucket",
            "Condition": "CreateProdRes",
            "Properties": {
                "AccessControl": "private",
                "BucketName": "myprodbucket"
            }
        }
    },
    "Outputs":{
        "InstanceId":{
            "Value":{
                "Fn::GetAtt":[
                    "WebServer",
                    "InstanceId"
                ]
            }
        },
        "OssDomain":{
            "Condition": "CreateProdRes",
            "Value":{
                "Fn::GetAtt":[
                    "OssBucket",
                    "DomainName"
                ]
            }
        }
    }
}
			
```


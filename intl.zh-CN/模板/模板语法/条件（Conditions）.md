# 条件（Conditions）

条件由Fn::And、Fn::Or、Fn::Not或Fn::Equals定义，根据您在创建或更新资源栈时，指定的输入参数值进行计算。在每个条件中，都可以引用其他条件、参数值或映射。

## 语法

每个条件由条件名和条件本身组成，其中条件名是字符串类型。多个条件用半角逗号（,）隔开，每个条件名不能重复。

模板的Resources和Outputs部分，将条件与资源关联起来。条件和资源的关联通过两种方式实现：Fn::If函数或者资源的Condition字段。

允许使用如下函数，但不能是最外层的函数：

Fn::Select、 Fn::Join、 Fn::Split、Fn::Replace、Fn::Base64Encode、Fn::Base64Decode、Fn::MemberListToMap、Fn::If、 Fn::ListMerge、 Fn::GetJsonValue、Fn::MergeMapToList、Fn::SelectMapList、Fn::Add、Fn::Avg、Fn::Str、Fn::Calculate、Ref（仅参数引用）、Fn:: FindInMap、Fn::Max、Fn::Min。

## 示例

-   设置Conditions

    ```
    "Conditions" : {
           "DevEnv": {"Fn::Equals": ["Dev", {"Ref": "EnvType"}]},
           "UTEnv": {"Fn::Equals": ["UT", {"Ref": "EnvType"}]},
           "PREEnv": {"Fn::Not": {"Fn::Or": ["DevEnv", "UTEnv"]}},
           "ProdEnv": {"Fn::And": [{"Fn::Equals": ["Prod", {"Ref": "EnvType"}]}, "PREEnv"]}
    }           
    ```

-   关联Conditions和Resources

    本示例中，根据EnvType参数值决定是否为ECS instance创建数据盘和OSS bucket。

    ```
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
                    "VpcId":"vpc-2zew9pxh2yirtzqxd****",
                    "SystemDiskCategory":"cloud_efficiency",
                    "SecurityGroupId":"sg-2zece6wcqriejf1v****",
                    "SystemDiskSize":40,
                    "ImageId":"centos_6_8_64_40G_base_2017****.vhd",
                    "IoOptimized":"optimized",
                    "VSwitchId":"vsw-2zed9txvy7h2srqo6****",
                    "InstanceType":"ecs.n1.medium"
                }
            },
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



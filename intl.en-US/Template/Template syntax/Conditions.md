# Conditions

Condition bodies are defined by Fn::And, Fn::Or, Fn::Not, and Fn::Equals operators. These operators, along with the parameters that you specify when you create or update a stack, are used to evaluate each condition. You can reference other conditions, parameters, and mappings in your condition.

## Syntax

Each condition consists of a condition name and a condition body. The condition name is a string. Multiple conditions are separated by commas \(,\). Each condition name must be unique.

Conditions are used in resource and output definitions to establish dependencies. Use Fn::If or Condition in resource and output definitions to implement conditions.

The following functions can be used, but not as the outermost functions:

Fn::Select, Fn::Join, Fn::Split, Fn::Replace, Fn::Base64Encode, Fn::Base64Decode, Fn::MemberListToMap, Fn::If, Fn::ListMerge, Fn::GetJsonValue, Fn::MergeMapToList, Fn::SelectMapList, Fn::Add, Fn::Avg, Fn::Str, Fn::Calculate, Ref \(for parameter references only\), Fn:: FindInMap, Fn::Max, and Fn::Min.

## Examples

-   The following example shows how to define conditions:

    ```
    "Conditions" : {
           "DevEnv": {"Fn::Equals": ["Dev", {"Ref": "EnvType"}]},
           "UTEnv": {"Fn::Equals": ["UT", {"Ref": "EnvType"}]},
           "PREEnv": {"Fn::Not": {"Fn::Or": ["DevEnv", "UTEnv"]}},
           "ProdEnv": {"Fn::And": [{"Fn::Equals": ["Prod", {"Ref": "EnvType"}]}, "PREEnv"]}
    }           
    ```

-   The following example shows how to use conditions in a resource definition.

    In this example, a condition is used to determine whether to create a data disk and an OSS bucket for an ECS instance based on the EnvType value.

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



# 创建对象存储OSS存储空间

本文为您介绍如何在Python语言环境通过ROS CDK创建对象存储OSS存储空间。

请确保Python版本在3.6及以上。

## 步骤一：初始化工程

1.  执行以下命令，创建工程目录并初始化工程。

    每个ROS CDK应用都要求创建在一个独立的工程目录下，且该应用需要使用独立工程目录中模块的依赖项。所以在创建应用之前，需要先创建一个工程目录并进行初始化。

    ```
    mkdir cdk_demo
    cd cdk_demo
    ros-cdk init --language=python --generate-only=true
    ```

2.  执行以下命令，创建一个属于当前工程的虚拟环境。

    Python工程的运行依赖于虚拟环境（virtualenv），所以在初始化Python工程之后需要创建一个属于当前工程的虚拟环境。

    ```
    python3 -m venv .venv
    ```

3.  执行以下命令，进入虚拟环境。

    ```
    source .venv/bin/activate
    ```


## 步骤二：配置阿里云凭证信息

1.  执行以下命令，配置阿里云凭证信息。

    ```
    ros-cdk config
    ```

2.  根据界面提示输入配置信息。

    ```
    endpoint(optional, default:https://ros.aliyuncs.com):
    defaultRegionId(optional, default:cn-hangzhou):cn-beijing
    
    [1] AK
    [2] StsToken
    [3] RamRoleArn
    [4] EcsRamRole
    [0] CANCEL
    
    Authenticate mode [1...4 / 0]: 1
    accessKeyId:************************
    accessKeySecret:******************************
    
     ✅ Your cdk configuration has been saved successfully!
    ```

    配置内容说明如下：

    -   endpoint：ROS服务地址。默认值为https://ros.aliyuncs.com。
    -   defaultRegionId：ROS资源栈部署的地域。默认值为cn-hangzhou。
    -   Authenticate mode：鉴权方式。本示例的鉴权方式为AccessKey，您需要输入AccessKey ID和AccessKey Secret。

## 步骤三：安装依赖

1.  修改`requirements.txt`文件，添加ECS SDK依赖包。

    ```
    ros-cdk-core
    ros-cdk-ecs
    ```

2.  执行以下命令，安装依赖。

    ```
    pip install -r requirements.txt
    ```


## 步骤四：创建资源

1.  修改`demo_stack.py`文件，创建OSS存储空间。

    ```
    import ros_cdk_core as core
    import ros_cdk_oss as oss
    
    
    class CdkDemoStack(core.Stack):
    
        def __init__(self, scope: core.Construct, construct_id: str, **kwargs) -> None:
            super().__init__(scope, construct_id, **kwargs)
            # create the ros parameters
            oss_bucket_name = core.RosParameter(
                self, "OssBucketName",
                type=core.RosParameterType.STRING,
                description="3 to 63 characters, not beginning and ending with a hyphen (-), can contain lowercase letters, Numbers and hyphens (-)"
            )
            oss_access_control = core.RosParameter(
                self, "OssAccessControl",
                type=core.RosParameterType.STRING,
                description="Set the access permission of the bucket",
                allowed_values=["private", "public-read", "public-read-write"],
                default_value="private"
            )
    
            # define the resource
    
            oss_bucket = oss.Bucket(self, "OSSBucket", props=oss.BucketProps(
                bucket_name=oss_bucket_name,
                access_control=oss_access_control,
            ))
    
            # define the outputs
            out_bucket_domain_name = core.RosOutput(
                self, "BucketDomainName", value=oss_bucket.attr_domain_name)
    ```

2.  执行以下命令，生成模板文件。

    ```
    ros-cdk synth --json
    ```

    执行命令后，输出以下内容：

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Parameters": {
        "OssBucketName": {
          "Type": "String",
          "Description": "3 to 63 characters, not beginning and ending with a hyphen (-), can contain lowercase letters, Numbers and hyphens (-)"
        },
        "OssAccessControl": {
          "Type": "String",
          "Default": "private",
          "AllowedValues": [
            "private",
            "public-read",
            "public-read-write"
          ],
          "Description": "Set the access permission of the bucket"
        }
      },
      "Resources": {
        "OSSBucket": {
          "Type": "ALIYUN::OSS::Bucket",
          "Properties": {
            "BucketName": {
              "Ref": "OssBucketName"
            },
            "AccessControl": {
              "Ref": "OssAccessControl"
            },
            "DeletionForce": false
          }
        }
      },
      "Outputs": {
        "BucketDomainName": {
          "Value": {
            "Fn::GetAtt": [
              "OSSBucket",
              "DomainName"
            ]
          }
        }
      }
    }
    ```


## 步骤五：单元测试

1.  修改`test/cdk_demo.test.ts`文件，验证资源栈创建OSS存储空间的可行性。

    ```
    # !/usr/bin/env python3
    import unittest
    import ros_cdk_core as core
    from cdk_demo.cdk_demo_stack import CdkDemoStack
    
    
    class TestStack(unittest.TestCase):
        def setUp(self):
            pass
    
        def test_stack(self):
            app = core.App()
            stack = CdkDemoStack(app, "testcdk-demo")
            artifact = app.synth().get_stack_artifact(stack.artifact_id).template
            expect = {
                "ROSTemplateFormatVersion": "2015-09-01",
                "Parameters": {
                    "OssBucketName": {
                        "Type": "String",
                        "Description": "3 to 63 characters, not beginning and ending with a hyphen (-), can contain lowercase letters, Numbers and hyphens (-)"
                    },
                    "OssAccessControl": {
                        "Type": "String",
                        "Default": "private",
                        "AllowedValues": [
                            "private",
                            "public-read",
                            "public-read-write"
                        ],
                        "Description": "Set the access permission of the bucket"
                    }
                },
                "Resources": {
                    "OSSBucket": {
                        "Type": "ALIYUN::OSS::Bucket",
                        "Properties": {
                            "BucketName": {
                                "Ref": "OssBucketName"
                            },
                            "AccessControl": {
                                "Ref": "OssAccessControl"
                            },
                            "DeletionForce": False
                        }
                    }
                },
                "Outputs": {
                    "BucketDomainName": {
                        "Value": {
                            "Fn::GetAtt": [
                                "OSSBucket",
                                "DomainName"
                            ]
                        }
                    }
                }
            }
            self.assertDictEqual(artifact, expect)
    
        def tearDown(self):
            pass
    
    
    if __name__ == '__main__':
        unittest.main()
    ```

2.  执行以下命令，进行单元测试。

    ```
    python -m unittest  -v
    ```

    执行命令后，输出以下内容：

    ```
    test_stack (test.test_cdk_demo.TestStack) ... ok
    
    ----------------------------------------------------------------------
    Ran 1 test in 0.057s
    
    OK
    ```


## 步骤六：管理资源栈

您可以使用ROS CDK命令，创建、查询或删除资源栈。

-   创建资源栈

    执行以下命令，创建资源栈，并指定OssBucketName（OSS存储空间名称）和OssAccessControl（OSS存储空间访问权限）。

    ```
    ros-cdk deploy --parameters OssBucketName=bestros  --parameters OssAccessControl=private
    ```

    执行命令后，输出以下内容：

    ```
     ✅  The deployment(create stack) has completed!
    RequestedId: BC963C80-054D-41A0-87E7-001E0AB7B1BA
    StackId: 218f0db0-7992-4e70-a586-12****
    ```

-   查询资源栈

    执行以下命令，查询资源栈。

    ```
    ros-cdk list-stacks
    ```

    执行命令后，输出以下内容：

    ```
    ✅ The Stacks list is:
     [
            {
                    "Status": "CREATE_COMPLETE",
                    "StackType": "ROS",
                    "ResourceGroupId": "rg-acfm2xwmxv*****",
                    "StatusReason": "Stack CREATE completed successfully",
                    "CreateTime": "2021-06-16T06:53:54",
                    "RegionId": "cn-beijing",
                    "StackName": "CdkDemoStack",
                    "DisableRollback": false,
                    "Tags": [
                            {
                                    "Value": "rg-acfm2xwmdg****",
                                    "Key": "acs:rm:rgId"
                            }
                    ],
                    "StackId": "218f0db0-7992-4e70-a586-12****",
                    "TimeoutInMinutes": 20
            }
    ]
    ```

-   查询资源栈的输出信息

    执行以下命令，查询资源栈的输出信息。

    ```
    ros-cdk output CdkDemoStack
    ```

    执行命令后，输出以下内容：

    ```
      ✅ The Stack CdkDemoStack 
     Output is: 
     [
            {
                    "Description": "No description given",
                    "OutputKey": "BucketDomainName",
                    "OutputValue": "bestros.oss-cn-beijing.aliyuncs.com"
            }
    ]
    ```

-   删除资源栈
    1.  执行以下命令，删除资源栈。

        ```
        ros-cdk destroy
        ```

    2.  根据界面提示，确认删除。

        ```
        Please confirm.(Y/N)
        y
        ```

        执行命令后，输出以下内容：

        ```
        ✅ Deleted
        RequestedId: 1BF864E1-7965-4148-A302-E6ABFF806641
        ```



# Python示例

本文以创建一个阿里云专有网络（VPC）实例为例，为您介绍如何在Python语言环境使用ROS CDK。

请确保Python版本在3.6及以上。

## 步骤一：初始化工程

1.  执行以下命令，创建工程目录并初始化工程。

    每个ROS CDK应用都要求创建在一个独立的工程目录下，且该应用需要使用独立工程目录中模块的依赖项。所以在创建应用之前，需要先创建一个工程目录并进行初始化。

    ```
    mkdir demo
    cd demo
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
    -   Authenticate mode：鉴权方式。本示例的鉴权方式为AccessKey，您需要输入accessKeyId和accessKeySecret。

## 步骤三：预览工程结构

执行以下命令，预览工程结构。

```
tree .
```

执行命令后，输出以下内容：

```
.
├── app.py
├── cdk.json
├── demo
│   ├── demo_stack.py
│   └── __init__.py
├── README.md
├── requirements.txt
├── setup.py
├── source.bat
└── test
    ├── __init__.py
    └── test_demo.py

2 directories, 10 files
```

工程结构说明如下：

-   `app.py`：入口文件。

    **说明：** 一个工程有且仅有一个应用。

    示例中创建了一个应用（类型为core.App）和一个资源栈（类型为DemoStack，名称为demo），并将资源栈添加到应用中。`app.py`文件内容如下：

    ```
    #!/usr/bin/env python3
    
    import ros_cdk_core as core
    
    from demo.demo_stack import DemoStack
    
    
    app = core.App()
    
    DemoStack(app, "demo")
    
    app.synth()
    ```

-   `demo/demo_stack.py`：资源栈的定义文件。

    您可以将资源添加到资源栈中，动态构建资源栈。初始化生成的代码中，只为资源栈添加了描述信息。`demo_stack.py`文件内容如下：

    ```
    import ros_cdk_core as core
    
    
    class DemoStack(core.Stack):
    
        def __init__(self, scope: core.Construct, construct_id: str, **kwargs) -> None:
            super().__init__(scope, construct_id, **kwargs)
    
            # The code that defines your stack goes here
    ```

-   `test/test_demo.py`：单元测试文件。

    用于验证构建资源栈的逻辑是否符合预期。`test_demo.py`文件内容如下：

    ```
    #!/usr/bin/env python3
    import unittest
    import ros_cdk_core as core
    from demo.demo_stack import DemoStack
    
    class TestStack(unittest.TestCase):
        def setUp(self):
            pass
    
        def test_stack(self):
            app = core.App()
            stack = DemoStack(app, "testdemo")
            artifact = app.synth().get_stack_artifact(stack.artifact_id).template
            expect = {
                      "ROSTemplateFormatVersion": "2015-09-01"
                    }
            self.assertDictEqual(artifact, expect)
    
        def tearDown(self):
            pass
    
    
    if __name__ == '__main__':
        unittest.main()
    ```


## 步骤四：安装依赖

1.  修改`requirements.txt`文件，添加ECS SDK依赖包。

    ```
    ros-cdk-core
    ros-cdk-ecs
    ```

2.  执行以下命令，安装依赖。

    -   方法一：

        ```
        pip install -r requirements.txt
        ```

    -   方法二：

        ```
        pip install ros-cdk-core ros-cdk-ecs
        ```


## 步骤五：创建资源

1.  修改`demo_stack.py`文件，创建VPC。

    ```
    import ros_cdk_core as core
    import ros_cdk_ecs as ecs
    
    class DemoStack(core.Stack):
    
        def __init__(self, scope: core.Construct, construct_id: str, **kwargs) -> None:
            super().__init__(scope, construct_id, **kwargs)
    
            # The code that defines your stack goes here
            props = {
                        'cidrBlock': '10.0.0.0/8',
                        'description': 'This is ros python cdk test',
                        'vpcName': 'test-ros-cdk-vpc'
                    }
            ecs.Vpc(self, "VPC", props)
    ```

2.  执行以下命令，生成模板文件。

    ```
    ros-cdk synth --json
    ```

    执行命令后，输出以下内容：

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "VPC": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "CidrBlock": "10.0.0.0/8",
            "Description": "This is ros python cdk test",
            "EnableIpv6": false,
            "VpcName": "test-ros-cdk-vpc"
          }
        }
      }
    }
    ```


## 步骤六：单元测试

1.  修改`test_demo.py`文件，验证资源栈创建VPC的可行性。

    ```
    #!/usr/bin/env python3
    import unittest
    import ros_cdk_core as core
    from demo.demo_stack import DemoStack
    
    class TestStack(unittest.TestCase):
        def setUp(self):
            pass
    
        def test_stack(self):
            app = core.App()
            stack = DemoStack(app, "testdemo")
            artifact = app.synth().get_stack_artifact(stack.artifact_id).template
            expect = {
                      "ROSTemplateFormatVersion": "2015-09-01",
                      "Resources": {
                        "VPC": {
                          "Type": "ALIYUN::ECS::VPC",
                          "Properties": {
                            "CidrBlock": "10.0.0.0/8",
                            "Description": "This is ros python cdk test",
                            "EnableIpv6": False,
                            "VpcName": "test-ros-cdk-vpc"
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
    test_stack (test.test_demo.TestStack) ... ok
    
    ----------------------------------------------------------------------
    Ran 1 test in 0.052s
    
    OK
    ```


## 步骤七：管理资源栈

您可以使用ROS CDK命令，创建、查询或删除资源栈。

-   创建资源栈

    执行以下命令，创建资源栈。

    ```
    ros-cdk deploy
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
                    "StatusReason": "Stack CREATE completed successfully",
                    "CreateTime": "2021-01-26T12:58:05",
                    "RegionId": "cn-beijing",
                    "DisableRollback": false,
                    "StackName": "demo",
                    "Tags": [],
                    "StackId": "218f0db0-7992-4e70-a586-152es****",
                    "TimeoutInMinutes": 20
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
        The following stack(s) will be destroyed(Only deployed stacks will be displayed).
        
        DemoStack
        
        Please confirm.(Y/N)
        Y
        ```

        执行命令后，输出以下内容：

        ```
        ✅ Deleted
        RequestedId: 1BF864E1-7965-4148-A302-E6ABFF806641
        ```



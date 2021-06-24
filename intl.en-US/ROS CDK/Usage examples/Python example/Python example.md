# Python example

This topic describes how to ROS Cloud Development Toolkit \(CDK\) for Python. In this example, a VPC is created.

The Python version is 3.6 or later.

## Step 1: Initialize a project

1.  Run the following commands to create a project directory and initialize the project:

    Each ROS CDK application must be created within an independent project directory. The application uses the dependencies of the modules in the directory. Therefore, you must create a project directory and initialize the project before you create an application.

    ```
    mkdir demo
    cd demo
    ros-cdk init --language=python --generate-only=true
    ```

2.  Run the following command to create a virtual environment that belongs to the current project.

    This operation is necessary because a virtual environment is required for the execution of every Python project.

    ```
    python3 -m venv .venv
    ```

3.  Run the following command to enter the virtual environment:

    ```
    source .venv/bin/activate
    ```


## Step 2: Configure an Alibaba Cloud credential

1.  Run the following command to configure an Alibaba Cloud credential:

    ```
    ros-cdk config
    ```

2.  Enter the configuration information as prompted.

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

    Parameter description:

    -   endpoint: the endpoint of ROS. The default value is https://ros.aliyuncs.com.
    -   defaultRegionId: the ID of the region where the stack is deployed. The default value is cn-hangzhou.
    -   Authenticate mode: the authentication method. In this example, an AccessKey pair is used for authentication. You must specify the accessKeyId and accessKeySecret parameters.

## Step 3: Preview the project structure

Run the following command to preview the project structure:

```
tree .
```

The following content is returned after you run the command:

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

The following section describes the project structure:

-   `app.py`: the launch file of the project.

    **Note:** A project can contain only a single application.

    In the example, an application of the core.App type and a DemoStack-typed stack named demo are created. The stack is added to the application. The `app.py` file contains the following content:

    ```
    #!/usr/bin/env python3
    
    import ros_cdk_core as core
    
    from demo.demo_stack import DemoStack
    
    
    app = core.App()
    
    DemoStack(app, "demo")
    
    app.synth()
    ```

-   `demo/demo_stack.py`: the definition file of the stack.

    You can add resources to the stack to dynamically create the stack. The code generated when the stack is created only contains information about the stack. `demo_stack.py` contains the following content:

    ```
    import ros_cdk_core as core
    
    
    class DemoStack(core.Stack):
    
        def __init__(self, scope: core.Construct, construct_id: str, **kwargs) -> None:
            super().__init__(scope, construct_id, **kwargs)
    
            # The code that defines your stack goes here
    ```

-   `test/test_demo.py`: the unit test file.

    The file is used to check whether the created stack follows the expected logic. The `test_demo.py` file contains the following content:

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


## Step 4: Install dependencies

1.  Modify the `requirements.txt` file to add the ECS SDK dependency package.

    ```
    ros-cdk-core
    ros-cdk-ecs
    ```

2.  Run one of the following commands to install the dependency package:

    -   Method 1:

        ```
        pip install -r requirements.txt
        ```

    -   Method 2:

        ```
        pip install ros-cdk-core ros-cdk-ecs
        ```


## Step 5: Create resources

1.  Modify the `demo_stack.py` file to create a VPC

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

2.  Run the following command to generate a template file:

    ```
    ros-cdk synth --json
    ```

    The following content is returned after you run the command:

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


## Step 6: Perform a unit test

1.  Modify the `test_demo.py` file to check whether a VPC can be created for the stack.

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

2.  Run the following command to perform a unit test:

    ```
    python -m unittest  -v
    ```

    The following content is returned after you run the command:

    ```
    test_stack (test.test_demo.TestStack) ... ok
    
    ----------------------------------------------------------------------
    Ran 1 test in 0.052s
    
    OK
    ```


## Step 7: Manage stacks

You can create, query, or delete stacks by running ROS CDK commands.

-   Create a stack

    Run the following command to create a stack:

    ```
    ros-cdk deploy
    ```

    The following content is returned after you run the command:

    ```
     ✅  The deployment(create stack) has completed!
    RequestedId: BC963C80-054D-41A0-87E7-001E0AB7B1BA
    StackId: 218f0db0-7992-4e70-a586-12****
    ```

-   Query information about a stack

    Run the following command to query information about a stack:

    ```
    ros-cdk list-stacks
    ```

    The following content is returned after you run the command:

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

-   Delete a stack
    1.  Run the following command to delete a stack:

        ```
        ros-cdk destroy
        ```

    2.  Confirm the deletion operation as prompted.

        ```
        The following stack(s) will be destroyed(Only deployed stacks will be displayed).
        
        DemoStack
        
        Please confirm.(Y/N)
        Y
        ```

        The following content is returned after you run the command:

        ```
        ✅ Deleted
        RequestedId: 1BF864E1-7965-4148-A302-E6ABFF806641
        ```



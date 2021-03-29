# JavaScript example

This topic describes how to use ROS Cloud Development Toolkit \(CDK\) for JavaScript. In this example, a VPC is created.

## Step 1: Initialize a project

Each ROS CDK application must be created within an independent project directory. The application uses the dependencies of the modules in the directory. Therefore, you must create a project directory and initialize the project before you create an application.

Run the following commands to create a project directory and initialize the project:

```
mkdir demo
cd demo
ros-cdk init --language=javascript --generate-only=true
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
├── bin
│   └── demo.js
├── cdk.json
├── jest.config.js
├── lib
│   └── demo-stack.js
├── package.json
├── README.md
└── test
    └── demo.test.js

3 directories, 7 files
```

The following section describes the project structure:

-   `bin/demo.js`: the launch file of the project.

    **Note:** A project can contain only a single application.

    In the example, an application of the ros.App type and a DemoStack-typed stack named DemoStack are created. The stack is added to the application. The `demo.js` file contains the following content:

    ```
    #!/usr/bin/env node
    
    const ros = require('@alicloud/ros-cdk-core');
    const { DemoStack } = require('../lib/demo-stack');
    
    const app = new ros.App();
    new DemoStack(app, 'DemoStack');
    app.synth();
    ```

-   `lib/demo-stack.js`: the definition file of the stack.

    You can add resources to the stack to dynamically create the stack. The code generated when the stack is created only contains information about the stack. `demo-stack.js` contains the following content:

    ```
    const ros = require('@alicloud/ros-cdk-core');
    
    class DemoStack extends ros.Stack {
      /**
       *
       * @param {ros.Construct} scope
       * @param {string} id
       * @param {ros.StackProps} props
       */
      constructor(scope, id, props) {
        super(scope, id, props);
        new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.");
        // The code that defines your stack goes here
      }
    }
    
    module.exports = { DemoStack }
    ```

-   `test/demo.test.js`: the unit test file.

    The file is used to check whether the created stack follows the expected logic. `demo.test.js` contains the following content:

    ```
    const { expect, matchTemplate, MatchStyle } = require('@alicloud/ros-cdk-assert');
    const ros = require('@alicloud/ros-cdk-core');
    const Demo = require('../lib/demo-stack');
    
    test('Stack with version.', () => {
        const app = new ros.App();
        // WHEN
        const stack = new Demo.DemoStack(app, 'MyTestStack');
        // THEN
        expect(stack).to(matchTemplate({
                ROSTemplateFormatVersion: '2015-09-01',
                Description: "This is the simple ros cdk app example."
            }, MatchStyle.EXACT))
    });
    ```


## Step 4: Install dependencies

1.  Modify the `package.json` file to add the ECS SDK dependency package.

    ```
    {
      "name": "demo",
      "version": "0.1.0",
      "bin": {
        "demo": "bin/demo.js"
      },
      "scripts": {
        "build": "echo \"The build step is not required when using JavaScript!\" && exit 0",
        "cdk": "cdk",
        "test": "jest"
      },
      "devDependencies": {
        "@types/jest": "^25.2.1",
        "@types/node": "10.17.5",
        "typescript": "^3.9.7",
        "jest": "^25.5.0",
        "ts-jest": "^25.3.1",
        "ts-node": "^8.1.0",
        "babel-jest": "^26.6.3",
        "@babel/core": "^7.12.9",
        "@babel/preset-env": "7.12.7",
        "@babel/preset-typescript": "^7.12.7",
        "@alicloud/ros-cdk-assert": "^1.0.0"
      },
      "dependencies": {
        "@alicloud/ros-cdk-core": "^1.0.0",
        "@alicloud/ros-cdk-ecs": "^1.0.0"
      }
    }
    ```

2.  Run the following command to install the dependency package:

    ```
    npm install
    ```


## Step 5: Create resources

1.  Modify the `demo-stack.js` file to create a VPC

    ```
    const ros = require('@alicloud/ros-cdk-core');
    const ecs = require('@alicloud/ros-cdk-ecs');
    
    class DemoStack extends ros.Stack {
      /**
       *
       * @param {ros.Construct} scope
       * @param {string} id
       * @param {ros.StackProps} props
       */
      constructor(scope, id, props) {
        super(scope, id, props);
        new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.");
        // The code that defines your stack goes here
        new ecs.Vpc(this, 'vpc-from-ros-cdk', {
          vpcName: 'test-ros-cdk-javascript',
          cidrBlock: '10.0.0.0/8',
          description: 'This is ros cdk test'
       });
      }
    }
    
    module.exports = { DemoStack }
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
            "Description": "This is ros cdk test",
            "EnableIpv6": false,
            "VpcName": "test-ros-cdk-javascript"
          }
        }
      }
    }
    ```


## Step 6: Perform a unit test

1.  Modify the `demo.test.js` file to check whether a VPC can be created for the stack.

    ```
    const {expect, matchTemplate, MatchStyle} = require('@alicloud/ros-cdk-assert');
    const ros = require('@alicloud/ros-cdk-core');
    const Demo = require('../lib/demo-stack');
    
    test('Stack with version.', () => {
        const app = new ros.App();
        // WHEN
        const stack = new Demo.DemoStack(app, 'MyTestStack');
        // THEN
        expect(stack).to(matchTemplate(
            {
                "Description": "This is the simple ros cdk app example.",
                "ROSTemplateFormatVersion": "2015-09-01",
                "Resources": {
                    "vpc-from-ros-cdk": {
                        "Type": "ALIYUN::ECS::VPC",
                        "Properties": {
                            "CidrBlock": "10.0.0.0/8",
                            "Description": "This is ros cdk test",
                            "EnableIpv6": false,
                            "VpcName": "test-ros-cdk-javascript"
                        }
                    }
                }
            }
            , MatchStyle.EXACT))
    });
    ```

2.  Run the following command to perform a unit test:

    ```
    npm test
    ```

    The following content is returned after you run the command:

    ```
    > demo@0.1.0 test /opt/demo
    > jest
    
     PASS  test/demo.test.js
      ✓ Stack with version. (257ms)
    
    Test Suites: 1 passed, 1 total
    Tests:       1 passed, 1 total
    Snapshots:   0 total
    Time:        1.79s
    Ran all test suites.
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
    StackId: 218f0db0-7992-4e70-a586-15****
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
                    "StackName": "DemoStack",
                    "Tags": [],
                    "StackId": "218f0db0-7992-4e70-a586-54e****",
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



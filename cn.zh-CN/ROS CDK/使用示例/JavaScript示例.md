# JavaScript示例

本文以创建一个阿里云专有网络（VPC）实例为例，为您介绍如何在JavaScript语言环境使用ROS CDK。

## 步骤一：初始化工程

每个ROS CDK应用都要求创建在一个独立的工程目录下，且该应用需要使用独立工程目录中模块的依赖项。所以在创建应用之前，需要先创建一个工程目录并进行初始化。

执行以下命令，创建工程目录并初始化工程。

```
mkdir demo
cd demo
ros-cdk init --language=javascript --generate-only=true
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

工程结构说明如下：

-   `bin/demo.js`：入口文件。

    **说明：** 一个工程有且仅有一个应用。

    示例中创建了一个应用（类型为ros.App）和一个资源栈（类型为DemoStack，名称为DemoStack），并将资源栈添加到应用中。`demo.js`文件内容如下：

    ```
    #!/usr/bin/env node
    
    const ros = require('@alicloud/ros-cdk-core');
    const { DemoStack } = require('../lib/demo-stack');
    
    const app = new ros.App();
    new DemoStack(app, 'DemoStack');
    app.synth();
    ```

-   `lib/demo-stack.js`：资源栈的定义文件。

    您可以将资源添加到资源栈中，动态构建资源栈。初始化生成的代码中，只为资源栈添加了描述信息。`demo-stack.js`文件内容如下：

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

-   `test/demo.test.js`：单元测试文件。

    用于验证构建资源栈的逻辑是否符合预期。`demo.test.js`文件内容如下：

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


## 步骤四：安装依赖

1.  修改`package.json`文件，添加ECS依赖包。

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

2.  执行以下命令，安装依赖。

    ```
    npm install
    ```


## 步骤五：创建资源

1.  修改`demo-stack.js`文件，创建VPC。

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
            "Description": "This is ros cdk test",
            "EnableIpv6": false,
            "VpcName": "test-ros-cdk-javascript"
          }
        }
      }
    }
    ```


## 步骤六：单元测试

1.  修改`demo.test.js`文件，验证资源栈创建VPC的可行性。

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

2.  执行以下命令，进行单元测试。

    ```
    npm test
    ```

    执行命令后，输出以下内容：

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
    StackId: 218f0db0-7992-4e70-a586-15****
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
                    "StackName": "DemoStack",
                    "Tags": [],
                    "StackId": "218f0db0-7992-4e70-a586-54e****",
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



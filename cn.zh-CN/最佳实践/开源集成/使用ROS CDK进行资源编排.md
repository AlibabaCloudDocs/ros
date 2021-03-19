# 使用ROS CDK进行资源编排

ROS CDK（Cloud Development Toolkit）是ROS推出的代码开发工具，帮助您使用少量代码实现复杂模板的资源编排效果。

-   ROS CDK已经在[github](https://github.com/aliyun/Resource-Orchestration-Service-Cloud-Development-Kit)上开源。
-   ROS CDK⽀持阿⾥云60种服务、276种资源。
-   ROS CDK⽀持JavaScript、TypeScript和Java三种编程语⾔。

## 安装CLI

CLI⼯具提供了便捷使⽤ROS CDK的能力。以下示例将在CentOS 8.2 64位的系统上安装CLI。

1.  执行以下命令，安装CLI。

    ```
    # 由于ROS CDK使用TypeScript开发，因此需要安装相关软件包。
    # 安装Node.js、npm、tsc、lerna。
    yum install -y nodejs
    npm install typescript -g
    npm install lerna -g
    # 安装ros-cdk-cli。
    npm install @alicloud/ros-cdk-cli -g
    ```

2.  执行以下命令，查看ROS CDK功能列表。

    ```
    ros-cdk
    ```

    执行命令后，输出以下内容：

    ```
    Usage: ros-cdk COMMAND
    
    Commands:
      ros-cdk init [TEMPLATE]         Create a new, empty CDK project from a
                                      template. Invoked without TEMPLATE, the app
                                      template will be used.
      ros-cdk list [STACKS..]         Lists all stacks in the app      [aliases: ls]
      ros-cdk synthesize [STACKS..]   Synthesizes and prints the ROS template for
                                      this stack                    [aliases: synth]
      ros-cdk deploy [STACKS..]       Deploys the stack(s) named STACKS to ROS into
                                      your alicloud account
      ros-cdk diff [STACKS..]         Compares the specified stack with the deployed
                                      stack or a local template file, and returns
                                      with status 1 if any difference is found
      ros-cdk destroy [STACKS..]      Destroy the stack(s) named STACKS
      ros-cdk event [STACK..]         Get resource events within the resource STACK
      ros-cdk resource [STACKS..]     Get resources in the resource STACKS
      ros-cdk list-stacks [STACKS..]  Get resources in the resource STACKS
      ros-cdk load-config             Load Aliyun CLI config to CDK.
      ros-cdk config                  Set your alicloud account configuration.
    
    Options:
      --json, -j       Use JSON output instead of YAML when templates are printed to
                       STDOUT                             [boolean] [default: false]
      --ignore-errors  Ignores synthesis errors, which will likely produce an
                       invalid output                     [boolean] [default: false]
      --trace          Print trace for stack warnings                      [boolean]
      --strict         Do not construct stacks with warnings               [boolean]
      --version        Show version number                                 [boolean]
      -h, --help       Show help                                           [boolean]
    
    If your app has a single stack, there is no need to specify the stack name
    
    If one of cdk.json or ~/.cdk.json exists, options specified there will be used
    as defaults. Settings in cdk.json take precedence.
    ```

    命令说明如下表所示：

    |命令|说明|
    |--|--|
    |init|初始化ROS CDK⼯程。|
    |list（ls）|列出⼯程中的所有资源栈。|
    |synthesize（synth）|由代码⽣成资源栈模板。|
    |deploy|通过ROS部署资源栈。|
    |diff|对⽐模板的差异。|
    |destroy|通过ROS服务删除资源栈。|
    |event|通过ROS服务查询资源栈事件。|
    |resource|通过ROS服务查询资源栈资源列表。|
    |list-stacks|通过ROS服务查询资源栈列表。|
    |load-config|从阿里云CLI获取阿里云账号信息。|
    |config|配置阿⾥云账号信息。|


## 使用示例

本文以TypeScript语言为例，为您介绍如何使用ROS CDK为资源栈添加VPC。

1.  初始化工程。

    1.  执行以下命令，创建工程目录并初始化工程。

        ```
        # 创建工程目录，目录名为工程名。
        mkdir demo
        cd demo
        # 初始化工程，使用TypeScript语言。
        ros-cdk init --language=typescript --generate-only=true
        ```

    2.  执行以下命令，为工程安装依赖。

        ```
        # 安装工程所需依赖包。
        npm install
        ```

    3.  执行以下命令，查看工程结构。

        ```
        tree -I "node_modules"
        ```

        执行命令后，输出以下内容：

        ```
        .
        ├── bin
        │   └── demo.ts
        ├── cdk.json
        ├── jest.config.js
        ├── lib
        │   └── demo-stack.ts
        ├── package.json
        ├── package-lock.json
        ├── README.md
        ├── test
        │   └── demo.test.ts
        └── tsconfig.json
        
        3 directories, 9 files
        ```

        工程结构说明如下：

        -   `bin/demo.ts`：入口。

            示例中创建了一个应用（类型为ros.App）和一个资源栈（类型为DemoStack，名称为DemoStack），并将资源栈添加到应用中。`demo.ts`文件内容如下：

            **说明：** 一个工程有且仅有一个应用。

            ```
            #!/usr/bin/env node
            import * as ros from '@alicloud/ros-cdk-core';
            import { DemoStack } from '../lib/demo-stack';
            const app = new ros.App({outdir: './cdk.out'});
            new DemoStack(app, 'DemoStack');
            ```

        -   `ib/demo-stack.ts`：DemoStack的定义。

            您可以将资源添加到资源栈中，动态构建资源栈。初始化生成的代码中，只为资源栈添加了描述信息。`demo-stack.ts`文件内容如下：

            ```
            import * as ros from '@alicloud/ros-cdk-core';
            export class DemoStack extends ros.Stack {
              constructor(scope: ros.Construct, id: string, props?: ros.StackProps) {
                super(scope, id, props);
                new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.");
                // The code that defines your stack goes here
              }
            }
            ```

        -   `test/demo.test.ts`：单元测试。

            用于验证构建资源栈的逻辑是否符合预期。`demo.test.ts`文件内容如下：

            ```
            import { expect as expectCDK, matchTemplate, MatchStyle } from '@alicloud/ros-cdk-assert';
            import * as ros from '@alicloud/ros-cdk-core';
            import * as Demo from '../lib/demo-stack';
            test('Stack with version.', () => {
              const app = new ros.App();
              // WHEN
              const stack = new Demo.DemoStack(app, 'MyTestStack');
              // THEN
              expectCDK(stack).to(
                matchTemplate(
                  {
                    ROSTemplateFormatVersion: '2015-09-01',
                    Description: "This is the simple ros cdk app example."
                  },
                  MatchStyle.EXACT,
                ),
              );
            });
            ```

2.  为资源栈添加一个VPC。

    1.  修改`package.json`文件，在`dependencies`中增加`@alicloud/ros-cdk-ecs`的依赖。

        ```
        {
          "name": "demo",
          "version": "0.1.0",
          "bin": {
            "demo": "bin/demo.js"
          },
          "scripts": {
            "build": "tsc",
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

    2.  执行以下命令，为工程安装新依赖。

        ```
        # 安装工程所需依赖包。
        npm install
        ```

    3.  修改`lib/demo-stack.ts`文件，增加一个VPC。

        ```
        import * as ros from '@alicloud/ros-cdk-core';
        import * as ecs from '@alicloud/ros-cdk-ecs';
        export class DemoStack extends ros.Stack {
          constructor(scope: ros.Construct, id: string, props?: ros.StackProps) {
            super(scope, id, props);
            new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.");
            // The code that defines your stack goes here
            new ecs.Vpc(this, 'vpc-from-ros-cdk', {
              vpcName: 'test-ros-cdk',
              cidrBlock: '10.0.0.0/8',
              description: 'This is ros cdk test'
           });
          }
        }
        ```

    4.  执行以下命令，查看模板。

        ```
        ros-cdk synth --json
        ```

        执行命令后，输出以下内容：

        ```
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
                "VpcName": "test-ros-cdk"
              }
            }
          }
        }
        ```

    5.  修改`test/demo.test.ts`文件，确保单元测试与代码一致。

        ```
        import { expect as expectCDK, matchTemplate, MatchStyle } from '@alicloud/ros-cdk-assert';
        import * as ros from '@alicloud/ros-cdk-core';
        import * as Demo from '../lib/demo-stack';
        test('Stack with version.', () => {
          const app = new ros.App();
          // WHEN
          const stack = new Demo.DemoStack(app, 'MyTestStack');
          // THEN
          expectCDK(stack).to(
            matchTemplate(
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
                      "VpcName": "test-ros-cdk"
                    }
                  }
                } 
              },
              MatchStyle.EXACT,
            ),
          );
        });
        ```

    6.  执行以下命令，进行单元测试。

        ```
        npm test
        ```

        执行命令后，输出以下内容：

        ```
        > demo@0.1.0 test /root/demo
        > jest
         PASS  test/demo.test.ts
          ✓ Stack with version. (136ms)
        Test Suites: 1 passed, 1 total
        Tests:       1 passed, 1 total
        Snapshots:   0 total
        Time:        2.988s, estimated 3s
        Ran all test suites.
        ```

3.  通过ROS服务部署资源栈。

    1.  配置ROS阿里云账号信息。

        1.  执行`ros-cdk config`命令。

            ```
            ros-cdk config
            ```

        2.  根据界面提示输入配置信息。

            ```
            endpoint(optional, default:https://ros.aliyuncs.com):
            defaultRegionId(optional, default:cn-hangzhou):
            
            [1] AK
            [2] StsToken
            [3] RamRoleArn
            [4] EcsRamRole
            [0] CANCEL
            
            Authenticate mode [1...4 / 0]: 1
            accessKeyId:****************
            accessKeySecret:******************************
            
             ✅ Your cdk configuration has been saved successfully!
            ```

            配置内容说明如下：

            -   endpoint：ROS服务地址。默认值为https://ros.aliyuncs.com。
            -   defaultRegionId：ROS资源栈部署的地域。默认值为cn-hangzhou。
            -   Authenticate mode：鉴权方式。本示例的鉴权方式为AccessKey，您需要输入accessKeyId和accessKeySecret。
    2.  执行以下命令，通过ROS部署资源栈。

        ```
        ros-cdk deploy
        ```

        执行命令后，输出以下内容：

        ```
         ✅ The deployment(create stack) has completed!
        RequestedId: BC963C80-054D-41A0-87E7-001E0AB7B1BA
        StackId: 0714be3a-0713-4b7d-b7aa-************
        ```

    3.  登录[资源编排控制台](http://ros.console.aliyun.com)，在左侧导航栏单击**资源栈**，查看资源栈状态。

        资源栈状态列显示**创建成功**，表示名为DemoStack的资源栈已经创建成功。

        ![资源栈](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9003440161/p211187.png)

4.  （可选）更改VPC名称并在VPC中创建VSwitch。

    通过ROS CDK可以实现更为复杂的功能，本示例中计划实现以下功能：

    -   更改VPC名称：将VPC名称从`test-ros-cdk`更改为`test-ros-cdk-vpc`。
    -   在VPC中创建3个VSwitch：3个VSwitch有不同的名称，属于不同的可用区和网段。
    1.  修改`lib/demo-stack.ts`文件。

        ```
        import * as ros from '@alicloud/ros-cdk-core';
        import * as ecs from '@alicloud/ros-cdk-ecs';
        export class DemoStack extends ros.Stack {
          constructor(scope: ros.Construct, id: string, props?: ros.StackProps) {
            super(scope, id, props);
            new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.");
            // The code that defines your stack goes here
           const vpc = new ecs.Vpc(this, 'vpc-from-ros-cdk', {
              vpcName: 'test-ros-cdk-vpc',
              cidrBlock: '10.0.0.0/8',
              description: 'This is ros cdk test'
            });
            for (let i = 0; i < 3; i++) {
              new ecs.VSwitch(this, `vsw-from-ros-cdk-${i}`, {
                vpcId: vpc.attrVpcId,
                zoneId: ros.Fn.select(`${i}`, ros.Fn.getAzs(ros.RosPseudo.region)),
                vSwitchName: `test-ros-cdk-vsw-${i}`,
                cidrBlock: `10.0.${i}.0/24`,
              });
            }
          }
        }
        ```

        修改说明如下：

        -   通过修改vpcName的取值，为VPC更改名称。
        -   通过for循环创建VSwitch，极大地减少了代码量。
        -   通过使用`vpc.attrVpcId`获取VPC的ID。
        -   通过Fn.getAzs函数配合伪参数`RosPseudo.region`获取可用区列表。
    2.  修改`test/demo.test.ts`文件，让单元测试与代码一致，并执行`npm test`命令进行单元测试。

        具体操作，请参见步骤2。

    3.  执行`ros-cdk diff`命令，查看变更情况。

        ```
        ros-cdk diff
        ```

        执行命令后，输出以下内容：

        ```
        Stack DemoStack
        Resources
        [+] ALIYUN::ECS::VSwitch vsw-from-ros-cdk-0/vsw-from-ros-cdk-0 vsw-from-ros-cdk-0 
        [+] ALIYUN::ECS::VSwitch vsw-from-ros-cdk-1/vsw-from-ros-cdk-1 vsw-from-ros-cdk-1 
        [+] ALIYUN::ECS::VSwitch vsw-from-ros-cdk-2/vsw-from-ros-cdk-2 vsw-from-ros-cdk-2 
        [~] ALIYUN::ECS::VPC vpc-from-ros-cdk/vpc-from-ros-cdk vpc-from-ros-cdk 
         └─ [~] VpcName
             ├─ [-] test-ros-cdk
             └─ [+] test-ros-cdk-vpc
        ```

    4.  执行以下命令，通过ROS部署资源栈。

        ```
        ros-cdk deploy
        ```

        执行命令后，输出以下内容：

        ```
         ✅ The deployment(update stack) has completed!
        RequestedId: 15E99FD6-968E-47AA-9CD2-82FA6E87C08E
        StackId: 0714be3a-0713-4b7d-b7aa-************
        ```

    5.  登录[资源编排控制台](http://ros.console.aliyun.com)，在左侧导航栏单击**资源栈**，查看资源栈状态。

        资源栈状态列显示**更新完成**，表示名为DemoStack的资源栈已经更新完成。

        ![更新成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9003440161/p212888.png)

        单击**资源**页签，查看资源列表。本示例中有1个VPC资源和3个VSwith资源。

        ![资源](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9003440161/p212891.png)

5.  （可选）删除资源栈。

    1.  执行以下命令，列出工程中所有资源栈。

        ```
        ros-cdk list
        ```

        执行命令后，输出以下内容：

        ```
        DemoStack deploy
        ```

    2.  执行以下命令，删除资源栈。

        ```
        ros-cdk destroy
        ```

        执行命令后，输出以下内容：

        ```
        The following stack(s) will be destroyed(Only deployed stacks will be displayed).
        DemoStack
        Please confirm.(Y/N)
        Y
         ✅ Deleted
        RequestedId: 1BF864E1-7965-4148-A302-E6ABFF806641
        ```


## 资源相关的npm包

资源相关的npm包如下，例如`@alicloud/ros-cdk-ecs`代表ECS服务。每个npm包含这个服务在ROS上所支持的所有资源类型。

您可以登录[资源编排控制台](http://ros.console.aliyun.com)，在左侧导航栏单击**资源类型**，查看不同服务支持的资源。

```
@alicloud/ros-cdk-acm
@alicloud/ros-cdk-actiontrail
@alicloud/ros-cdk-apigateway
@alicloud/ros-cdk-arms
@alicloud/ros-cdk-bss
@alicloud/ros-cdk-cas
@alicloud/ros-cdk-cdn
@alicloud/ros-cdk-cen
@alicloud/ros-cdk-cloudfw
@alicloud/ros-cdk-cms
@alicloud/ros-cdk-cr
@alicloud/ros-cdk-cs
@alicloud/ros-cdk-datahub
@alicloud/ros-cdk-dbs
@alicloud/ros-cdk-dms
@alicloud/ros-cdk-dns
@alicloud/ros-cdk-drds
@alicloud/ros-cdk-dts
@alicloud/ros-cdk-eci
@alicloud/ros-cdk-ecs
@alicloud/ros-cdk-edas
@alicloud/ros-cdk-ehpc
@alicloud/ros-cdk-elasticsearch
@alicloud/ros-cdk-emr
@alicloud/ros-cdk-ens
@alicloud/ros-cdk-ess
@alicloud/ros-cdk-fc
@alicloud/ros-cdk-fnf
@alicloud/ros-cdk-foas
@alicloud/ros-cdk-ga
@alicloud/ros-cdk-gws
@alicloud/ros-cdk-hbr
@alicloud/ros-cdk-iot
@alicloud/ros-cdk-kafka
@alicloud/ros-cdk-kms
@alicloud/ros-cdk-marketplace
@alicloud/ros-cdk-memcache
@alicloud/ros-cdk-mns
@alicloud/ros-cdk-mongodb
@alicloud/ros-cdk-mse
@alicloud/ros-cdk-nas
@alicloud/ros-cdk-oos
@alicloud/ros-cdk-oss
@alicloud/ros-cdk-ots
@alicloud/ros-cdk-polardb
@alicloud/ros-cdk-pvtz
@alicloud/ros-cdk-ram
@alicloud/ros-cdk-rds
@alicloud/ros-cdk-redis
@alicloud/ros-cdk-resourcemanager
@alicloud/ros-cdk-rocketmq
@alicloud/ros-cdk-ros
@alicloud/ros-cdk-sae
@alicloud/ros-cdk-sag
@alicloud/ros-cdk-slb
@alicloud/ros-cdk-sls
@alicloud/ros-cdk-uis
@alicloud/ros-cdk-vpc
@alicloud/ros-cdk-vs
@alicloud/ros-cdk-waf
```


# Use ROS CDK to orchestrate resources

ROS Cloud Development Toolkit \(CDK\) is a code development tool available with Resource Orchestration Service \(ROS\). It allows you to perform complex orchestration operations on Alibaba Cloud resources by using a small amount of code.

-   ROS CDK is open-sourced on [GitHub](https://github.com/aliyun/Resource-Orchestration-Service-Cloud-Development-Kit).
-   ROS CDK supports 276 resource types of 60 Alibaba Cloud services.
-   ROS CDK supports the JavaScript, TypeScript, and Java programming languages.

## Install Alibaba Cloud CLI

Alibaba Cloud command-line interface \(CLI\) provides easy access to ROS CDK capabilities. In the following example, Alibaba Cloud CLI is installed on CentOS 8.2 64-bit.

1.  Run the following commands to install Alibaba Cloud CLI:

    ```
    # ROS CDK is developed by using TypeScript, which requires you to install relevant packages in advance.
    # Install Node.js, npm, tsc, and Lerna.
    yum install -y nodejs
    npm install typescript -g
    npm install lerna -g
    # Install ros-cdk-cli.
    npm install @alicloud/ros-cdk-cli -g
    ```

2.  Run the following command to query a list of operations that you can perform by using ROS CDK:

    ```
    ros-cdk
    ```

    The following content is returned after you run the command:

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

    The following table describes the commands in the query result.

    |Command|Description|
    |-------|-----------|
    |init|Initializes an ROS CDK project.|
    |list \(ls\)|Lists all the stacks in the project.|
    |synthesize \(synth\)|Uses code to create a stack template.|
    |deploy|Deploys a stack by using ROS.|
    |diff|Compares templates.|
    |destroy|Deletes a stack by using ROS.|
    |event|Queries stack events by using ROS.|
    |resource|Queries a list of resources in a stack by using ROS.|
    |list-stacks|Queries a list of stacks by using ROS.|
    |load-config|Queries information of the Alibaba Cloud account by using Alibaba Cloud CLI.|
    |config|Configures the Alibaba Cloud account.|


## Usage examples

The following section describes how to add a VPC to a stack by using ROS CDK. TypeScript is used in the example.

1.  Initialize a project.

    1.  Run the following command to create a project directory and initialize the project.

        ```
        # Create a project directory whose name is the same as the project name.
        mkdir demo
        cd demo
        # Initialize the project by using TypeScript.
        ros-cdk init --language=typescript --generate-only=true
        ```

    2.  Run the following command to install dependencies for the project:

        ```
        # Install the dependencies required by the project.
        npm install
        ```

    3.  Run the following command to view the project structure:

        ```
        tree -I "node_modules"
        ```

        The following content is returned after you run the command:

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

        The following section describes the project structure:

        -   `bin/demo.ts`: the launch file of the project.

            In the example, an application of the ros.App type and a DemoStack-typed stack named DemoStack are created. The stack is added to the application. The `demo.ts` file contains the following content.

            **Note:** A project contains only a single application.

            ```
            #! /usr/bin/env node
            import * as ros from '@alicloud/ros-cdk-core';
            import { DemoStack } from '../lib/demo-stack';
            const app = new ros.App({outdir: './cdk.out'});
            new DemoStack(app, 'DemoStack');
            ```

        -   `ib/demo-stack.ts`: the definition of DemoStack.

            You can add resources to the stack to dynamically create the stack. The code generated when the stack is created contains information only about the stack. `demo-stack.ts` contains the following content:

            ```
            import * as ros from '@alicloud/ros-cdk-core';
            export class DemoStack extends ros.Stack {
              constructor(scope: ros.Construct, id: string, props?: ros.StackProps) {
                super(scope, id, props);
                new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.") ;
                // The code that defines your stack goes here
              }
            }
            ```

        -   `test/demo.test.ts`: the unit test.

            The test is used to check whether the created stack follows the expected logic. `demo.test.ts` contains the following content:

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

2.  Add a VPC to the stack.

    1.  Modify the `package.json` file to add `@alicloud/ros-cdk-ecs` to `dependencies`.

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

    2.  Run the following command to install a new dependency for the project:

        ```
        # Install the dependencies required by the project.
        npm install
        ```

    3.  Modify `lib/demo-stack.ts` to add a VPC.

        ```
        import * as ros from '@alicloud/ros-cdk-core';
        import * as ecs from '@alicloud/ros-cdk-ecs';
        export class DemoStack extends ros.Stack {
          constructor(scope: ros.Construct, id: string, props?: ros.StackProps) {
            super(scope, id, props);
            new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.") ;
            // The code that defines your stack goes here
            new ecs.Vpc(this, 'vpc-from-ros-cdk', {
              vpcName: 'test-ros-cdk',
              cidrBlock: '10.0.0.0/8',
              description: 'This is ros cdk test'
           });
          }
        }
        ```

    4.  Run the following command to view the template:

        ```
        ros-cdk synth --json
        ```

        The following content is returned after you run the command:

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

    5.  Modify `test/demo.test.ts` to ensure the consistency between the unit test and the code.

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

    6.  Run the following command to perform the unit test:

        ```
        npm test
        ```

        The following content is returned after you run the command:

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

3.  Deploy the stack by using ROS.

    1.  Configure the Alibaba Cloud account.

        1.  Run the following command:``

            ```
            ros-cdk config
            ```

        2.  Enter the configuration information as prompted.

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

            Parameter description:

            -   endpoint: the endpoint of ROS. Default value: https://ros.aliyuncs.com.
            -   defaultRegionId: the ID of the region where the stack is deployed. Default value: cn-hangzhou.
            -   Authenticate mode: the authentication method. In this example, the AccessKey pair is used for authentication. You must specify the accessKeyId and accessKeySecret parameters.
    2.  Run the following command to deploy the stack by using ROS:

        ```
        ros-cdk deploy
        ```

        The following content is returned after you run the command:

        ```
         ✅ The deployment(create stack) has completed!
        RequestedId: BC963C80-054D-41A0-87E7-001E0AB7B1BA
        StackId: 0714be3a-0713-4b7d-b7aa-************
        ```

    3.  Log on to the [ROS console](http://ros.console.aliyun.com). In the left-side navigation pane, click **Stacks**. Then, view the stack status.

        If **Created** is displayed in the Status column, the stack named DemoStack is created.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2113825161/p247283.jpg)

4.  \(Optional\) Modify the name of the VPC and create vSwitches in the VPC.

    You can use ROS CDK to perform operations that are more complex. The following operations are performed in the example:

    -   Change the name of the VPC from `test-ros-cdk` to `test-ros-cdk-vpc`.
    -   Create three vSwitches in the VPC that have different names and belong to different zones and CIDR blocks.
    1.  Modify `lib/demo-stack.ts`.

        ```
        import * as ros from '@alicloud/ros-cdk-core';
        import * as ecs from '@alicloud/ros-cdk-ecs';
        export class DemoStack extends ros.Stack {
          constructor(scope: ros.Construct, id: string, props?: ros.StackProps) {
            super(scope, id, props);
            new ros.RosInfo(this, ros.RosInfo.description, "This is the simple ros cdk app example.") ;
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

        Description:

        -   vpcName indicates the name of the VPC.
        -   The for loop is used to create the vSwitches. This is a highly concise method.
        -   `vpc.attrVpcId` is used to obtain the ID of the VPC.
        -   Fn.getAzs is used with the `RosPseudo.region` psudo parameter to obtain the zone list.
    2.  Modify `test/demo.test.ts` to ensure the consistency between the unit test and the code. Then, run the `npm test` command to perform the unit test.

        For more information, see Step 2.

    3.  Run the `ros-cdk diff` command to view the modified content.

        ```
        ros-cdk diff
        ```

        The following content is returned after you run the command:

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

    4.  Run the following command to deploy the stack by using ROS:

        ```
        ros-cdk deploy
        ```

        The following content is returned after you run the command:

        ```
         ✅ The deployment(update stack) has completed!
        RequestedId: 15E99FD6-968E-47AA-9CD2-82FA6E87C08E
        StackId: 0714be3a-0713-4b7d-b7aa-************
        ```

    5.  Log on to the [ROS console](http://ros.console.aliyun.com). In the left-side navigation pane, click **Stacks**. Then, view the stack status.

        If **Updated** is displayed in the Status column, the stack named DemoStack is updated.

        ![2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2113825161/p247284.jpg)

        Click the stack ID. On the stack management page, click the **Resources** tab to view the resource list. In this example, a VPC and three vSwitches are displayed in the resource list.

        ![3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2113825161/p247285.jpg)

5.  \(Optional\) Delete the stack.

    1.  Run the following command to query a list of stacks in the project:

        ```
        ros-cdk list
        ```

        The following content is returned after you run the command:

        ```
        DemoStack deploy
        ```

    2.  Run the following command to delete the stack:

        ```
        ros-cdk destroy
        ```

        The following content is returned after you run the command:

        ```
        The following stack(s) will be destroyed(Only deployed stacks will be displayed).
        DemoStack
        Please confirm.( Y/N)
        Y
         ✅ Deleted
        RequestedId: 1BF864E1-7965-4148-A302-E6ABFF806641
        ```


## npm packages related to Alibaba Cloud resources

The following section lists the npm packages related to Alibaba Cloud resources. For example, `@alicloud/ros-cdk-ecs` indicates ECS resources. Each npm package contains all the resource types of a specific service supported by ROS.

You can log on to the [ROS console](http://ros.console.aliyun.com) and click **Resource Types** in the left-side navigation pane to view the resource types supported by all services.

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


# 安装ROS CDK

本文为您介绍如何安装ROS CDK。

请确保Node.js和TypeScript满足以下版本要求：

-   Node.js：10.23.0及以上。
-   TypeScript：2.7及以上。

## 在Linux平台安装ROS CDK

以下示例将在CentOS 8.2 64位的系统上安装ROS CDK。

1.  执行以下命令，安装Node.js、npm、tsc、lerna。

    ```
    # 由于ROS CDK使用TypeScript开发，因此需要安装相关软件包。
    yum install -y nodejs
    npm install typescript -g
    npm install lerna -g
    ```

2.  执行以下命令，安装CLI。

    ```
    npm install @alicloud/ros-cdk-cli -g
    ```

3.  执行以下命令，查看ROS CDK功能列表。

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


## 在Windows平台安装ROS CDK

以下示例将在Windows2016 64位的系统上安装ROS CDK。

1.  安装Node.js。

    1.  访问[Node.js官网](https://nodejs.org/en/download/)，下载Node.js安装包。

    2.  据界面提示，安装Node.js。

    3.  在cmd命令提示符窗口中执行以下命令，验证Node.js版本。

        ```
        C:\Users\Administrator>node --version
        v10.23.0
        ```

2.  执行以下命令，安装npm、tsc、lerna。

    ```
    # 由于ROS CDK使用TypeScript开发，因此需要安装相关软件包。
    C:\Users\Administrator>npm install typescript -g
    C:\Users\Administrator>npm install lerna -g
    ```

3.  执行以下命令，安装CLI。

    ```
    C:\Users\Administrator>npm install @alicloud/ros-cdk-cli -g
    ```

4.  执行以下命令，查看ROS CDK功能列表。

    ```
    C:\Users\Administrator>ros-cdk
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



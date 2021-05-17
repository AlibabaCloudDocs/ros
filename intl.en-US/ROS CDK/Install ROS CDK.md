# Install ROS CDK

This topic describes how to install ROS Cloud Development Toolkit \(CDK\).

Node.js and TypeScript are available in the following versions:

-   Node.js: 10.23.0 or later
-   TypeScript: 2.7 or later

## Install ROS CDK on Linux

In the following example, ROS CDK is installed on CentOS 8.2 64-bit.

1.  Run the following commands to install Node.js, npm, tsc, and Lerna:

    ```
    # ROS CDK is developed by using TypeScript, which requires you to install relevant packages in advance. 
    yum install -y nodejs
    npm install typescript -g
    npm install lerna -g
    ```

2.  Run the following command to install Alibaba Cloud CLI:

    ```
    npm install @alicloud/ros-cdk-cli -g
    ```

3.  Run the following command to query a list of operations that you can perform by using ROS CDK:

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


## Install ROS CDK on Windows

In the following example, ROS CDK is installed on Windows Server 2016 64-bit.

1.  Install Node.js.

    1.  Download the installation package from the [Node.js official website](https://nodejs.org/en/download/).

    2.  Install Node.js as prompted.

    3.  Run the following command in the command prompt window to verify the Node.js version:

        ```
        C:\Users\Administrator>node --version
        v10.23.0
        ```

2.  Run the following commands to install npm, tsc, and Lerna:

    ```
    # ROS CDK is developed by using TypeScript, which requires you to install relevant packages in advance. 
    C:\Users\Administrator>npm install typescript -g
    C:\Users\Administrator>npm install lerna -g
    ```

3.  Run the following commands to install Alibaba Cloud CLI:

    ```
    C:\Users\Administrator>npm install @alicloud/ros-cdk-cli -g
    ```

4.  Run the following command to query a list of operations that you can perform by using ROS CDK:

    ```
    C:\Users\Administrator>ros-cdk
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


## Install ROS CDK on macOS

In the following example, ROS CDK is installed on macOS Big Sur 11.2.2 64-bit.

1.  Run the following commands to install Homebrew, Node.js, npm, tsc, and Lerna:

    ```
    curl -LsSf http://github.com/mxcl/homebrew/tarball/master | sudo tar xvz -C/usr/local --strip 1
    brew install nodejs
    npm install typescript -g
    npm install lerna -g
    ```

2.  Run the following command to install Alibaba Cloud CLI:

    ```
    npm install @alicloud/ros-cdk-cli -g
    ```

3.  Run the following command to query a list of operations that you can perform by using ROS CDK:

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
                       STDOUT                                 [boolean] [default: false]
      --ignore-errors  Ignores synthesis errors, which will likely produce an
                       invalid output                         [boolean] [default: false]
      --trace          Print trace for stack warnings                      [boolean]
      --strict         Do not construct stacks with warnings               [boolean]
      --version        Show version number                                 [boolean]
      -h, --help       Show help                                           [boolean]
    
    If your app has a single stack, there is no need to specify the stack name
    
    If one of cdk.json or ~/.cdk.json exists, options specified there will be used
    as defaults. Settings in cdk.json take precedence.
    ```



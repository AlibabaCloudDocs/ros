# C\# example

This topic describes how to use ROS Cloud Development Toolkit \(CDK\) for C\#. In this example, a VPC is created.

The NET Core version is 3.1 or later, and the NET SDK version is 5.0 or later.

## Step 1: Initialize a project

Each ROS CDK application must be created within an independent project directory. The application uses the dependencies of the modules in the directory. Therefore, you must create a project directory and initialize the project before you create an application.

Run the following commands to create a project directory and initialize the project:

```
mkdir demo
cd demo
ros-cdk init --language=csharp --generate-only=true
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
├── cdk.json
├── global.sln
├── README.md
└── src
    ├── Demo
    │   ├── Demo.csproj
    │   ├── DemoStack.cs
    │   ├── GlobalSuppressions.cs
    │   └── Program.cs
    └── DemoTest
        ├── DemoTest.cs
        └── DemoTest.csproj

3 directories, 9 files
```

After the project is initialized, an application file named Program.cs and a definition file of the stack named DemoStack.cs are created. You can dynamically create stacks by using custom code in the DemoStack.cs file. The stack is added to the application. A project can contain only a single application. The following section describes the project structure:

-   `DemoStack.cs`: the definition file of the stack.

    The code generated when the stack is created only contains information about the stack. `DemoStack.cs` contains the following content:

    ```
    using AlibabaCloud.SDK.ROS.CDK.Core;
    
    namespace Demo
    {
        public class DemoStack : Stack
        {
            public DemoStack(Construct scope, string id, IStackProps props = null) : base(scope, id, props)
            {
                // The code that defines your stack goes here
            }
        }
    }
    ```

-   `Program.cs`: the application file.

    You can add stacks to the application. `Program.cs` contains the following content:

    ```
    using AlibabaCloud.SDK.ROS.CDK.Core;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    
    namespace Demo
    {
        sealed class Program
        {
            public static void Main(string[] args)
            {
                var app = new App();
                new DemoStack(app, "DemoStack");
                app.Synth();
            }
        }
    }
    ```

-   `DemoTest.cs`: the unit test file.

    The file is used to check whether the created stack follows the expected logic. `DemoTest.cs` contains the following content:

    ```
    using AlibabaCloud.SDK.ROS.CDK.Core;
    using NUnit.Framework;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    using Demo;
    
    namespace Stack.UnitTests.Services
    {
        [TestFixture]
        public class Stack_IsStackShould
        {
            [Test]
            public void DemoStack_IsStackShould()
            {
                var app = new App();
                var testStack = new DemoStack(app, "TestStack");
                var result = app.Synth().GetStackArtifact(testStack.ArtifactId).Template;
                var expectedJson = JsonConvert.SerializeObject(result);
                JObject obj = new JObject();
                obj.Add("ROSTemplateFormatVersion", "2015-09-01");
                var actual = JsonConvert.SerializeObject(obj);
                Assert.AreEqual(expectedJson, actual);
            }
        }
    }
    ```


## Step 4: Install dependencies

Modify the `Demo.csproj` file to add the ECS SDK dependency package.

```
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <!-- Roll forward to future major versions of the netcoreapp as needed -->
    <RollForward>Major</RollForward>
  </PropertyGroup>

  <ItemGroup>
    <!-- CDK Construct Library dependencies -->
    <PackageReference Include="AlibabaCloud.SDK.ROS.CDK.Core" Version="1.0.0" />
    <PackageReference Include="AlibabaCloud.SDK.ROS.CDK.Ecs" Version="1.0.0" />

    <!-- jsii Roslyn analyzers (un-comment to obtain compile-time checks for missing required props
    <PackageReference Include="Amazon.Jsii.Analyzers" Version="*" PrivateAssets="all" />
    -->

  </ItemGroup>

</Project>
```

## Step 5: Create resources

1.  Modify the `DemoStack.cs` file to create a VPC.

    ```
    using AlibabaCloud.SDK.ROS.CDK.Core;
    using AlibabaCloud.SDK.ROS.CDK.Ecs;
    
    namespace Demo
    {
        public class DemoStack : Stack
        {
            public DemoStack(Construct scope, string id, IStackProps props = null) : base(scope, id, props)
            {
                new Vpc(this, "vpc-from-ros-cdk", new VPCProps
                {
                    VpcName = "test-ros-cdk-csharp",
                    CidrBlock = "10.0.0.0/8",
                    Description = "This is ros cdk test"
                });
            }
        }
    }
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
        "vpc-from-ros-cdk": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "CidrBlock": "10.0.0.0/8",
            "Description": "This is ros cdk test",
            "EnableIpv6": false,
            "VpcName": "test-ros-cdk-csharp"
          }
        }
      }
    }
    ```


## Step 6: Perform a unit test

1.  Modify the `DemoTest.java` file to check whether a VPC can be created for the stack.

    ```
    using AlibabaCloud.SDK.ROS.CDK.Core;
    using NUnit.Framework;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    using Demo;
    
    namespace Stack.UnitTests.Services
    {
        [TestFixture]
        public class Stack_IsStackShould
        {
            [Test]
            public void DemoStack_IsStackShould()
            {
                var app = new App();
                var testStack = new DemoStack(app, "TestStack");
                var result = app.Synth().GetStackArtifact(testStack.ArtifactId).Template;
                var actualJson = JsonConvert.SerializeObject(result);
                JObject obj = new JObject();
                JObject Resources = new JObject();
                JObject VPC = new JObject();
                JObject Properties = new JObject();
                VPC.Add("Type", "ALIYUN::ECS::VPC");
                VPC.Add("Properties", Properties);
                Resources.Add("vpc-from-ros-cdk", VPC);
                Properties.Add("CidrBlock", "10.0.0.0/8");
                Properties.Add("Description", "This is ros cdk test");
                Properties.Add("EnableIpv6", false);
                Properties.Add("VpcName", "test-ros-cdk-csharp");
                obj.Add("ROSTemplateFormatVersion", "2015-09-01");
                obj.Add("Resources", Resources);
                var expected = JsonConvert.SerializeObject(obj);
                Assert.AreEqual(actualJson, expected);
            }
        }
    }
    ```

2.  Run the following command to perform a unit test:

    ```
    dotnet test
    ```

    The following content is returned after you run the command:

    ```
    Test run for /home/demo/src/DemoTest/bin/Debug/netcoreapp3.1/DemoTest.dll(.NETCoreApp,Version=v3.1)
    Microsoft (R) Test Execution Command Line Tool Version 16.7.1
    Copyright (c) Microsoft Corporation.  All rights reserved.
    
    Starting test execution, please wait...
    
    A total of 1 test files matched the specified pattern.
    
    Test Run Successful.
    Total tests: 1
         Passed: 1
     Total time: 2.6478 Seconds
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
     ✅ The deployment(create stack) has completed!
    RequestedId: FDFF3996-6CBC-48F9-A217-5FAEGXFE8
    StackId: 9c62f0f2-af85-4536-987a-154eg****
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
                    "CreateTime": "2021-02-19T03:30:30",
                    "RegionId": "cn-beijing",
                    "DisableRollback": false,
                    "StackName": "DemoStack",
                    "Tags": [],
                    "StackId": "9c62f0f2-af85-4536-987a-dgd2****",
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



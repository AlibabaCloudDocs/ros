# C\#示例

本文以创建一个阿里云专有网络（VPC）实例为例，为您介绍如何在C\#语言环境使用ROS CDK。

请确保.NET Core版本在3.1及以上，并且.NET SDK版本在5.0及以上。

## 步骤一：初始化工程

每个ROS CDK应用都要求创建在一个独立的工程目录下，且该应用需要使用独立工程目录中模块的依赖项。所以在创建应用之前，需要先创建一个工程目录并进行初始化。

执行以下命令，创建工程目录并初始化工程。

```
mkdir demo
cd demo
ros-cdk init --language=csharp --generate-only=true
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

## 步骤三：预览工程结构

执行以下命令，预览工程结构。

```
tree .
```

执行命令后，输出以下内容：

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

初始化工程之后默认会定义一个应用文件（Program.cs），与一个资源栈文件（DemoStack.cs）。您可以在DemoStack.cs中通过自定义代码的方式动态构建资源栈。资源栈将被默认添加到应用中，每个工程只允许存在一个应用。工程结构说明如下：

-   `DemoStack.cs`：资源栈文件。

    初始化生成的代码中，只为资源栈添加了描述信息。`DemoStack.cs`文件内容如下：

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

-   `Program.cs`：应用文件。

    您可以将资源栈添加到应用中。`Program.cs`文件内容如下：

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

-   `DemoTest.cs`：单元测试文件。

    用于验证构建资源栈的逻辑是否符合预期。`DemoTest.cs`文件内容如下：

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


## 步骤四：安装依赖

修改`Demo.csproj`文件，添加ECS依赖包。

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

## 步骤五：创建资源

1.  修改`DemoStack.cs`文件，添加VPC。

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

2.  执行以下命令，生成模板文件。

    ```
    ros-cdk synth --json
    ```

    执行命令后，输出以下内容：

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


## 步骤六：单元测试

1.  修改`DemoTest.cs`文件，验证资源栈创建VPC的可行性。

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

2.  执行以下命令，进行单元测试。

    ```
    dotnet test
    ```

    执行命令后，输出以下内容：

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


## 步骤七：管理资源栈

您可以使用ROS CDK命令，创建、查询或删除资源栈。

-   创建资源栈

    执行以下命令，创建资源栈。

    ```
    ros-cdk deploy
    ```

    执行命令后，输出以下内容：

    ```
     ✅ The deployment(create stack) has completed!
    RequestedId: FDFF3996-6CBC-48F9-A217-5FAEGXFE8
    StackId: 9c62f0f2-af85-4536-987a-154eg****
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



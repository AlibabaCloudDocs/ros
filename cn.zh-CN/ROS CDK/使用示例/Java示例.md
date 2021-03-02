# Java示例

本文以创建一个阿里云专有网络（VPC）实例为例，为您介绍如何在Java语言环境使用ROS CDK。

请确保JDK和Maven满足以下版本要求：

-   JDK：8及以上。
-   Maven：3.6及以上。

## 步骤一：初始化工程

每个ROS CDK应用都要求创建在一个独立的工程目录下，且该应用需要使用独立工程目录中模块的依赖项。所以在创建应用之前，需要先创建一个工程目录并进行初始化。

执行以下命令，创建工程目录并初始化工程。

```
mkdir demo
cd demo
ros-cdk init --language=java --generate-only=true
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
├── cdk.json
├── pom.xml
├── README.md
└── src
    ├── main
    │   └── java
    │       └── com
    │           └── myorg
    │               ├── DemoApp.java
    │               └── DemoStack.java
    └── test
        └── java
            └── com
                └── myorg
                    └── DemoTest.java

9 directories, 6 files
```

工程结构说明如下：

-   `DemoApp.java`：入口文件。

    **说明：** 一个工程有且仅有一个应用。

    示例中创建了一个应用（类型为App）和一个资源栈（类型为DemoStack，名称为DemoStack），并将资源栈添加到应用中。`DemoApp.java`文件内容如下：

    ```
    package com.myorg;
    
    import com.aliyun.ros.cdk.core.*;
    
    import java.util.Arrays;
    
    public class DemoApp {
        public static void main(final String[] args) {
            App app = new App();
    
            new DemoStack(app, "DemoStack");
    
            app.synth();
        }
    }
    ```

-   `DemoStack.java`：资源栈的定义文件。

    您可以将资源添加到资源栈中，动态构建资源栈。初始化生成的代码中，只为资源栈添加了描述信息。`DemoStack.java`文件内容如下：

    ```
    package com.myorg;
    
    import com.aliyun.ros.cdk.core.*;
    
    public class DemoStack extends Stack {
        public DemoStack(final Construct scope, final String id) {
            this(scope, id, null);
        }
    
        public DemoStack(final Construct scope, final String id, final StackProps props) {
            super(scope, id, props);
    
            // The code that defines your stack goes here
        }
    }
    ```

-   `DemoTest.java`：单元测试文件。

    用于验证构建资源栈的逻辑是否符合预期。`DemoTest.java`文件内容如下：

    ```
    package com.myorg;
    
    import com.aliyun.ros.cdk.core.*;
    import com.fasterxml.jackson.databind.JsonNode;
    import com.fasterxml.jackson.databind.ObjectMapper;
    import com.fasterxml.jackson.databind.SerializationFeature;
    import com.fasterxml.jackson.databind.node.ObjectNode;
    import org.junit.Test;
    
    import java.io.IOException;
    
    import static org.junit.Assert.assertEquals;
    
    public class DemoTest {
        private final static ObjectMapper JSON =
            new ObjectMapper().configure(SerializationFeature.INDENT_OUTPUT, true);
    
        @Test
        public void testStack() throws IOException {
            App app = new App();
            DemoStack stack = new DemoStack(app, "test");
    
            // synthesize the stack to a ROS template and compare against
            // a checked-in JSON file.
            JsonNode actual = JSON.valueToTree(app.synth().getStackArtifact(stack.getArtifactId()).getTemplate());
            ObjectNode expected = new ObjectMapper().createObjectNode();
            expected.put("ROSTemplateFormatVersion", "2015-09-01");
            assertEquals(expected, actual);
        }
    }
    ```


## 步骤四：安装依赖

1.  修改`pom.xml`文件，添加ECS SDK依赖包。

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
             xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <modelVersion>4.0.0</modelVersion>
    
        <groupId>com.myorg</groupId>
        <artifactId>java_demo</artifactId>
        <version>0.1</version>
    
        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <cdk.version>1.0.3</cdk.version>
        </properties>
    
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.8.1</version>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                    </configuration>
                </plugin>
    
                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>exec-maven-plugin</artifactId>
                    <version>1.6.0</version>
                    <configuration>
                        <mainClass>com.myorg.DemoApp</mainClass>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    
        <dependencies>
            <!-- AliCloud ROS Cloud Development Kit (ROS CDK) -->
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>ros-cdk-core</artifactId>
                <version>1.0.0</version>
            </dependency>
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>ros-cdk-ecs</artifactId>
                <version>1.0.0</version>
            </dependency>
    
            <!-- https://mvnrepository.com/artifact/junit/junit -->
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.12</version>
                <scope>test</scope>
            </dependency>
        </dependencies>
    </project>
    ```

2.  执行以下命令，安装依赖。

    ```
    mvn compile
    ```


## 步骤五：创建资源

1.  修改`DemoStack.java`文件，创建VPC。

    ```
    package com.myorg;
    
    import com.aliyun.ros.cdk.core.*;
    import com.aliyun.ros.cdk.ecs.*;
    
    public class DemoStack extends Stack {
        public DemoStack(final Construct scope, final String id) {
            this(scope, id, null);
        }
    
        public DemoStack(final Construct scope, final String id, final StackProps props) {
            super(scope, id, props);
    
            // The code that defines your stack goes here
    
            Vpc.Builder.create(this, "VPC").vpcName("TestJavaCDK").description("This is ros java cdk test").
                    cidrBlock("10.0.0.0/8").build();
        }
    }
    ```

2.  执行以下命令，生成模板文件。

    ```
    mvn compile
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
            "Description": "This is ros java cdk test",
            "EnableIpv6": false,
            "VpcName": "TestJavaCDK"
          }
        }
      }
    }
    ```


## 步骤六：单元测试

1.  修改`DemoTest.java`文件，验证资源栈创建VPC的可行性。

    ```
    package com.myorg;
    
    import com.aliyun.ros.cdk.core.*;
    import com.fasterxml.jackson.databind.JsonNode;
    import com.fasterxml.jackson.databind.ObjectMapper;
    import com.fasterxml.jackson.databind.SerializationFeature;
    import com.fasterxml.jackson.databind.node.ObjectNode;
    import org.junit.Test;
    
    import java.io.IOException;
    
    import static org.junit.Assert.assertEquals;
    
    public class DemoTest {
        private final static ObjectMapper JSON =
            new ObjectMapper().configure(SerializationFeature.INDENT_OUTPUT, true);
    
        @Test
        public void testStack() throws IOException {
            App app = new App();
            DemoStack stack = new DemoStack(app, "test");
    
            // synthesize the stack to a ROS template and compare against
            // a checked-in JSON file.
            JsonNode actual = JSON.valueToTree(app.synth().getStackArtifact(stack.getArtifactId()).getTemplate());
            ObjectNode expected = new ObjectMapper().createObjectNode();
            ObjectNode Properties = new ObjectMapper().createObjectNode();
            ObjectNode Resources = new ObjectMapper().createObjectNode();
            ObjectNode VPC = new ObjectMapper().createObjectNode();
            VPC.put("Type","ALIYUN::ECS::VPC");
            VPC.put("Properties",Properties);
            Resources.put("VPC",VPC);
            Properties.put("CidrBlock","10.0.0.0/8");
            Properties.put("Description","This is ros java cdk test");
            Properties.put("EnableIpv6",false);
            Properties.put("VpcName","TestJavaCDK");
            expected.put("ROSTemplateFormatVersion", "2015-09-01");
            expected.put("Resources", Resources);
            assertEquals(expected, actual);
        }
    }
    ```

2.  执行以下命令，进行单元测试。

    ```
    npm test
    ```

    执行命令后，输出以下内容：

    ```
    -------------------------------------------------------
     T E S T S
    -------------------------------------------------------
    Running com.myorg.DemoTest
    Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 1.294 sec
    
    Results :
    
    Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
    
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time:  9.158 s
    [INFO] Finished at: 2021-01-28T20:00:59+08:00
    [INFO] ------------------------------------------------------------------------
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
                    "StackName": "DemoStack",
                    "Tags": [],
                    "StackId": "218f0db0-7992-4e70-a586-15e****",
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



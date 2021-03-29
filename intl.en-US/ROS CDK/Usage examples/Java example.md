# Java example

This topic describes how to use ROS Cloud Development Toolkit \(CDK\) for Java. In this example, a VPC is created.

JDK and Maven are available in the following versions:

-   JDK: 8 or later
-   Maven: 3.6 or later

## Step 1: Initialize a project

Each ROS CDK application must be created within an independent project directory. The application uses the dependencies of the modules in the directory. Therefore, you must create a project directory and initialize the project before you create an application.

Run the following commands to create a project directory and initialize the project:

```
mkdir demo
cd demo
ros-cdk init --language=java --generate-only=true
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

The following section describes the project structure:

-   `DemoApp.java`: the launch file of the project.

    **Note:** A project can contain only a single application.

    In the example, an application of the App type and a DemoStack-typed stack named DemoStack are created. The stack is added to the application. The `DemoApp.java` file contains the following content:

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

-   `DemoStack.java`: the definition file of the stack.

    You can add resources to the stack to dynamically create the stack. The code generated when the stack is created only contains information about the stack. `DemoStack.java` contains the following content:

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

-   `DemoTest.java`: the unit test file.

    The file is used to check whether the created stack follows the expected logic. `DemoTest.java` contains the following content:

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


## Step 4: Install dependencies

1.  Modify the `pom.xml` file to add the ECS SDK dependency package.

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

2.  Run the following command to install the dependency package:

    ```
    mvn compile
    ```


## Step 5: Create resources

1.  Modify the `DemoStack.java` file to create a VPC.

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

2.  Run the following command to generate a template file:

    ```
    mvn compile
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
            "Description": "This is ros java cdk test",
            "EnableIpv6": false,
            "VpcName": "TestJavaCDK"
          }
        }
      }
    }
    ```


## Step 6: Perform a unit test

1.  Modify the `DemoTest.java` file to check whether a VPC can be created for the stack.

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

2.  Run the following command to perform a unit test:

    ```
    npm test
    ```

    The following content is returned after you run the command:

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
                    "StackName": "DemoStack",
                    "Tags": [],
                    "StackId": "218f0db0-7992-4e70-a586-15e****",
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



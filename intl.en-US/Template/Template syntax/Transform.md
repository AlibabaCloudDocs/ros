# Transform

Transform makes it easy to author templates in specific scenarios. You can specify the Transform section to use this feature. Resource Orchestration Service \(ROS\) transforms a template that has the Transform section specified to a standard template and then performs operations such as creating and updating resources.

ROS supports transformation of the Aliyun::Serverless resources in serverless scenarios based on Alibaba Cloud Function Compute. For more information, see [Serverless architecture]().

ROS transforms a template written in the Serverless Application Model \(SAM\) syntax based on Funcraft to a standard ROS template.

For more information, see [t1881164.md\#]() and visit [Serverless Application Model](https://github.com/alibaba/funcraft/blob/master/docs/specs/2018-04-03.md).

## Supported resource types

-   [Aliyun::Serverless::Api](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::Api.md)
-   [Aliyun::Serverless::CustomDomain](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::CustomDomain.md)
-   [Aliyun::Serverless::Function](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::Function.md)
-   [Aliyun::Serverless::Log](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::Log.md)
-   [Aliyun::Serverless::Log::Logstore](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::Log::Logstore.md)
-   [Aliyun::Serverless::MNSTopic](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::MNSTopic.md)
-   [Aliyun::Serverless::Service](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::Service.md)
-   [Aliyun::Serverless::TableStore](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::TableStore.md)
-   [Aliyun::Serverless::TableStore::Table](/intl.en-US/Resource Types/Transform/Aliyun::Serverless::TableStore::Table.md)

## Syntax

The declaration in the Transform section must be a String-type value and cannot be a parameter or function.

`JSON` example

```
"Transform" : "Aliyun::Serverless-2018-04-03"
```

`YAML` example

```
Transform: Aliyun::Serverless-2018-04-03
```

## Examples

The following template is written in the SAM syntax:

```
ROSTemplateFormatVersion: "2015-09-01"
Transform: "Aliyun::Serverless-2018-04-03"
Resources:
  MyService: # service name
    Type: "Aliyun::Serverless::Service"
    Properties:
      Policies:
        - AliyunFCReadOnlyAccess # Managed Policy
        - Version: "1" # Policy Document
          Statement:
            - Effect: Allow
              Action:
                - oss:GetObject
                - oss:GetObjectACL
              Resource: "*"
    MyFunction: # function name
      Type: "Aliyun::Serverless::Function"
      Properties:
        Handler: index.handler
        Runtime: nodejs6
        CodeUri: "oss://testBucket/myCode.zip"
```

When the template is used to create change sets or stacks, ROS transforms the template based on the SAM syntax. The following changes occur in the transformed template:

-   Aliyun::Serverless::Service is transformed to ALIYUN::FC::Service.
-   The value of the Policies parameter specified in Aliyun::Serverless::Service is transformed to ALIYUN::RAM::Role and ALIYUN::RAM::AttachPolicyToRole, and the policies are specified in the Role parameter of ALIYUN::FC::Service.
-   Aliyun::Serverless::Function is transformed to ALIYUN::FC::Function.

The following template is available after the transformation:

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MyServiceRole": {
      "Type": "ALIYUN::RAM::Role",
      "Properties": {
        "RoleName": "test-MyServiceRole-7840BA19B01C",
        "Description": "Function Compute default role",
        "Policies": [
          {
            "PolicyName": "test-MyServiceRole-7840BA19B01CPolicy1",
            "PolicyDocument": {
              "Version": "1",
              "Statement": [
                {
                  "Action": ["oss:GetObject", "oss:GetObjectACL"],
                  "Resource": ["*"],
                  "Effect": "Allow"
                }
              ]
            }
          }
        ],
        "AssumeRolePolicyDocument": {
          "Version": "1",
          "Statement": [
            {
              "Action": "sts:AssumeRole",
              "Effect": "Allow",
              "Principal": {
                "Service": ["fc.aliyuncs.com"]
              }
            }
          ]
        }
      }
    },
    "AliyunFCReadOnlyAccessMyServiceRole": {
      "Type": "ALIYUN::RAM::AttachPolicyToRole",
      "Properties": {
        "PolicyName": "AliyunFCReadOnlyAccess",
        "PolicyType": "System",
        "RoleName": {
          "Fn::GetAtt": ["MyServiceRole", "RoleName"]
        }
      },
      "DependsOn": "MyServiceRole"
    },
    "MyService": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "ServiceName": "test-MyService-E522E1B83D81",
        "Role": {
          "Fn::GetAtt": ["MyServiceRole", "Arn"]
        },
        "LogConfig": {
          "Project": "",
          "Logstore": ""
        },
        "InternetAccess": true
      },
      "DependsOn": ["MyServiceRole", "AliyunFCReadOnlyAccessMyServiceRole"]
    },
    "MyServiceMyFunction": {
      "Type": "ALIYUN::FC::Function",
      "Properties": {
        "Code": {
          "OssBucketName": "testBucket",
          "OssObjectName": "myCode.zip"
        },
        "FunctionName": "MyFunction",
        "ServiceName": "test-MyService-E522E1B83D81",
        "EnvironmentVariables": {
          "PATH": "/code/.fun/root/usr/local/bin:/code/.fun/root/usr/local/sbin:/code/.fun/root/usr/bin:/code/.fun/root/usr/sbin:/code/.fun/root/sbin:/code/.fun/root/bin:/code/.fun/python/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/sbin:/bin",
          "LD_LIBRARY_PATH": "/code/.fun/root/usr/lib:/code/.fun/root/usr/lib/x86_64-linux-gnu:/code/.fun/root/lib/x86_64-linux-gnu:/code/.fun/root/usr/lib64:/code:/code/lib:/usr/local/lib",
          "PYTHONUSERBASE": "/code/.fun/python"
        },
        "Handler": "index.handler",
        "Runtime": "nodejs6"
      },
      "DependsOn": ["MyService"]
    }
  }
}
```


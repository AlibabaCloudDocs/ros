# 转换（Transform）

转换用于简化特定场景的模板编写复杂度，可通过在模板中指定Transform进行声明。ROS会将含有Transform的模板转换为普通模板，然后进行资源的创建、更新等操作。

ROS支持Aliyun::Serverless转换，可用于基于函数计算服务的无服务器（Serverless）场景。更多信息，请参见[无服务器架构]()。

Aliyun::Serverless转换会将使用SAM（Serverless Application Model）语法编写的模板（基于阿里云Funcraft工具），转换为ROS的普通模板。

更多信息，请参见[SAM（Serverless Application Model）语法](https://github.com/alibaba/funcraft/blob/master/docs/specs/2018-04-03.md)。

## 支持的资源类型

-   [Aliyun::Serverless::Api](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::Api.md)
-   [Aliyun::Serverless::CustomDomain](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::CustomDomain.md)
-   [Aliyun::Serverless::Function](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::Function.md)
-   [Aliyun::Serverless::Log](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::Log.md)
-   [Aliyun::Serverless::Log::Logstore](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::Log::Logstore.md)
-   [Aliyun::Serverless::MNSTopic](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::MNSTopic.md)
-   [Aliyun::Serverless::Service](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::Service.md)
-   [Aliyun::Serverless::TableStore](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::TableStore.md)
-   [Aliyun::Serverless::TableStore::Table](/intl.zh-CN/资源类型/Transform/Aliyun::Serverless::TableStore::Table.md)

## 语法

转换声明的值必须为字符串，不能使用参数或函数来指定转换值。

`JSON`示例

```
"Transform" : "Aliyun::Serverless-2018-04-03"
```

`YAML`示例

```
Transform: Aliyun::Serverless-2018-04-03
```

## 示例

以下是一个使用阿里云SAM语法编写的模板：

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

使用模板创建更改集或者资源栈时，ROS会展开SAM语法。上述模板将会转换以下内容：

-   将Aliyun::Serverless::Service资源转换为ALIYUN::FC::Service资源。
-   将Aliyun::Serverless::Service资源中定义的Policies转换为ALIYUN::RAM::Role和ALIYUN::RAM::AttachPolicyToRole资源，并指定在 ALIYUN::FC::Service的Role参数中。
-   将Aliyun::Serverless::Function资源转换为ALIYUN::FC::Function资源。

转换后的ROS模板如下：

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


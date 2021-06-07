# Create a RAM user and grant permissions to the RAM user

This topic describes how to create a Resource Access Management \(RAM\) user for Resource Orchestration Service \(ROS\) and grant permissions to the RAM user when you create a stack in the ROS console.

You must perform multiple operations when you create a RAM user and grant permissions to the RAM user in the RAM console. To improve efficiency, you can complete the operations in the ROS console. For more information about RAM users, see [Overview of a RAM user](/intl.en-US/RAM User Management/Overview of a RAM user.md).

## Step 1: Edit a template

The following sample code shows how to create a RAM user, a custom permission policy, and an AccessKey pair, and how to grant permissions to the RAM user.

For more information about resource types, see [List of resource types by service](/intl.en-US/Resource Types/List of resource types by service.md).

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "UserName": {
      "Type": "String",
      "Description": "RAM User Name",
      "Label": {
        "en": "RAM User Name"
      }
    },
    "PolicyName": {
      "Type": "String",
      "Description": "RAM Policy Name",
      "Label": {
        "en": "RAM Policy Name"
      }
    },
    "Action": {
      "Default": [
        "vpc:*"
      ],
      "Type": "Json",
      "Description": {
        "en": "The operation of products and services defined by the strategy, Resources for operations, refer to <a href='https://www.alibabacloud.com/help/doc-detail/93738.htm'>Policy elements</a> for more info."
      },
      "Label": {
        "en": "PolicyAction"
      }
    },
    "Effect": {
      "Default": "Allow",
      "AllowedValues": [
        "Allow",
        "Deny"
      ],
      "Type": "String",
      "Description": {
        "en": "Allow/Deny Action for Resource"
      },
      "Label": {
        "en": "Authority"
      }
    },
    "Resource": {
      "Default": [
        "*"
      ],
      "Type": "Json",
      "Description": {
        "en": "Resources for operations, refer to <a href='https://www.alibabacloud.com/help/doc-detail/93738.htm'>Policy elements</a> for more info."
      },
      "Label": {
        "en": "Resource"
      }
    }
  },
  "Resources": {
    "ManagedPolicy": {
      "Type": "ALIYUN::RAM::ManagedPolicy",
      "Properties": {
        "PolicyName": {
          "Ref": "PolicyName"
        },
        "PolicyDocument": {
          "Version": "1",
          "Statement": [
            {
              "Action": {
                "Ref": "Action"
              },
              "Resource": {
                "Ref": "Resource"
              },
              "Effect": {
                "Ref": "Effect"
              }
            }
          ]
        }
      }
    },
    "RamAK": {
      "Type": "ALIYUN::RAM::AccessKey",
      "Properties": {
        "UserName": {
          "Fn::GetAtt": [
            "RamUser",
            "UserName"
          ]
        }
      },
      "DependsOn": "RamUser"
    },
    "RamUser": {
      "Type": "ALIYUN::RAM::User",
      "Properties": {
        "UserName": {
          "Ref": "UserName"
        }
      }
    },
    "AttachPolicyToUser": {
      "DependsOn": [
        "ManagedPolicy",
        "RamUser"
      ],
      "Type": "ALIYUN::RAM::AttachPolicyToUser",
      "Properties": {
        "PolicyType": "Custom",
        "UserName": {
          "Fn::GetAtt": [
            "RamUser",
            "UserName"
          ]
        },
        "PolicyName": {
          "Fn::GetAtt": [
            "ManagedPolicy",
            "PolicyName"
          ]
        }
      }
    }
  },
  "Outputs": {
    "AKSecret": {
      "Value": {
        "Fn::GetAtt": [
          "RamAK",
          "AccessKeySecret"
        ]
      }
    },
    "AKId": {
      "Value": {
        "Fn::GetAtt": [
          "RamAK",
          "AccessKeyId"
        ]
      }
    },
    "UserId": {
      "Value": {
        "Fn::GetAtt": [
          "RamUser",
          "UserId"
        ]
      }
    }
  }
}            
```

## Step 2: Create a stack

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner of the page, select the region where you want to create the stack from the drop-down list.

4.  On the Stacks page, click **Create Stack** and select **Use New Resources \(Standard\)** from the drop-down list.

5.  In the Select Template step, select Select an Existing Template. Set **Template Import Method** to **Enter Template Content**, enter the template content you edited in [Step 1](#section_yfz_i16_y63) into the Template Content code editor, and then click **Next**.

6.  In the Configure Template Parameters step, set **Stack Name** and the following parameters.

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |**RAM User Name**|The name of the RAM user. For more information, see [Overview of a RAM user](/intl.en-US/RAM User Management/Overview of a RAM user.md).

|vpc-dev|
    |**RAM Policy Name**|The name of the permission policy. For more information, see [Policy overview](/intl.en-US/Policy Management/Policy overview.md).

|vpcDevPolicy|
    |**PolicyAction**|The operation to be performed on a specific resource by the permission policy. For more information, see [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md).

|\["vpc:\*"\]|
    |**Authority**|The authorization effect of the permission policy. Valid values:    -   Allow
    -   Deny
For more information, see [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md).

|Allow|
    |**Resource**|The object to which the permission policy is granted. For more information, see [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md).

|\["\*"\]|

7.  Click **Create**.

    After the stack is created, you can log on to the [RAM console](https://ram.console.aliyun.com/) to view the RAM user, custom permission policy, AccessKey pair, and permissions of the RAM user.



# Move a resource between stacks

This topic describes how to move a resource from one stack to another. An Elastic IP Address \(EIP\) resource is used in the example.

In this example, an EIP resource named EIP2 is moved from Stack A to Stack B.

1.  Remove EIP2 from Stack A.

    For more information, see [Remove a resource from a stack](/intl.en-US/Resource import/Remove a resource from a stack.md).

    Before you remove EIP2, it is contained in the template of Stack A. The following code shows a sample template before EIP2 is removed from Stack A:

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "Eip": {
          "Type": "ALIYUN::VPC::EIP",
          "Properties": {
            "Bandwidth": 5
          }
        },
        "Eip2": {
          "Type": "ALIYUN::VPC::EIP",
          "DeletionPolicy": "Retain",
          "Properties": {
            "Bandwidth": 5
          }
        }
      },
      "Outputs": {
        "EipAddress": {
          "Value": {
            "Fn::GetAtt": [
              "Eip",
              "EipAddress"
            ]
          }
        },
        "AllocationId": {
          "Value": {
            "Fn::GetAtt": [
              "Eip",
              "AllocationId"
            ]
          }
        },
        "EipAddress2": {
          "Value": {
            "Fn::GetAtt": [
              "Eip2",
              "EipAddress"
            ]
          }
        },
        "AllocationId2": {
          "Value": {
            "Fn::GetAtt": [
              "Eip2",
              "AllocationId"
            ]
          }
        }
      }
    }
    ```

    **Note:** The `DeletionPolicy` parameter is set to `Retain`, which indicates that the resource is retained when it is removed from a stack. To prevent resources from being unexpectedly deleted, we recommend that you set the DeletionPolicy parameter to Retain.

    After you remove EIP2, it is no longer contained in the template of Stack A. The following code shows a sample template after EIP2 is removed from Stack A:

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "Eip": {
          "Type": "ALIYUN::VPC::EIP",
          "Properties": {
            "Bandwidth": 5
          }
        }
      },
      "Outputs": {
        "EipAddress": {
          "Value": {
            "Fn::GetAtt": [
              "Eip",
              "EipAddress"
            ]
          }
        },
        "AllocationId": {
          "Value": {
            "Fn::GetAtt": [
              "Eip",
              "AllocationId"
            ]
          }
        }
      }
    }
    ```

2.  Import EIP2 to Stack B.

    For more information, see [Import an existing resource to a stack](/intl.en-US/Resource import/Import an existing resource to a stack.md).

    Before you import EIP2, it is not contained in the template of Stack B. The following code shows a sample template before EIP2 is imported to Stack B:

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01"
    }
    ```

    After you import EIP2, it is contained in the template of Stack B. The following code shows a sample template after EIP2 is imported to Stack B:

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "Eip2": {
          "Type": "ALIYUN::VPC::EIP",
          "DeletionPolicy": "Retain",
          "Properties": {
            "Bandwidth": 5
          }
        }
      },
      "Outputs": {
        "EipAddress2": {
          "Value": {
            "Fn::GetAtt": [
              "Eip2",
              "EipAddress"
            ]
          }
        },
        "AllocationId2": {
          "Value": {
            "Fn::GetAtt": [
              "Eip2",
              "AllocationId"
            ]
          }
        }
      }
    }
    ```


After the preceding operations, EIP2 is moved from Stack A to Stack B. You can view information about the imported EIP2 resource on the **Resources** tab of the stack management page of Stack B.


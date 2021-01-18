# Obtain a resource identifier property for resource import

When you import a resource, you must provide its resource identifier property. This topic describes how to obtain a resource identifier property by calling the GetResourceTypeTemplate and GetTemplateSummary operations. ALIYUN::VPC::EIP is used in the example.

1.  Log on to [OpenAPI Explorer](https://api.alibabacloud.com/#/?product=ROS).

2.  Call the GetResourceTypeTemplate operation to query the template body of ALIYUN::VPC::EIP. For more information, see [GetResourceTypeTemplate](/intl.en-US/API Reference/Resource operations/GetResourceTypeTemplate.md).

    1.  Search for the GetResourceTypeTemplate operation.

    2.  Set **ResourceType** to ALIYUN::VPC::EIP and click **Submit Request**.

        **Note:** For more information about resource types, see [Resource type index](/intl.en-US/Resource Types/Resource type index.md).

        The following result is returned:

        ```
        {
         "RequestId": "4EE61317-00F7-4DB6-9FBD-E12ECC79805A",
         "TemplateBody": {
          "Parameters": {
           "Description": {
            "Type": "String",
            "Description": "Optional. The description of the EIP. The description must be 2 to 256 characters in length. It must start with a letter. It cannot start with http://  or https://."
           },
           "ResourceGroupId": {
            "Type": "String",
            "Description": "Resource group id."
           },
           "InstanceChargeType": {
            "Type": "String",
            "Description": "The resource charge type. Default value is Postpaid",
            "AllowedValues": [
             "Prepaid",
             "Postpaid"
            ],
            "Default": "Postpaid"
           },
           "PricingCycle": {
            "Type": "String",
            "Description": "Price cycle of the resource. This property has no default value. If ChargeType is specified as Postpaid, this value will be ignore.",
            "AllowedValues": [
             "Month",
             "Year"
            ],
            "Default": "Month"
           },
           "Isp": {
            "Type": "String",
            "Description": "ISP tag for finance cloud region. only for cn-hangzhou and cn-qingdao region), if you are not finance cloud user, this value will be ignore."
           },
           "Period": {
            "Type": "Number",
            "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
            "MinValue": 1,
            "MaxValue": 9,
            "Default": 1
           },
           "DeletionProtection": {
            "Type": "Boolean",
            "Description": "Whether to enable deletion protection.\nDefault to False.",
            "AllowedValues": [
             "True",
             "true",
             "False",
             "false"
            ],
            "Default": false
           },
           "AutoPay": {
            "Type": "Boolean",
            "Description": "Automatic Payment. Default is false.",
            "AllowedValues": [
             "True",
             "true",
             "False",
             "false"
            ],
            "Default": false
           },
           "Name": {
            "Type": "String",
            "Description": "The name of the EIP. The name must be 2 to 128 characters in length. It must start with a letter. It can contain numbers, periods (.), underscores (_), and hyphens (-). It cannot start with http://  or https://"
           },
           "InternetChargeType": {
            "Type": "String",
            "Description": "The network charge type. Support 'PayByBandwidth' and 'PayByTraffic' only. Default is PayByBandwidth. PayByTraffic will charge by hour, PayByBandwidth will charge by day. ",
            "AllowedValues": [
             "PayByBandwidth",
             "PayByTraffic"
            ],
            "Default": "PayByBandwidth"
           },
           "Netmode": {
            "Type": "String",
            "Description": "The network type. Valid value: public (public network)."
           },
           "Bandwidth": {
            "Type": "Number",
            "Description": "Bandwidth for the output network. Default is 5MB.",
            "Default": 5
           },
           "Tags": {
            "Type": "Json",
            "Description": "Tags to attach to eip. Max support 20 tags to add during create eip. Each tag with two properties Key and Value, and Key is required.",
            "MaxLength": 20
           }
          },
          "ROSTemplateFormatVersion": "2015-09-01",
          "Outputs": {
           "AllocationId": {
            "Description": "ID that Aliyun assigns to represent the allocation of the address for use with VPC. Returned only for VPC elastic IP addresses.",
            "Value": {
             "Fn::GetAtt": [
              "ElasticIp",
              "AllocationId"
             ]
            }
           },
           "EipAddress": {
            "Description": "IP address of created EIP.",
            "Value": {
             "Fn::GetAtt": [
              "ElasticIp",
              "EipAddress"
             ]
            }
           },
           "OrderId": {
            "Description": "Order ID of prepaid EIP instance.",
            "Value": {
             "Fn::GetAtt": [
              "ElasticIp",
              "OrderId"
             ]
            }
           }
          },
          "Resources": {
           "ElasticIp": {
            "Type": "ALIYUN::VPC::EIP",
            "Properties": {
             "Description": {
              "Ref": "Description"
             },
             "ResourceGroupId": {
              "Ref": "ResourceGroupId"
             },
             "InstanceChargeType": {
              "Ref": "InstanceChargeType"
             },
             "PricingCycle": {
              "Ref": "PricingCycle"
             },
             "Isp": {
              "Ref": "Isp"
             },
             "Period": {
              "Ref": "Period"
             },
             "DeletionProtection": {
              "Ref": "DeletionProtection"
             },
             "AutoPay": {
              "Ref": "AutoPay"
             },
             "Name": {
              "Ref": "Name"
             },
             "InternetChargeType": {
              "Ref": "InternetChargeType"
             },
             "Netmode": {
              "Ref": "Netmode"
             },
             "Bandwidth": {
              "Ref": "Bandwidth"
             },
             "Tags": {
              "Ref": "Tags"
             }
            }
           }
          }
         }
        }
        ```

3.  Call the GetTemplateSummary operation to query the template information that contains the resource identifier. For more information, see [GetTemplateSummary](/intl.en-US/API Reference/Template operations/GetTemplateSummary.md).

    1.  Search for the GetTemplateSummary operation.

    2.  Specify the **RegionId** parameter, set **TemplateBody** to the template body of ALIYUN::VPC::EIP that is returned in Step 2, and then click **Submit Request**.

        The following result is returned:

        ```
        {
         "ResourceTypes": [
          "ALIYUN::VPC::EIP"
         ],
         "Description": "No description",
         "Parameters": [
          {
           "NoEcho": "false",
           "Type": "Boolean",
           "Description": "Whether to enable deletion protection.\nDefault to False.",
           "AllowedValues": [
            "True",
            "true",
            "False",
            "false"
           ],
           "Label": "DeletionProtection",
           "Default": false,
           "ParameterKey": "DeletionProtection"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "Optional. The description of the EIP. The description must be 2 to 256 characters in length. It must start with a letter. It cannot start with http://  or https://.",
           "Label": "Description",
           "ParameterKey": "Description"
          },
          {
           "NoEcho": "false",
           "Type": "Json",
           "Description": "Tags to attach to eip. Max support 20 tags to add during create eip. Each tag with two properties Key and Value, and Key is required.",
           "Label": "Tags",
           "MaxLength": 20,
           "ParameterKey": "Tags"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "ISP tag for finance cloud region. only for cn-hangzhou and cn-qingdao region), if you are not finance cloud user, this value will be ignore.",
           "Label": "Isp",
           "ParameterKey": "Isp"
          },
          {
           "NoEcho": "false",
           "Type": "Number",
           "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
           "Label": "Period",
           "MinValue": 1,
           "MaxValue": 9,
           "Default": 1,
           "ParameterKey": "Period"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "Resource group id.",
           "Label": "ResourceGroupId",
           "ParameterKey": "ResourceGroupId"
          },
          {
           "NoEcho": "false",
           "Type": "Boolean",
           "Description": "Automatic Payment. Default is false.",
           "AllowedValues": [
            "True",
            "true",
            "False",
            "false"
           ],
           "Label": "AutoPay",
           "Default": false,
           "ParameterKey": "AutoPay"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "The resource charge type. Default value is Postpaid",
           "AllowedValues": [
            "Prepaid",
            "Postpaid"
           ],
           "Label": "InstanceChargeType",
           "Default": "Postpaid",
           "ParameterKey": "InstanceChargeType"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "Price cycle of the resource. This property has no default value. If ChargeType is specified as Postpaid, this value will be ignore.",
           "AllowedValues": [
            "Month",
            "Year"
           ],
           "Label": "PricingCycle",
           "Default": "Month",
           "ParameterKey": "PricingCycle"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "The network charge type. Support 'PayByBandwidth' and 'PayByTraffic' only. Default is PayByBandwidth. PayByTraffic will charge by hour, PayByBandwidth will charge by day. ",
           "AllowedValues": [
            "PayByBandwidth",
            "PayByTraffic"
           ],
           "Label": "InternetChargeType",
           "Default": "PayByBandwidth",
           "ParameterKey": "InternetChargeType"
          },
          {
           "NoEcho": "false",
           "Type": "Number",
           "Description": "Bandwidth for the output network. Default is 5MB.",
           "Label": "Bandwidth",
           "Default": 5,
           "ParameterKey": "Bandwidth"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "The network type. Valid value: public (public network).",
           "Label": "Netmode",
           "ParameterKey": "Netmode"
          },
          {
           "NoEcho": "false",
           "Type": "String",
           "Description": "The name of the EIP. The name must be 2 to 128 characters in length. It must start with a letter. It can contain numbers, periods (.), underscores (_), and hyphens (-). It cannot start with http://  or https://",
           "Label": "Name",
           "ParameterKey": "Name"
          }
         ],
         "RequestId": "2AA4188A-15D8-4BB4-9C26-847ED8315D20",
         "Version": "2015-09-01",
         "Metadata": {},
         "ResourceIdentifierSummaries": [
          {
           "LogicalResourceIds": [
            "ElasticIp"
           ],
           "ResourceType": "ALIYUN::VPC::EIP",
           "ResourceIdentifiers": [
            "AllocationId"
           ]
          }
         ]
        }
        ```

    3.  View the value of `ResourceIdentifiers` in the `ResourceIdentifierSummaries` section. This value is the resource identifier property.

        In this example, `AllocationId` is returned for `ResourceIdentifiers`, which indicates that an ALIYUN::VPC::EIP resource can be identified by using its ID.



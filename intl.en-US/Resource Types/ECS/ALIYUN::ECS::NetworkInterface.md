# ALIYUN::ECS::NetworkInterface {#concept_acc_41n_qgb .concept}

Creates an elastic network interface \(ENI\).

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::NetworkInterface",
  "Properties": {
    "SecurityGroupId": String,
    "VSwitchId": String,
    "Description": String,
    "NetworkInterfaceName": String,
    "PrimaryIpAddress": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SecurityGroupId|String|Yes|Yes|The ID of the security group associated with the ENI. The security group and the ENI must be in the same VPC.|N/A|
|VSwitchId|String|Yes|No|Specifies the ID of the VSwitch in the VPC.|N/A|
|Description|String|No|Yes| The description of the ENI. The description must be 2 to 256 characters in length and must not start with http:// or https://.

 This parameter is unspecified by default.

 |N/A|
|NetworkInterfaceName|String|No|Yes| The name of the ENI. The name must be 2 to 128 characters in length, including digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with an uppercase letter, lowercase letter or a Chinese character and must not start with http:// or https://.

 This parameter is unspecified by default.

 |N/A|
|PrimaryIpAddress|String|No|No|The primary private IP address of the ENI. The specified IP address must be an unused address within the IP range of the virtual switch. If this parameter is unspecified, a random unused IP address is assigned to the VSwitch by default.|N/A|

## Response elements {#section_fsg_t4n_4fb .section}

**FN:GetAtt**

-   NetworkInterfaceId: indicates the ID of the ENI.

## Example {#section_klp_54n_4fb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of your ENI. It is a string of [2, 256] English or Chinese characters."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the security group that the ENI joins. The security group and the ENI must be in a same VPC."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VSwitch ID of the specified VPC. Specifies the switch ID for the VPC."
    },
    "NetworkInterfaceName": {
      "Type": "String",
      "Description": "Name of your ENI. It is a string of [2, 128]  Chinese or English characters. It must begin with a letter and can contain numbers, underscores (_), colons (:), or hyphens (-)."
    },
    "PrimaryIpAddress": {
      "Type": "String",
      "Description": "The primary private IP address of the ENI.  The specified IP address must have the same Host ID as the VSwitch. If no IP addresses are specified, a random network ID is assigned for the ENI."
    }
  },
  "Resources": {
    "EniInstance": {
      "Type": "ALIYUN::ECS::NetworkInterface",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "NetworkInterfaceName": {
          "Ref": "NetworkInterfaceName"
        },
        "PrimaryIpAddress": {
          "Ref": "PrimaryIpAddress"
        }
      }
    }
  },
  "Outputs": {
    "NetworkInterfaceId": {
      "Description": "ID of your Network Interface.",
      "Value": {
        "Fn::GetAtt": [
          "EniInstance",
          "NetworkInterfaceId"
        ]
      }
    }
  }
}
```


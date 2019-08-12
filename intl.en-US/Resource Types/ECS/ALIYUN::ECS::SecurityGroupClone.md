# ALIYUN::ECS::SecurityGroupClone {#concept_54355_zh .concept}

ALIYUN::ECS::SecurityGroupClone is used to clone a security group.

## Syntax {#section_xyd_mz2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::SecurityGroupClone",
  "Properties": {
    "SourceSecurityGroupId": String,
    "NetworkType": String,
    "VpcId": String,
    "Description": String,
    "SecurityGroupName": String,
    "DestinationRegionId": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SourceSecurityGroupId|String|Yes|No|The ID of the security group to be cloned.|Only applicable security group rules are copied to the new security group. The security group rules are selected based on the network type of the new security group.|
|NetworkType|String|No|No|The network type of the new security group.|Valid value: Classic|
|VpcId|String|No|No|The ID of the VPC to which the new security group belongs.|The NetworkType parameter is ignored if both the VpcId and NetworkType parameters are specified.|
|Description|String|No|No|The description of the security group.|The description must be 2 to 256 characters in length. It cannot start with http:// or https://.|
|SecurityGroupName|String|No|No|The name of the security group.|This parameter is empty by default. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.|
|DestinationRegionId|String|No|No|The ID of the destination region where the new security group resides.|Default value: CURRENT|

## Response parameters { .section}

 **Fn::GetAtt** 

SecurityGroupId: the ID of the security group.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SecurityGroupClone": {
      "Type": "ALIYUN::ECS::SecurityGroupClone",
      "Properties": {
        "SourceSecurityGroupId": {
          "Ref": "SourceSecurityGroupId"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Description": {
          "Ref": "Description"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "DestinationRegionId": {
          "Ref": "DestinationRegionId"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        }
      }
    }
  },
  "Parameters": {
    "SourceSecurityGroupId": {
      "Type": "String",
      "Description": "Source security group ID is used to copy properties to clone new security group. If the NetworkType and VpcId parameters are not specified, the same security group will be cloned. If NetworkType or VpcId is specified, only proper security group rules will be cloned."
    },
    "VpcId": {
      "Type": "String",
      "Description": "Physical ID of the VPC."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the security group, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "Display name of the security group, [2, 128] characters, must start with a letter, can contain numbers, '_' or '.', '-'"
    },
    "DestinationRegionId": {
      "Default": "CURRENT",
      "Type": "String",
      "Description": "Clone security group to the specified region. Default to current region."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "Clone new security group as classic network type. If the VpcId parameter is specified, the value will be ignored.",
      "AllowedValues": [
        "Classic"
      ]
    }
  },
  "Outputs": {
    "SecurityGroupId": {
      "Description": "Generated security group ID of new security group.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityGroupClone",
          "SecurityGroupId"
        ]
      }
    }
  }
}
```


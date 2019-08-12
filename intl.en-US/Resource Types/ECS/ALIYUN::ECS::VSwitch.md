# ALIYUN::ECS::VSwitch {#concept_51192_zh .concept}

Creates a VSwitch.

## Syntax {#section_vs2_ldf_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::VSwitch",
  "Properties": {
    "ZoneId": String,
    "CidrBlock": String,
    "VpcId": String,
    "VSwitchName": String,
    "Description": String
  }
}
```

## Properties {#section_zh3_pdf_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|VpcId|String|Yes|No|The ID of the VPC where a VSwitch is to be created|N/A.|
|ZoneId|String|Yes|No|The ID of the zone to which the VSwtich is assigned|N/A.|
|VSwitchName|String|No|No|The name of the VSwitch to be created|The name must be 2 to 128 characters in length, including letters, Chinese characters, digits, underscores\(\_\) and hyphens \(-\). It must start with an uppercase letter, lowercase letter, or Chinese character, and must not start with http:// or https://.|
|CidrBlock|String|Yes|No|The CIDR block of the VSwitch|The Classless Inter-Domain Routing \(CIDR\) block of the VSwitch must be a subnet of the VPC where the VSwitch is located and not used by other VSwitches.|
|Description|String|No|No|The description of the VSwitch|The description must be 2 to 258 characters in length and must not start with http:// or https://.|

## Response elements {#section_svv_qdf_lfb .section}

**Fn::GetAtt**

VSwitchId: indicates the VSwitch ID allocated by the system.

## Example {#section_wdy_tdf_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcName": {
      "Type": "String"
    },
    "VSwitch1CidrBlock": {
      "Type": "String",
      "Default": "172.16.100.0/24"
    },
    "VSwitch2CidrBlock": {
        "Type": "String",
        "Default": "172.16.80.0/24"
    }
  },
  "Resources": {
    "EcsVpc": {
      "Type": "ALIYUN::ECS::VPC",
      "Properties": {
        "CidrBlock": "172.16.0.0/12",
        "VpcName": {"Ref": "VpcName"},
      },
    },
    "VSwitch1": {
      "Type": "ALIYUN::ECS::VSwitch",
      "Properties": {
        "ZoneId": "cn-beijing-a",
        "CidrBlock": {"Ref": "VSwitch1CidrBlock"},
        "VpcId": { "Fn::GetAtt": [ "EcsVpc", "VpcId" ] },
        "VSwitchName": "create_vpc_vswitch_sg1"
      }
    },
    "VSwitch2": {
      "Type": "ALIYUN::ECS::VSwitch",
      "Properties": {
        "ZoneId": "cn-beijing-a",
        "CidrBlock": {"Ref": "VSwitch2CidrBlock"},
        "VpcId": { "Fn::GetAtt": [ "EcsVpc", "VpcId" ] },
        "VSwitchName": "create_vpc_vswitch_sg2"
      }
    },
    "SG_VSwitch1": {
      "Type": "ALIYUN::ECS::SecurityGroup",
      "Properties": {
        "SecurityGroupName": "app_mall",
        "Description": "this is created by heat",
        "VpcId": { "Fn::GetAtt": [ "EcsVpc", "VpcId" ] }
      },
      "Outputs": {
        "SecurityGroupId": {
             "Value": {"get_attr": ["SG_VSwitch1","SecurityGroupId"]}
        }
      }
    },
    "SG_VSwitch1_InRule": {
      "Type": "ALIYUN::ECS::SecurityGroupIngress",
      "Properties": {
        "SecurityGroupId": { "Fn::GetAtt": [ "SG_VSwitch1", "SecurityGroupId" ] },
        "IpProtocol": "tcp",
        "PortRange": "1/65535",
        "SourceCidrIp": {"Ref": "VSwitch2CidrBlock"}
      }
    },
    "SG_VSwitch1_OutRule": {
      "Type": "ALIYUN::ECS::SecurityGroupEgress",
      "Properties": {
        "SecurityGroupId": { "Fn::GetAtt": [ "SG_VSwitch1", "SecurityGroupId" ] },
        "IpProtocol": "tcp",
        "PortRange": "1/65535",
        "DestCidrIp": {"Ref": "VSwitch2CidrBlock"}
      }
    },
    "SG_VSwitch2": {
      "Type": "ALIYUN::ECS::SecurityGroup",
      "Properties": {
        "SecurityGroupName": "app_mall",
        "Description": "this is created by heat",
        "VpcId": { "Fn::GetAtt": [ "EcsVpc", "VpcId" ] }
      },
    },
    "SG_VSwitch2_InRule": {
      "Type": "ALIYUN::ECS::SecurityGroupIngress",
      "Properties": {
        "SecurityGroupId": { "Fn::GetAtt": [ "SG_VSwitch2", "SecurityGroupId" ] },
        "IpProtocol": "tcp",
        "PortRange": "1/65535",
        "SourceCidrIp": {"Ref": "VSwitch1CidrBlock"}
      }
    },
    "SG_VSwitch2_OutRule": {
      "Type": "ALIYUN::ECS::SecurityGroupEgress",
      "Properties": {
        "SecurityGroupId": { "Fn::GetAtt": [ "SG_VSwitch2", "SecurityGroupId" ] },
        "IpProtocol": "tcp",
        "PortRange": "1/65535",
        "DestCidrIp": {"Ref": "VSwitch1CidrBlock"}
      }
    }
  }
}
```


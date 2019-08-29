# ALIYUN::ECS::VSwitch {#concept_51192_zh .concept}

ALIYUN::ECS::VSwitch 类型用于新建交换机。

## 语法 {#section_vs2_ldf_lfb .section}

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

## 属性 {#section_zh3_pdf_lfb .section}

|名称|类型|必须|允许更新|描述|约束|
|--|--|--|----|--|--|
|VpcId|String|是|否|将要创建交换机的专有网络 ID。|无。|
|ZoneId|String|是|否|可用区 ID。|无。|
|VSwitchName|String|否|否|VSwitch 名称。|参数值长度为\[2, 128\]。必须以大小写字母或汉字开头，可包含英文字母、汉字、数字、下划线（\_）和连字符（-）。不能以 http:// 或 https:// 开头。|
|CidrBlock|String|是|否|VSwitch 网段。|必须是所属专有网络的子网段，并且没有被其他交换机占用。|
|Description|String|否|否|交换机描述。|参数值长度为\[2, 256\]。不能以 http:// 和 https:// 开头。|

## 返回值 {#section_svv_qdf_lfb .section}

**Fn::GetAtt**

VSwitchId：系统分配的 VSwitch ID。

## 示例 {#section_wdy_tdf_lfb .section}

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


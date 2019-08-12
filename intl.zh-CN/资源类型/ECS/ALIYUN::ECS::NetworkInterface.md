# ALIYUN::ECS::NetworkInterface {#concept_acc_41n_qgb .concept}

ALIYUN::ECS::NetworkInterface类型用于创建一个弹性网卡（ENI）。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_9n0_7kw_i0n .language-json}
{
  "Type": "ALIYUN::ECS::NetworkInterface",
  "Properties": {
    "Description": String,
    "SecurityGroupId": String,
    "PrimaryIpAddress": String,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "NetworkInterfaceName": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|SecurityGroupId|String|是|是|所属的安全组ID必须是同一个VPC下的安全组。|无|
|VSwitchId|String|是|否|指定VPC的交换机ID。|无|
|Description|String|否|是| 弹性网卡的描述信息。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。

 默认值：空。

 |无|
|NetworkInterfaceName|String|否|是| 弹性网卡名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空。

 |无|
|PrimaryIpAddress|String|否|否|弹性网卡的主私有IP地址。指定IP必须是在所属交换机的地址段内的空闲地址，不指定则默认随机分配该交换机中的空闲地址。|无|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   NetworkInterfaceId: 弹性网卡ID。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_ldn_jj7_kud}
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


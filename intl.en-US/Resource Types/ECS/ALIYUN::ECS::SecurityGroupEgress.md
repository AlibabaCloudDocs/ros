# ALIYUN::ECS::SecurityGroupEgress {#concept_51189_zh .concept}

Creates an outbound access rule for a security group.

## Syntax {#section_wz1_wz2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::SecurityGroupEgress",
  "Properties": {
    "SecurityGroupId": String,
    "IpProtocol": String,
    "PortRange": String,
    "DestGroupId": String,
    "DestGroupOwnerAccount": String,
    "DestCidrIp": String,
    "Policy": String,
    "Priority": String,
    "NicType": String
  }
}
```

## Properties {#section_xfj_xz2_lfb .section}

|Property|Type|Required|Editable|Description|Validity|
|--------|----|--------|--------|-----------|--------|
|IpProtocol|String|Yes|No|The IP protocol.|Valid values: tcp | udp | icmp | gre | all. The value all indicates that it supports four protocols.|
|PortRange|String|No|No|The port range of a specific IP protocol.| If the IpProtocol parameter is set to tcp or udp, the default port is used. Value range: 1 to 65535. For example, 1/200 indicates that the port range is from 1 to 200. If 200/1 is entered, an error message appears when the API is called.

 If the IpProtocol parameter is set to icmp, the port range is -1/-1.

 If the IpProtocol parameter is set to gre, the port range is -1/-1.

 If the IpProtocol parameter is set to all, the port range is -1/-1.

 |
|SecurityGroupId|String|No|No|The ID of the security group for which an outbound access rule is to be created.|N/A|
|NicType|String|No|No|The network type.| Valid values: internet | intranet.

 Default value: internet.

 |
|Priority|Integer|No|No|The priority level of the authorization policy.|Value range: 1 to 100. Default value: 1.|
|DestGroupId|String|No|No|The ID of the destination security group in the same region.|You must specify either the DestGroupId parameter or the DestCidrIp parameter. If both are specified, DestCidrIp is granted access to the specified IP range by default. If only the DestGroupId parameter is specified, the NicType parameter must be set to intranet.|
|DestCidrIp|String|No|No|The destination IP address range.|The IP address range must be specified in CIDR notation. The default value is 0.0.0.0/0, indicating that no restriction is applied. For example, an applicable value is 10.159.6.18/12. Only IPV4 addresses are supported.|
|Policy|String|No|No|The authorization policy.|Valid values: accept \(access request accepted\) | drop \(access request denied\). Default value: accept.|
|DestGroupOwnerAccount|String|No|No|The Alibaba Cloud account that manages the destination security group. If this parameter is specified, the destination security group authorizes a security group of another account to set an access rule.|N/A|
|Description|String|No|No|The description of the security group rule.|The description must be 1 to 512 characters in length.|
|DestGroupOwnerId|String|No|No|The ID of the Alibaba Cloud account that manages the destination security group. If this parameter is specified, the destination security group authorizes a security group of another account to set an access rule.-   If neither the DestGroupOwnerId nor the DestGroupOwnerAccount is specified, the access rule of your other security groups is set.
-   The DestGroupOwnerId parameter is inapplicable If the DestCidrIp parameter is specified.

|N/A|

## Response elements {#section_tlq_f1f_lfb .section}

**Fn::GetAtt**

None.

## Example {#section_jny_h1f_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SG": {
      "Type": "ALIYUN::ECS::SecurityGroupEgress",
      "Properties": {
        "SecurityGroupId": "sg-25bowo058",
        "IpProtocol": "tcp",
        "PortRange": "65535/65535",
        "DestCidrIp": "0.0.0.0/0"
      }
    }
  }
}
```


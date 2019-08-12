# ALIYUN::ECS::SecurityGroupIngress {#concept_51206_zh .concept}

Creates an inbound access rule for a security group.

## Syntax {#section_sff_p1f_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::SecurityGroupIngress",
  "Properties": {
    "SecurityGroupId": String,
    "IpProtocol": String,
    "PortRange": String,
    "SourceGroupId": String,
    "SourceGroupOwnerAccount": String,
    "SourceCidrIp": String,
    "Policy": String,
    "Priority": String,
    "NicType": String
  }
}
```

## Properties {#section_wgj_q1f_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|IpProtocol|String|Yes|No|The IP protocol.|Valid values: tcp | udp | icmp | gre | all. The value all indicates that it supports four protocols.|
|PortRange|String|No|No|The port range of a specific IP protocol.| If the IpProtocol parameter is set to tcp or udp, the default port is used. Value range: 1 to 65535. For example, 1/200 indicates that the port range is from 1 to 200. If 200/1 is entered, an error message appears when the API is called.

 If the IpProtocol parameter is set to icmp, the port range is -1/-1.

 If the IpProtocol parameter is set to gre, the port range is -1/-1.

 If the IpProtocol parameter is set to all, the port range is -1/-1.

 |
|SourceGroupId|String|No|No|The ID of the source security group in the same region.|The ID of the source security group. You must specify either the SourceGroupId parameter or the SourceCidrIp parameter. If both are specified, SourceCidrIp is granted access to the specified IP range by default. If only the SourceGroupId parameter is specified, the NicType parameter must be set to intranet.|
|SecurityGroupId|String|No|No|The ID of the security group for which the inbound access rule is to be created.|N/A|
|NicType|String|No|No|The network type.| Valid values: internet | intranet.

 Default value: internet.

 |
|SourceGroupOwnerAccount|String|No|No|The Alibaba Cloud account that manages the source security group. If this parameter is specified, the source security group authorizes a security group of another account to set an access rule.|If this parameter is unspecified, the source security group authorizes a security group of the same account to set an access rule by default. This parameter is inapplicable if the SourceCidrIp parameter is specified.|
|Priority|Integer|No|No|The priority level of the authorization policy.| Value range: 1 to 100.

 Default value: 1.

 |
|SourceCidrIp|String|No|No|The destination IP address range.| The IP address range must be specified in CIDR format.

 The default value is 0.0.0.0/0, indicating that no restriction is applied. Other applicable values include 10.159.6.18/12. Only IPv4 addresses are supported.

 |
|Policy|String|No|No|The authorization policy.| Valid values: accept \(access request accepted\) | drop \(access request denied\).

 Default value: accept.

 |
|SourceGroupOwnerId|String|No|No|The ID of the Alibaba Cloud account that manages the source security group. If this parameter is specified, the source security group authorizes a security group of another account to set an access rule.-   If SourceGroupOwnerId and SourceGroupOwnerAccount is unspecified, the access rule of your other security groups is set.
-   The SourceGroupOwnerId parameter is inapplicable if the SourceCidrIp parameter is specified.

|N/A|
|Description|string|No|No|The description of the security group rule|The description must be 1 to 512 characters in length.|

## Response elements {#section_eky_v1f_lfb .section}

**Fn::GetAtt**

None.

## Example {#section_opn_y1f_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SG": {
      "Type": "ALIYUN::ECS::SecurityGroupIngress",
      "Properties": {
        "SecurityGroupId": "sg-25bowo058",
        "IpProtocol": "tcp",
        "PortRange": "65535/65535",
        "SourceCidrIp": "0.0.0.0/0"
      }
    }
  }
}
```


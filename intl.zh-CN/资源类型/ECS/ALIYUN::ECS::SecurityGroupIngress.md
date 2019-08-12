# ALIYUN::ECS::SecurityGroupIngress {#concept_51206_zh .concept}

ALIYUN::ECS::SecurityGroupIngress 类型可用于创建安全组入方向的访问规则。

## 语法 {#section_sff_p1f_lfb .section}

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

## 属性 {#section_wgj_q1f_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IpProtocol|string|是|否|IP 协议。|可选值：tcp、udp、icmp、gre和 all。 all 表示同时支持四种协议。|
|PortRange|string|否|否|IP 协议相关的端口号范围 。| 协议为 tcp 或 udp 时默认端口号，取值范围为1~65535；例如 “1/200” 意思是端口号范围为 1~200。若输入值为：“200/1”，接口调用将报错。

 协议为 icmp 时端口号范围值为-1/-1。

 协议为 gre 时端口号范围值为-1/-1。

 协议为 all 时端口号范围值为-1/-1。

 |
|SourceGroupId|string|否|否|同一 Region 内的源安全组 ID 。|源安全组 ID。SourceGroupId 或 SourceCidrIp 参数必须设置一项。如果两项都设置，则默认对 SourceCidrIp授权。如果指定了该字段，但没有指定 SourceCidrIp，则 NicType只能选择 intranet。|
|SecurityGroupId|string|否|否|指定需要创建入规则的安全组 ID。|无|
|NicType|string|否|否|网络类型 。| 取值：internet 或 intranet。

 默认值为internet。

 |
|SourceGroupOwnerAccount|string|否|否|跨用户安全组授权时，源安全组所属用户的阿里云账号。|如果未设置，则默认为同一账户安全组间授权。SourceCidrIp如果已经被设置，则该参数无效。|
|Priority|integer|否|否|授权策略优先级。| 参数值可为：1-100。

 默认值为：1 。

 |
|SourceCidrIp|string|否|否|目标 IP 地址范围 。| 必须采用 CIDR 格式来指定 IP 地址范围。

 默认值为 0.0.0.0/0（表示不受限制），其他支持的格式，如 10.159.6.18/12。仅支持 IPV4。

 |
|Policy|string|否|否|授权策略 。| 参数值可为：accept（接受访问）或 drop \(拒绝访问\)。

 默认值为：accept。

 |
|SourceGroupOwnerId|string|否|否|跨账户设置安全组规则时，源端安全组所属的阿里云账户 ID。-   如果 SourceGroupOwnerId 及 SourceGroupOwnerAccount 均未设置，则认为是设置您其他安全组的访问权限。
-   如果您已经设置参数 SourceCidrIp，则参数 SourceGroupOwnerId 无效。

|无。|
|Description|string|否|否|安全组规则的描述信息。|长度为 \[1, 512\] 个字符。|

## 返回值 {#section_eky_v1f_lfb .section}

**Fn::GetAtt**

无

## 示例 {#section_opn_y1f_lfb .section}

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


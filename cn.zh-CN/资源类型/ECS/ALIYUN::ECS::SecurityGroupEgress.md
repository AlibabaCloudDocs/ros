# ALIYUN::ECS::SecurityGroupEgress {#concept_51189_zh .concept}

ALIYUN::ECS::SecurityGroupEgress 类型可用于创建安全组出方向的访问规则。

## 语法 {#section_wz1_wz2_lfb .section}

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

## 属性 {#section_xfj_xz2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IpProtocol|string|是|否|IP协议。|可选值：tcp、udp、icmp、gre 和 all。 all 表示同时支持四种协议。|
|PortRange|string|否|否|IP协议相关的端口号范围 。| 协议为 tcp 或 udp 时，默认端口号。取值范围为 1~65535。例如 “1/200” 意思是端口号范围为 1~200，若输入值为：“200/1”，接口调用将报错。

 协议为 icmp 时，端口号范围值为-1/-1。

 协议为 gre 时，端口号范围值为-1/-1。

 协议为 all 时，端口号范围值为-1/-1。

 |
|SecurityGroupId|string|否|否|指定需要创建出规则的安全组 ID。|无|
|NicType|string|否|否|网络类型 。| 取值：internet 或 intranet。

 默认值为internet。

 |
|Priority|integer|否|否|授权策略优先级。|参数值可为：1-100。默认值为：1。|
|DestGroupId|string|否|否|同一 Region 内的目标安全组 ID。|DestGroupId 或者 DestCidrIp 参数必须设置一项。如果两项都设置，则默认对 DestCidrIp 授权。如果指定了该字段且没有指定 DestCidrIp，则 NicType 只能选择 intranet。|
|DestCidrIp|string|否|否|目标 IP 地址范围 。|必须采用 CIDR 格式来指定 IP 地址范围，默认值为0.0.0.0/0（表示不受限制）。其他支持的格式，例如 10.159.6.18/12。仅支持 IPV4。|
|Policy|string|否|否|授权策略。|参数值可为：accept（接受访问）或 drop \(拒绝访问\)。默认值为：accept。|
|DestGroupOwnerAccount|string|否|否|目的端安全组所属帐号ID，亦即UID。|无|
|Description|string|否|否|安全组规则的描述信息。|长度为 \[1, 512\] 个字符。|
|DestGroupOwnerId|string|否|否|目的端安全组所属的帐号登录名称。|无。|

## 返回值 {#section_tlq_f1f_lfb .section}

**Fn::GetAtt**

无

## 示例 {#section_jny_h1f_lfb .section}

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


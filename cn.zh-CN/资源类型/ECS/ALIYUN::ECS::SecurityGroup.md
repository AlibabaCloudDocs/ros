# ALIYUN::ECS::SecurityGroup {#concept_51207_zh .concept}

ALIYUN::ECS::SecurityGroup 类型可用于创建安全组。

## 语法 {#section_sf3_5x2_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ECS::SecurityGroup",
  "Properties": {
    "VpcId": String,
    "Description": String,
    "SecurityGroupName": String,
    "Tags": List,
    "SecurityGroupEgress": List,
    "SecurityGroupIngress": List,
    "ResourceGroupId": String
  }
}
```

## 属性 {#section_g2f_wx2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|VpcId|String|否|否|专有网络 ID|无|
|Description|String|否|否|安全组描述信息|\[2, 256\] 个字符。不能以 http:// 和 https:// 开头。|
|Tags|List|否|否|用户自定义标签|最多支持 4 个标签，格式如: \[\{“Key”:”tagKey”,”Value”:”tagValue”\},\{“Key”:”tagKey2”,”Value”:”tagValue2”\}\]。|
|SecurityGroupName|String|否|否|安全组名称|不填则为空，默认值为空。长度为 \[2, 128\] 英文或中文字符，必须以大小字母或中文开头，可包含字母，汉字、数字，点（.）、下划线（\_）、和连字符（-）。磁盘名称会展示在控制台。不能以 http:// 和 https:// 开头。|
|SecurityGroupEgress|List|否|否|安全组出方向的访问规则|无|
|SecurityGroupIngress|List|否|否|安全组入方向的访问规则|无|

## Tags 语法 {#section_im4_by2_lfb .section}

``` {#codeblock_uoz_vdu_2d5 .language-json}
"Tags": [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tags 属性 {#section_wfu_0rz_ppw .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|无|无|
|Value|String|否|否|无|无|

## SecurityGroupEgress语法 {#section_lng_y21_pq0 .section}

``` {#codeblock_uoz_vdu_2d5 .language-json}
"SecurityGroupEgress": [
  {
    "Description": String,
    "PortRange": String,
    "SecurityGroupId": String,
    "NicType": String,
    "Priority": Integer,
    "DestGroupId": String,
    "DestCidrIp": String,
    "Policy": String,
    "IpProtocol": String,
    "DestGroupOwnerAccount": String,
    "DestGroupOwnerId": String
  }
]
```

## SecurityGroupEgress 属性 {#section_0mv_0n3_5gr .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|否|安全组规则的描述信息。长度为1~512个字符。|无。|
|DestGroupOwnerId|String|否|否|跨账户设置安全组规则时，目的端安全组所属的阿里云账户 ID。如果 DestGroupOwnerId 及 DestGroupOwnerAccount 均未设置，则认为是设置您其他安全组的访问权限。如果您已经设置参数 DestCidrIp，则参数 DestGroupOwnerId 无效。|无。|
|IpProtocol|String|是|否|IP 协议|可选值：tcp、udp、icmp、 gre 或 all。 all 表示同时支持四种协议。|
|PortRange|String|否|否|IP 协议相关的端口号范围| 协议为 tcp 或 udp 时默认端口号，取值范围为 1~65535。例如 “1/200” 意思是端口号范围为 1~200。若输入值为 “200/1”， 接口调用将报错。

 协议为 icmp 时，端口号范围值为： -1/-1。

 协议为 gre 时，端口号范围值为： -1/-1。

 协议为 all 时，端口号范围值为： -1/-1。

 |
|SecurityGroupId|String|否|否|指定需要创建出规则的安全组 ID|无|
|NicType|String|否|否|网络类型| 可选值：internet、 intranet。

 默认值为 internet。

 |
|Priority|Integer|否|否|授权策略优先级|参数值可为：1~100，默认值为：1。|
|DestGroupId|String|否|否|同一 Region 内的目标安全组 ID|DestGroupId 或者 DestCidrIp 参数必须设置一项。如果两项都设置，则默认对 DestCidrIp 授权。如果指定了该字段，且没有指定 DestCidrIp，则 NicType 只能选择 intranet。|
|DestCidrIp|String|否|否|目标IP地址范围|必须采用 CIDR 格式来指定 IP 地址范围。默认值为： 0.0.0/0（表示不受限制）。其他支持的格式，如 10.159.6.18/12。仅支持 IPV4。|
|Policy|String|否|否|授权策略|参数值可为：accept（接受访问）、drop \(拒绝访问\)。默认值为：accept。|
|DestGroupOwnerAccount|String|否|否|跨用户安全组授权时，目标安全组所属用户阿里云账号。|无|

## SecurityGroupIngress 语法 {#section_msk_foi_a0p .section}

``` {#codeblock_z17_lwl_m80 .language-json}
"SecurityGroupIngress": [
  {
    "SourceGroupOwnerId": String,
    "Description": String,
    "PortRange": String,
    "SecurityGroupId": String,
    "NicType": String,
    "SourceGroupOwnerAccount": String,
    "Priority": Integer,
    "SourceGroupId": String,
    "Policy": String,
    "IpProtocol": String,
    "SourceCidrIp": String
  }
]
```

## SecurityGroupIngress 属性 {#section_cex_usg_xo8 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SourceGroupOwnerId|String|否|否|源安全组所属的阿里云账户 ID。|无。|
|Description|String|否|否|安全组规则的描述信息。长度为1~512个字符。|无。|
|IpProtocol|String|是|否|IP协议|可选值：tcp、 udp、 icmp、 gre 、或 all。 all 表示同时支持四种协议。|
|PortRange|String|否|否|IP 协议相关的端口号范围| 协议为 tcp 或 udp 时默认端口号，取值范围为 1~65535。例如 “1/200” 意思是端口号范围为 1~200。若输入值为“200/1” 接口调用将报错。

 协议为 icmp 时，端口号范围值为 -1/-1。

 协议为 gre 时，端口号范围值为 -1/-1。

 协议为 all时，端口号范围值为 -1/-1。

 |
|SourceGroupId|String|否|否|同一 Region 内的源安全组 ID|源安全组 ID，SourceGroupId 或者 SourceCidrIp 参数必须设置一项。如果两项都设置，则默认对 SourceCidrIp 授权。如果指定了该字段，且没有指定 SourceCidrIp，则 NicType 只能选择 intranet。|
|SecurityGroupId|String|否|否|指定需要创建入规则的安全组 ID|无|
|NicType|String|否|否|网络类型|可选值：internet、 intranet。默认值为：internet。|
|SourceGroupOwnerAccount|String|否|否|跨用户安全组授权时，目标安全组所属用户阿里云账号。|无|
|Priority|Integer|否|否|授权策略优先级|参数值可为：1~100。默认值为：1。|
|SourceCidrIp|String|否|否|目标 IP 地址范围|必须采用 CIDR 格式来指定 IP 地址范围。默认值为：：0.0.0.0/0（表示不受限制）。其他支持的格式，如 10.159.6.18/12。仅支持 IPV4。|
|Policy|String|否|否|授权策略|参数值可为：accept（接受访问）、 drop \(拒绝访问\)。 默认值为：accept。|

## 返回值 {#section_qxy_sqt_bi5 .section}

**Fn::GetAtt**

SecurityGroupId：安全组 ID。

## 示例 {#section_aet_c55_k3x .section}

``` {#codeblock_aeb_q84_wqt .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "SG": {
      "Type": "ALIYUN::ECS::SecurityGroup",
      "Properties": {
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "SecurityGroupIngress": [
          {
            "SourceCidrIp": "0.0.0.0/0",
            "IpProtocol": "all",
            "NicType": "internet",
            "PortRange": "-1/-1",
            "Priority": 1
          },
          {
            "SourceCidrIp": "0.0.0.0/0",
            "IpProtocol": "all",
            "NicType": "intranet",
            "PortRange": "-1/-1",
            "Priority": 1
          }
        ],
        "SecurityGroupEgress": [
          {
            "IpProtocol": "all",
            "DestCidrIp": "0.0.0.0/0",
            "NicType": "internet",
            "PortRange": "-1/-1",
            "Priority": 1
          },
          {
            "IpProtocol": "all",
            "DestCidrIp": "0.0.0.0/0",
            "NicType": "intranet",
            "PortRange": "-1/-1",
            "Priority": 1
          }
        ],
        "VpcId": {
          "Ref": "Vpc"
        }
      }
    }
  },
  "Outputs": {
    "SecurityGroupId": {
      "Value" : {"Fn::GetAtt": ["SG","SecurityGroupId"]}
    }
  }
}
```


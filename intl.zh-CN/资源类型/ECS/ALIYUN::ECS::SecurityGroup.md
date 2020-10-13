# ALIYUN::ECS::SecurityGroup

ALIYUN::ECS::SecurityGroup类型用于创建安全组。

## 语法

```
{
  "Type": "ALIYUN::ECS::SecurityGroup",
  "Properties": {
    "VpcId": String,
    "Description": String,
    "SecurityGroupName": String,
    "Tags": List,
    "SecurityGroupEgress": List,
    "SecurityGroupIngress": List,
    "ResourceGroupId": String,
    "SecurityGroupType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无|
|VpcId|String|否|否|专有网络ID。|无|
|Description|String|否|否|安全组描述信息。|长度为2~256个字符。|
|Tags|List|否|是|安全组的标签。|最多支持20个标签。 详情请参见[Tags属性](#section_wfu_0rz_ppw)。 |
|SecurityGroupName|String|否|否|安全组名称。|不填则为空，默认值为空。 -   长度为2~128个字符。
-   必须以英文字母或汉字开头，不能以`http://`和`https://`开头。
-   可包含英文字母、汉字、数字、英文句点（.）、下划线（\_）和短划线（-）。 |
|SecurityGroupEgress|List|否|是|安全组出方向的访问规则。|详情请参见[SecurityGroupEgress属性](#section_0mv_0n3_5gr)。|
|SecurityGroupIngress|List|否|是|安全组入方向的访问规则。|详情请参见[SecurityGroupIngress属性](#section_cex_usg_xo8)。|
|SecurityGroupType|String|否|否|安全组的类型。|取值： -   normal：基本安全组。
-   enterprise：高级安全组。 |

## Tags语法

```
"Tags": [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## SecurityGroupEgress语法

```
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
    "DestGroupOwnerId": String,
    "Ipv6DestCidrIp": String
  }
]
```

## SecurityGroupEgress属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|安全组规则的描述信息。|长度为1~512个字符。|
|DestGroupOwnerId|String|否|否|跨账号设置安全组规则时，目的端安全组所属的阿里云账号ID。|如果未设置DestGroupOwnerId，则认为您设置了其它安全组的访问权限。如果您已经设置参数DestCidrIp，则参数DestGroupOwnerId无效。|
|IpProtocol|String|是|否|IP协议。|取值： -   tcp
-   udp
-   icmp
-   gre
-   all：同时支持四种协议。 |
|PortRange|String|是|否|IP协议相关的端口号范围。|目的端安全组开放的传输层协议相关的端口范围。取值： -   TCP/UDP协议：1~65,535。使用正斜线（/）分隔起始端口和终止端口。
    -   正确示例：1/200。
    -   错误示例：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。 |
|SecurityGroupId|String|否|否|需要创建出方向规则的安全组ID。|无|
|NicType|String|否|否|网络类型。|取值： -   internet（默认值）
-   intranet |
|Priority|Integer|否|否|授权策略优先级。|取值范围：1~100。 默认值：1。 |
|DestGroupId|String|否|否|同一地域内的目标安全组ID。|DestGroupId或DestCidrIp参数必须指定一项。 -   如果两项都指定，则默认对DestCidrIp进行授权。
-   如果指定了该参数，且没有指定DestCidrIp，则NicType只能选择intranet。 |
|DestCidrIp|String|否|否|目标IP地址范围。|必须采用CIDR格式来指定IP地址范围。默认值： 0.0.0.0/0（表示不受限制）。

其它支持的格式，例如 10.159.XX.XX/12。 最多10个IP地址或地址段，用英文逗号（,）隔开。

**说明：** 仅支持IPv4。 |
|Policy|String|否|否|授权策略。|取值： -   accept（默认值）：接受访问。
-   drop：拒绝访问。 |
|Ipv6DestCidrIp|String|否|否|目标地址IPv6 CIDR地址段。|支持在CIDR格式和IPv6格式的IP地址范围。仅支持专有网络类型的IP地址。|

## SecurityGroupIngress语法

```
"SecurityGroupIngress": [
  {
    "SourceGroupOwnerId": String,
    "Description": String,
    "PortRange": String,
    "SecurityGroupId": String,
    "NicType": String,
    "Ipv6SourceCidrIp": String,
    "Priority": Integer,
    "SourceGroupId": String,
    "Policy": String,
    "IpProtocol": String,
    "SourcePortRange": String,
    "SourceCidrIp": String
  }
]
```

## SecurityGroupIngress属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SourceGroupOwnerId|String|否|否|源安全组所属的阿里云账号ID。|无|
|Description|String|否|是|安全组规则的描述信息。|长度为1~512个字符。|
|IpProtocol|String|是|否|IP协议。|取值： -   tcp
-   udp
-   icmp
-   gre
-   all：同时支持四种协议。 |
|PortRange|String|是|否|IP协议相关的端口范围。|目的端安全组开放的传输层协议相关的端口范围。取值： -   TCP/UDP协议：1~65535。使用正斜线（/）间隔起始端口和终止端口。
    -   正确示例：1/200。
    -   错误示例：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。 |
|SourceGroupId|String|否|否|同一地域内的源安全组ID。|SourceGroupId或者 SourceCidrIp参数必须指定一项。 -   如果两项都指定，则默认对SourceCidrIp授权。
-   如果指定了该参数，且没有指定SourceCidrIp，则NicType只能选择intranet。 |
|SecurityGroupId|String|否|否|需要创建入方向规则的安全组ID。|无|
|NicType|String|否|否|网络类型。|取值： -   internet（默认值）
-   intranet |
|Priority|Integer|否|否|授权策略优先级。|取值范围：1~100。 默认值：1。 |
|SourceCidrIp|String|否|否|源IP地址范围。|必须采用CIDR格式来指定IP地址范围。默认值：0.0.0.0/0（表示不受限制）。

其它支持的格式，例如10.159.XX.XX/12。

最多10个IP地址或地址段，用英文逗号（,）隔开。

**说明：** 仅支持IPV4。 |
|Policy|String|否|否|授权策略。|取值： -   accept（默认值）：接受访问。
-   drop：拒绝访问。 |
|SourcePortRange|String|否|否|源端安全组开放的传输层协议相关的端口范围。|取值： -   TCP/UDP协议：取值为1~65535。使用正斜线（/）间隔起始端口和终止端口。
    -   正确示例：1/200。
    -   错误示例：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   IpProtocol取值为all：-1/-1。 |
|Ipv6SourceCidrIp|String|否|否|源IPv6 CIDR地址段。|仅支持专有网络类型的IP地址。支持在CIDR格式和IPv6格式的IP地址范围。|

## 返回值

Fn::GetAtt

SecurityGroupId：安全组ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the security group, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "VpcId": {
      "Type": "String",
      "Description": "Physical ID of the VPC."
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "Display name of the security group, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SecurityGroupType": {
      "Type": "String",
      "Description": "The type of the security group. Valid values:\nnormal: basic security group\nenterprise: advanced security group",
      "AllowedValues": [
        "normal",
        "enterprise"
      ]
    },
    "SecurityGroupIngress": {
      "Type": "Json",
      "Description": "Ingress rules for the security group."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "SecurityGroupEgress": {
      "Type": "Json",
      "Description": "egress rules for the security group."
    }
  },
  "Resources": {
    "SecurityGroup": {
      "Type": "ALIYUN::ECS::SecurityGroup",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SecurityGroupType": {
          "Ref": "SecurityGroupType"
        },
        "SecurityGroupIngress": {
          "Ref": "SecurityGroupIngress"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "SecurityGroupEgress": {
          "Ref": "SecurityGroupEgress"
        }
      }
    }
  },
  "Outputs": {
    "SecurityGroupId": {
      "Description": "generated security group id for security group.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityGroup",
          "SecurityGroupId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  Description:
    Type: String
    Description: >-
      Description of the security group, [2, 256] characters. Do not fill or
      empty, the default is empty.
  VpcId:
    Type: String
    Description: Physical ID of the VPC.
  SecurityGroupName:
    Type: String
    Description: >-
      Display name of the security group, [2, 128] English or Chinese
      characters, must start with a letter or Chinese in size, can contain
      numbers, '_' or '.', '-'
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  SecurityGroupType:
    Type: String
    Description: |-
      The type of the security group. Valid values:
      normal: basic security group
      enterprise: advanced security group
    AllowedValues:
      - normal
      - enterprise
  SecurityGroupIngress:
    Type: Json
    Description: Ingress rules for the security group.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  SecurityGroupEgress:
    Type: Json
    Description: egress rules for the security group.
Resources:
  SecurityGroup:
    Type: 'ALIYUN::ECS::SecurityGroup'
    Properties:
      Description:
        Ref: Description
      VpcId:
        Ref: VpcId
      SecurityGroupName:
        Ref: SecurityGroupName
      ResourceGroupId:
        Ref: ResourceGroupId
      SecurityGroupType:
        Ref: SecurityGroupType
      SecurityGroupIngress:
        Ref: SecurityGroupIngress
      Tags:
        Ref: Tags
      SecurityGroupEgress:
        Ref: SecurityGroupEgress
Outputs:
  SecurityGroupId:
    Description: generated security group id for security group.
    Value:
      'Fn::GetAtt':
        - SecurityGroup
        - SecurityGroupId
```


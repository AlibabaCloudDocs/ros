# ALIYUN::VPC::NetworkAcl

ALIYUN::VPC::NetworkAcl类型用于创建网络ACL（Network Access Control List）。

## 语法

```
{
  "Type": "ALIYUN::VPC::NetworkAcl",
  "Properties": {
    "NetworkAclName": String,
    "Description": String,
    "VpcId": String,
    "EgressAclEntries": List,
    "IngressAclEntries": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NetworkAclName|String|否|是|网络ACL的名称。|长度为2~128个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|
|Description|String|否|是|网络ACL的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|VpcId|String|是|否|网络ACL所属的VPC的ID。|如果VPC中含有以下实例规格族中的任一实例，则不支持为该VPC创建网络ACL： ecs.c1、ecs.c2、ecs.c4、ecs.c5、ecs.ce4、ecs.cm4、ecs.d1、ecs.e3、ecs.e4、ecs.ga1、ecs.gn4、ecs.gn5、ecs.i1、ecs.m1、ecs.m2、ecs.mn4、ecs.n1、ecs.n2、ecs.n4、ecs.s1、ecs.s2、ecs.s3、ecs.se1、ecs.sn1、ecs.sn2、ecs.t1、ecs.xn4。如需创建网络ACL，请先升级实例规格。更多信息，请参见[包年包月实例升配规格](/intl.zh-CN/实例/升降配实例/修改实例规格/包年包月实例升配规格.md)和[按量付费实例变配规格](/intl.zh-CN/实例/升降配实例/修改实例规格/按量付费实例变配规格.md)

**说明：** 如果您的VPC中含有实例规格族限制中的任一实例，且您已经创建了网络ACL，为了保证正常使用网络ACL功能，请升级实例规格。 |
|IngressAclEntries|List|否|是|入方向网络ACL规则。|最多支持20个规则。更多信息，请参见[IngressAclEntries属性](#section_qq7_ihy_zp1)。 |
|EgressAclEntries|List|否|是|出方向网络ACL规则。|最多支持20个规则。更多信息，请参见[EgressAclEntries属性](#section_d1h_knm_jrx)。 |

## IngressAclEntries语法

```
"IngressAclEntries": [
  {
    "Policy": String,
    "Description": String,
    "EntryType": String,
    "SourceCidrIp": String,
    "Port": String,
    "Protocol": String,
    "NetworkAclEntryName": String
  }
]
```

## IngressAclEntries属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Policy|String|是|是|授权策略。|取值：-   accept：允许。
-   drop：拒绝。 |
|Description|String|否|是|入方向规则的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|EntryType|String|否|是|规则类型。|取值：-   custom（默认值）：自定义规则。
-   system：系统规则。 |
|SourceCidrIp|String|否|是|源地址网段。|无|
|Port|String|是|是|源端口范围。|无|
|Protocol|String|是|是|传输层协议。|取值：-   icmp
-   gre
-   tcp
-   udp
-   all |
|NetworkAclEntryName|String|否|是|入方向规则的名称。|无|

## EgressAclEntries语法

```
"EgressAclEntries": [
  {
    "Policy": String,
    "Description": String,
    "EntryType": String,
    "DestinationCidrIp": String,
    "Port": String,
    "Protocol": String,
    "NetworkAclEntryName": String
  }
]
```

## EgressAclEntries属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Policy|String|是|是|授权策略。|取值：-   accept：允许。
-   drop：拒绝。 |
|Description|String|否|是|出方向规则的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，不能以`http://`或`https://`开头。|
|EntryType|String|否|是|规则类型。|取值：-   custom（默认值）：自定义规则。
-   system：系统规则。 |
|DestinationCidrIp|String|否|是|目标地址网段。|无|
|Port|String|是|是|目的端口范围。|无|
|Protocol|String|是|是|传输层协议。|取值：-   icmp
-   gre
-   tcp
-   udp
-   all |
|NetworkAclEntryName|String|否|是|出方向规则的名称。|无|

## 返回值

Fn::GetAtt

-   NetworkAclId：网络ACL的ID。
-   NetworkAclEntryName：网络ACL规则名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "IngressAclEntries": {
      "Type": "Json",
      "Description": "The list of ingress network ACL entries.",
      "MaxLength": 20
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the network ACL.\nThe description must be 2 to 256 characters in length. The description must start\nwith a letter but cannot start with http:// or https://."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the virtual private cloud (VPC) to which the network ACL belongs."
    },
    "EgressAclEntries": {
      "Type": "Json",
      "Description": "The list of egress network ACL entries.",
      "MaxLength": 20
    },
    "NetworkAclName": {
      "Type": "String",
      "Description": "The name of the network ACL.\nThe name must be 2 to 128 characters in length and can contain letters, digits, periods\n(.), underscores (_), and hyphens (-). The name must start with a letter and cannot\nstart with http:// or https://."
    }
  },
  "Resources": {
    "NetworkAcl": {
      "Type": "ALIYUN::VPC::NetworkAcl",
      "Properties": {
        "IngressAclEntries": {
          "Ref": "IngressAclEntries"
        },
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "EgressAclEntries": {
          "Ref": "EgressAclEntries"
        },
        "NetworkAclName": {
          "Ref": "NetworkAclName"
        }
      }
    }
  },
  "Outputs": {
    "NetworkAclId": {
      "Description": "The ID of the network ACL.",
      "Value": {
        "Fn::GetAtt": [
          "NetworkAcl",
          "NetworkAclId"
        ]
      }
    },
    "NetworkAclEntryName": {
      "Description": "The name of the inbound rule.",
      "Value": {
        "Fn::GetAtt": [
          "NetworkAcl",
          "NetworkAclEntryName"
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
    Description: 'The description of the network ACL.

      The description must be 2 to 256 characters in length. The description must
      start

      with a letter but cannot start with http:// or https://.'
    Type: String
  EgressAclEntries:
    Description: The list of egress network ACL entries.
    MaxLength: 20
    Type: Json
  IngressAclEntries:
    Description: The list of ingress network ACL entries.
    MaxLength: 20
    Type: Json
  NetworkAclName:
    Description: 'The name of the network ACL.

      The name must be 2 to 128 characters in length and can contain letters, digits,
      periods

      (.), underscores (_), and hyphens (-). The name must start with a letter and
      cannot

      start with http:// or https://.'
    Type: String
  VpcId:
    Description: The ID of the virtual private cloud (VPC) to which the network ACL
      belongs.
    Type: String
Resources:
  NetworkAcl:
    Properties:
      Description:
        Ref: Description
      EgressAclEntries:
        Ref: EgressAclEntries
      IngressAclEntries:
        Ref: IngressAclEntries
      NetworkAclName:
        Ref: NetworkAclName
      VpcId:
        Ref: VpcId
    Type: ALIYUN::VPC::NetworkAcl
Outputs:
  NetworkAclEntryName:
    Description: The name of the inbound rule.
    Value:
      Fn::GetAtt:
      - NetworkAcl
      - NetworkAclEntryName
  NetworkAclId:
    Description: The ID of the network ACL.
    Value:
      Fn::GetAtt:
      - NetworkAcl
      - NetworkAclId
```


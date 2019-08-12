# ALIYUN::MEMCACHE::Instance {#concept_48456_zh .concept}

ALIYUN::MEMCACHE::Instance 类型用于创建 Memcache 实例。

## 语法 {#section_ysq_3m1_mfb .section}

```language-json
{
    "Type" : "ALIYUN::MEMCACHE::Instance",
    "Properties" : {
         "VpcId" : String,
         "Capacity" : Integer,
         "PrivateIpAddr" : String,
         "ZoneId" : String,
         "SecurityIPArray" : String,
         "VSwitchId" : String,
         "NetworkType" : String,
         "Password" : String,
         "InstanceName" : String
    }
}

```

## 属性 { .section}

|属性名称|类型|必须|描述|约束|
|Capacity|integer|是|指定存储空间|取值范围是：1024MB-32GB。允许可选值是1024MB, 2048MB, 4096MB, 8192MB, 16384MB, 32768MB，单位是 MB。|
|Password|string|是|密码|长度：8～30 个字符，需同时包含大写字母、小写字母和数字。|
|VpcId|string|否|指定专有网络的 ID|无|
|PrivateIpAddr|string|否|指定专有网络下的私有 IP 地址|私有 IP 地址必须属于 VpcId 和 VSwitchId 指定的网段。|
|ZoneId|string|否|指定可用区|无|
|SecurityIPArray|string|否|指定可访问该实例的 IP 名单|以逗号隔开，不可重复，最多 1000 个；支持格式：%，0.0.0.0/0，10.23.12.24（IP），或者10.23.12.24/24（CIDR模式，无类域间路由，/24表示了地址中前缀的长度，范围\[1,32\]）。0.0.0.0/0，表示不限制。默认不限制|
|VSwitchId|string|否|指定 VpcId 下的虚拟网络交换机 ID|无|
|NetworkType|string|否|指定网络类型|可选值：CLASSIC 和 VPC。|
|InstanceName|string|否|指定实例的名称|长度为 128 个字符。|

## 返回值 { .section}

**Fn::GetAtt**

-   InstanceStatus：所创建实例的状态。
-   InstanceId：所创建实例的 ID。
-   ConnectionDomain：用于连接实例的域名。
-   QPS：此实例的峰值 QPS。
-   InstanceName：此实例的名称。
-   PrivateIpAddress：VPC 网络下此实例的 IP 地址，经典网络没有私网 IP 地址。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "OcsInstance": {
      "Type": "ALIYUN::MEMCACHE::Instance",
      "Properties": {
        "Password": "YU76sdfsfdUY",
        "Capacity": 1024,
        "VpcId": "vpc-25o8sqkwb",
        "VSwitchId": "vsw-25rc1y5t9",
        "ZoneId": "cn-beijing-c"
      }
    }
  }，
  "Outputs": {
    "ConnectionDomain": {
      "Description": "内网连接字符串",
      "Value": {
        "Fn::GetAtt": [
          "OcsInstance",
          "ConnectionDomain"
        ]
      }
    },
    "PrivateIpAddress": {
      "Description": "内网ip",
      "Value": {
        "Fn::GetAtt": [
          "OcsInstance",
          "PrivateIpAddress"
        ]
      }
    }
  }
}

```


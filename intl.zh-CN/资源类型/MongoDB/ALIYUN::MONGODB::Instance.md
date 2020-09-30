# ALIYUN::MONGODB::Instance

ALIYUN::MONGODB::Instance类型用于创建MongoDB副本集实例，同时也可用于克隆MongoDB副本集实例。

## 语法

```
{
  "Type": "ALIYUN::MONGODB::Instance",
  "Properties": {
    "DatabaseNames": String,
    "VpcPasswordFree": Boolean,
    "ReadonlyReplicas": Integer,
    "BusinessInfo": String,
    "AccountPassword": String,
    "VpcId": String,
    "AutoRenew": Boolean,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "StorageEngine": String,
    "SrcDBInstanceId": String,
    "ReplicationFactor": Integer,
    "ZoneId": String,
    "EngineVersion": String,
    "RestoreTime": String,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "CouponNo": String,
    "Period": Integer,
    "SecurityIPArray": String,
    "ChargeType": String,
    "BackupId": String,
    "DBInstanceClass": String,
    "NetworkType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcPasswordFree|Boolean|否|否|是否为VPC网络中访问该实例启用免密码。|取值： -   true
-   false |
|DBInstanceStorage|Integer|是|否|数据库实例的大小|取值范围：5~1000，必须是5的倍数。

 单位：GB。|
|DBInstanceClass|String|是|否|实例规格|详情请参见[实例规格表](/intl.zh-CN/产品简介/实例规格表.md)。|
|SrcDBInstanceId|String|否|否|源实例ID|只有当调用本接口进行克隆实例时，才能指定此参数，且必须和BackupId或RestoreTime参数一同指定。|
|DBInstanceDescription|String|否|否|实例名称。|-   长度为2~256个字符。
-   以中文字符或英文字符，可包含中文字符、英文字符、数字、下划线（\_）和短划线（-）。 |
|SecurityIPArray|String|否|否|所有可以访问该实例的IP名单|IP地址以英文逗号（,）隔开，不可重复，最多支持1000个。

 支持格式：0.0.0.0/0、10.23.XX.XX（IP）或者10.23.XX.XX/24（CIDR模式，无类域间路由。/24表示地址中前缀的长度，取值范围：1~32）。

 默认值：0.0.0.0/0，表示不指定IP白名单，即所有IP均可访问。 |
|ZoneId|String|否|否|可用区ID|详情请参见[DescribeRegions](/intl.zh-CN/API参考/区域管理/DescribeRegions.md)。在专有网络下，此参数取值需与VSwitchId的可用区保持一致。|
|VpcId|String|否|否|专有网络ID|只有当NetworkType取值为VPC时，此参数为有效参数。|
|VSwitchId|String|否|否|VPC下的虚拟交换机ID|只有当NetworkType取值为VPC时，此参数为有效参数。|
|BackupId|String|否|否|备份集ID|只有调用本接口用于克隆实例时才能指定该参数，且必须和SrcDBInstanceId参数一同指定。|
|NetworkType|String|否|否|网络类型|取值： -   CLASSIC（默认值）
-   VPC |
|AccountPassword|String|否|否|Root用户的密码|-   长度为8~32个字符。
-   可包含英文字符、数字和以下特殊字符：

    ```
!#$%^&*()_+-=
    ``` |
|EngineVersion|String|否|否|数据库版本号|取值： -   3.2
-   3.4（默认值）
-   4.0 |
|StorageEngine|String|否|否|存储引擎|关于存储引擎与版本选择的约束详情，请参见[版本及存储引擎](/intl.zh-CN/产品简介/版本及存储引擎.md)。 取值：

-   WiredTiger（默认值）
-   RocksDB
-   TerarkDB |
|ReplicationFactor|Integer|否|否|副本集节点数|取值： -   3（默认值）
-   5
-   7 |
|DatabaseNames|String|否|否|数据库名|无|
|ReadonlyReplicas|Integer|否|否|只读节点的数量|取值： -   1
-   2
-   3
-   4
-   5 |
|BusinessInfo|String|否|否|业务信息|此参数为附加参数|
|ResourceGroupId|String|否|否|资源组的ID|无|
|AutoRenew|Boolean|否|否|是否为实例启用自动续费|取值： -   true：自动续费
-   false（默认值）：手动续费 |
|RestoreTime|String|否|否|克隆实例时所恢复数据的时间点|格式：yyyy-MM-ddTHH:mm:ssZ（UTC时间）。 只有调用本接口进行克隆实例时，才能指定此参数，且必须和SrcDBInstanceId、BackupId参数一同指定。支持选择7天内的任一时间点进行克隆。 |
|CouponNo|String|否|否|优惠券代码|默认值：youhuiquan\_promotion\_option\_id\_for\_blank。|
|Period|Integer|否|否|实例的购买时长|单位：月。 取值：1、2、3、4、5、6、7、8、9、12、24、36。

 默认值：1。

 只有当ChargeType取值为PrePaid时，此参数为有效参数。 |
|ChargeType|String|否|否|实例的付费类型|取值： -   PostPaid：按量付费
-   PrePaid：预付费 |

## 返回值

Fn::GetAtt

-   OrderId：创建MongoDB实例的订单ID。
-   DBInstanceId：MongoDB实例ID，全局唯一。
-   DBInstanceStatus：MongoDB实例的状态信息。
-   ConnectionURI：连接URI。
-   ReplicaSetName：副本集名称。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MongoDB": {
      "Type": "ALIYUN::MONGODB::Instance",
      "Properties": {
        "DBInstanceClass":"dds.mongo.mid",
        "DBInstanceStorage":"10",
        "VpcId": "vpc-25o8s****",
        "VSwitchId": "vsw-25w8q****"
      }
    }
  },
  "Outputs": {
    "DBInstanceStatus": {
      "Description": "Status of mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDB",
          "DBInstanceStatus"
        ]
      }
    },
    "InstanceId": {
      "Description": "The instance id of created mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDB",
          "DBInstanceId"
        ]
      }
    }
  }
}
```


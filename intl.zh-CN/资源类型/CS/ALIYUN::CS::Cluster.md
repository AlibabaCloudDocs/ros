# ALIYUN::CS::Cluster {#concept_48439_zh .concept}

ALIYUN::CS::Cluster 类型用于创建阿里云 Docker 集群。

## 语法 {#section_cnd_4d1_mfb .section}

```language-json
{
  "Type": "ALIYUN::CS::Cluster",
  "Properties": {
    "SystemDiskCategory": String,
    "VpcId": String,
    "Name": String,
    "DataDiskCategory": String,
    "Password": String,
    "ZoneId": String,
    "ImageId": String,
    "VSwitchId": String,
    "SubnetCidr": String,
    "DataDiskSize": Integer,
    "IoOptimized": Boolean,
    "CreateSlbByDefault": Boolean,
    "InstanceType": String,
    "InstanceIds": List,
    "Size": Integer
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|否|指定 Docker 集群的名称。|名称为 1-64 个字符，可包含数字、汉字、英文字符或连字符（-）。|
|InstanceType|String|否|否|指定创建 Docker 集群所用 ECS 的规格。|无|
|Size|Integer|是|否|指定集群使用多少台 ECS 实例。|无|
|VpcId|String|否|否|指定专有网络 ID。|无|
|ImageId|String|否|否|指定 ECS 实例所用的镜像 ID 。|无|
|VSwitchId|String|否|否|指定专有网络下的交换机 ID。|无|
|SubnetCidr|String|否|否|指定 Docker 容器的子网地址。|允许的子网段为：172.17.XX.XX/24 - 172.31.XX.XX/24。确保此网段不能和专有网络网段相同。|
|Password|String|是|否|指定 ECS 实例的登录密码。|实例的密码。8-30 个字符，同时包含大小写字母和数字，不支持特殊符号。|
|ZoneId|String|否|否|可用区 ID。|无|
|SystemDiskCategory|String|否|否|指定系统盘类型。| 可选值：cloud、cloud\_efficiency、cloud\_ssd、 ephemeral\_ssd。

 默认值：cloud。

 |
|DataDiskCategory|String|否|否|指定数据盘类型。| 可选值：cloud、cloud\_efficiency、cloud\_ssd、 ephemeral\_ssd。

 默认值：cloud。

 |
|DataDiskSize|Integer|否|否|数据盘大小。|单位：GB。|
|IoOptimized|Boolean|否|否|创建的 ECS 是否 I/O 优化。| 可选值：true 和 false。

 默认值：false。

 |
|CreateSlbByDefault|Boolean|否|否|指定是否给 Docker 集群创建负载均衡。| 可选值：true 和 false。

 默认值：false。

 |
|InstanceIds|List|否|否|创建 Docker 集群的 ECS 实例列表。|列表中的 ID 以逗号分隔。当指定 InstanceType 的时候，该值将被忽略。当该值指定时，Size 属性为列表中 ID 的个数和其他属性都会被忽略。所有 ID 对应的 ECS 实例的系统盘都会被替换。指定该值创建 Docker 集群时，请确保系统盘的中的数据已经备份。|

## 返回值 { .section}

**Fn::GetAtt**

-   MasterUrl：集群的主 URL 地址。
-   Ca：CA 证书。
-   ClusterId：集群 ID。
-   Cert：客户端证书。
-   Key：客户端主键。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MyCluster": {
      "Properties": {
        "InstanceType": "ecs.s1.small",
        "Name": "stormcluster",
        "Password": "Test****",
        "Size": "1"
      },
      "Type": "ALIYUN::CS::Cluster"
    }
  },
  "Outputs": {
    "CaCert": {
      "Description": "CA cert of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "MyCluster",
          "Ca"
        ]
      }
    },
    "ClientCert": {
      "Description": "Client cert of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "MyCluster",
          "Cert"
        ]
      }
    },
    "ClientKey": {
      "Description": "Client key of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "MyCluster",
          "Key"
        ]
      }
    },
    "ClusterId": {
      "Description": "Id of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "MyCluster",
          "ClusterId"
        ]
      }
    },
    "Endpoints": {
      "Description": "Endpoints of the app.",
      "Value": {
        "Fn::GetAtt": [
          "App",
          "Endpoints"
        ]
      }
    },
    "MasterUrl": {
      "Description": "Master url of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "MyCluster",
          "MasterUrl"
        ]
      }
    }
  }
}
```


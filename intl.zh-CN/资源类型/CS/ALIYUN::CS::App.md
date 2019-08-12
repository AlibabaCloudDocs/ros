# ALIYUN::CS::App {#concept_48453_zh .concept}

ALIYUN::CS::App 类型用于创建基于 ALIYUN::CS::Cluster 的应用。

## 语法 {#section_yqz_3d1_mfb .section}

```language-json
{
  "Type": "ALIYUN::CS::App",
  "Properties": {
    "Name": String,
    "Ca": String,
    "ClusterId": String,
    "Environment": Map,
    "Cert": String,
    "Version": String,
    "MasterUrl": String,
    "Key": String,
    "Template": String,
    "Description": String
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|否|指定应用的名称。|无|
|ClusterId|String|是|否|指定集群的 ID。|无|
|MasterUrl|String|是|否|指定集群的主 URL 地址。|无|
|Ca|String|否|否|指定集群的 CA 证书。|无|
|Environment|Map|否|否|指定环境变量。|无|
|Cert|String|否|否|指定集群的客户端证书。|无|
|Version|String|否|否|指定应用的版本号。|无|
|Key|String|否|否|指定集群的客户端主键。|无|
|Template|String|否|否|指定部署 Docker 应用的模版。|无|
|Description|String|否|否|指定应用的描述。|长度为 2-256 个字符，默认为空。|

## 返回值 { .section}

**Fn::GetAtt**

Endpoints：访问应用的域名。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "App": {
      "Properties": {
        "Ca": {
          "Fn::GetAtt": [
            "MyCluster",
            "Ca"
          ]
        },
        "Cert": {
          "Fn::GetAtt": [
            "MyCluster",
            "Cert"
          ]
        },
        "ClusterId": {
          "Fn::GetAtt": [
            "MyCluster",
            "ClusterId"
          ]
        },
        "Key": {
          "Fn::GetAtt": [
            "MyCluster",
            "Key"
          ]
        },
        "MasterUrl": {
          "Fn::GetAtt": [
            "MyCluster",
            "MasterUrl"
          ]
        },
        "Name": "ngix",
        "Template": {"Fn::Join": ["\\n", [
             "mysql:",
             "  environment:",
             "    - MYSQL_MAJOR=5.6",
             "    - MYSQL_ROOT_PASSWORD=password",
             "  expose:",
             "    - 3306/tcp",
             "  image: 'registry.aliyuncs.com/acs-sample/mysql:5.6'",
             "  labels:",
             "    aliyun.routing.port_3306: nnn;http://nn.abc.com",
             "    aliyun.scale: '3'",
             "  restart: always",
             "  volumes:",
             "    - /var/lib/mysql"
         ]]}
      },
      "Type": "ALIYUN::CS::App"
    },
    "MyCluster": {
      "Properties": {
        "InstanceType": "ecs.s1.small",
        "Name": "mysqlcluster",
        "Password": "Test****",
        "Size": 3
      },
      "Type": "ALIYUN::CS::Cluster"
    }
  },
  "Outputs": {
    "Endpoints": {
      "Description": "Endpoints of the app.",
      "Value": {
        "Fn::GetAtt": [
          "App",
          "Endpoints"
        ]
      }
    }
  }
}			
```


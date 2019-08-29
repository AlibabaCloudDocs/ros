# ALIYUN::CS::App {#concept_48453_zh .concept}

ALIYUN::CS::App is used to create an application based on ALIYUN::CS::Cluster.

## Syntax {#section_yqz_3d1_mfb .section}

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
    "Template" : String,
    "Description": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description |Validity|
|----|----|--------|--------|------------|--------|
|Name|String|Yes|No|The name of the application to be created.|None|
|ClusterId|String |Yes|No|The ID of the cluster where the application resides.|None|
|MasterUrl|String |Yes|No|The master URL of the specified cluster.|None|
|Ca|String|No|No|The CA certificate of the specified cluster.|None|
|Environment|Map|No|No|The application environment variables.|None|
|Cert|String|No|No|The client certificate of the specified cluster.|None|
|Version|String|No|No|The version of the application.|None|
|Key|String|No|No|The client primary key used to identify the cluster.|None|
|Template|String|No|No|The template used to deploy the Docker application.|None|
|Description|String|No|No|The description of the application.|The description must be 2 to 256 characters in length. This parameter is empty by default.|

## Response parameters { .section}

**Fn::GetAtt**

Endpoints: the endpoints used to access the application.

## Examples { .section}

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


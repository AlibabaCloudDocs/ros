# ALIYUN::CS::Cluster {#concept_48439_zh .concept}

ALIYUN::CS::Cluster is used to create an Alibaba Cloud Docker cluster.

## Syntax {#section_cnd_4d1_mfb .section}

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

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Name|String|Yes|No|The name of the Docker cluster to be created.|The name must be 1 to 64 characters in length and can contain letters, digits, and hyphens \(-\).|
|InstanceType|String|No|No|The ECS instance type used to create the Docker cluster.|None|
|Size |Integer|Yes|No|The number of ECS instances to be contained in the Docker cluster.|None|
|VpcId|String|No|No|The ID of the VPC to which the Docker cluster belongs.|None|
|ImageId|String|No|No|The ID of the image used by the contained ECS instances.|None|
|VSwitchId|String|No|No|The ID of the VSwitch for the specified VPC.|None|
|SubnetCidr|String|No|No|The subnet CIDR block of the Docker cluster.|The allowed subnet CIDR block ranges from 172.17.0.0/24 to 172.31.0.0/24. Make sure that the subnet CIDR block is different from that of the VPC.|
|Password|String|Yes|No|The password used to log on to an ECS instance.|The password must be 8 to 30 characters in length and can contain letters and digits. It cannot contain any special characters.|
|ZoneId|String|No|No|The ID of the zone where the Docker cluster resides.|None|
|SystemDiskCategory|String|No|No|The type of a system disk.| Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd.

 Default value: cloud.

 |
|DataDiskCategory|String|No|No|The type of a data disk.| Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd.

 Default value: cloud.

 |
|DataDiskSize|Integer|No|No|The size of the data disk.|Unit: GB.|
|IoOptimized|Boolean|No|No|Indicates whether a created ECS instance is I/O optimized.| Valid values: true and false.

 Default value: false.

 |
|CreateSlbByDefault|Boolean|No|No|Indicates whether to create a Server Load Balancer \(SLB\) instance for the Docker cluster.| Valid values: true and false.

 Default value: false.

 |
|InstanceIds|List|No|No|The list of IDs of ECS instances used to create the Docker cluster.|IDs in the list are separated by commas \(,\). This parameter is ignored if the InstanceType parameter is set. If this parameter is set, other properties of ALIYUN::CS::Cluster are ignored, except for the Size property that indicates the number of IDs in the list. System disks of all ECS instances corresponding to the IDs are replaced. Before you set this parameter when creating a Docker cluster, ensure that data in the system disks has been backed up.|

## Response parameters { .section}

**Fn::GetAtt**

-   MasterUrl: the master URL of the cluster.
-   Ca: the CA certificate.
-   ClusterId: the ID of the cluster.
-   Cert: the client certificate.
-   Key: the client primary key.

## Examples { .section}

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


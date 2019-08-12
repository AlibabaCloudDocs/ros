# ALIYUN::ECS::CustomImage {#concept_55980_zh .concept}

ALIYUN::ECS::CustomImage 类型用于创建自定义镜像。

## 语法 { .section}

```language-json
{
  "Type": "ALIYUN::ECS::CustomImage",
  "Properties": {
    "Description": String,
    "InstanceId": String,
    "ImageName": String,
    "ImageVersion": String,
    "SnapshotId": String,
    "Tag": List,
    "ResourceGroupId": String,
    "Platform": String,
    "DiskDeviceMapping": List,
    "Architecture": String
  }
}
```

## 属性 { .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|Description|String|否|否|镜像的描述。|长度限制在 256 个字符内。默认值为空。不能以 http:// 和 https:// 开头。|
|InstanceId|String|否|否|实例 ID。|指定该参数则表示[使用实例创建自定义镜像](https://www.alibabacloud.com/help/doc-detail/35109.htm)。|
|ImageName|String|否|否|镜像名称。|长度为 \[2, 128\]。必须以大小字母或中文开头，可包含字母、汉字、数字、下划线（\_）和连字符（-）。不能以 http:// 和 https:// 开头。|
|ImageVersion|String|否|否|镜像版本号。|长度为\[1, 40\]。|
|SnapshotId|String|否|否|快照 ID。| -   指定该参数则表示[使用快照创建自定义镜像](https://www.alibabacloud.com/help/doc-detail/25460.htm)。

 -   如果同时指定该参数和InstanceId，则该参数将被忽略，系统会使用实例创建自定义镜像。

 |
|Tag|List|否|否|标签。|无|
|ResourceGroupId|String|否|否|自定义镜像所在的企业资源组 ID。|无|
|Platform|String|否|否|指定数据盘快照做镜像的系统盘后，需要通过Platform确定系统盘的的操作系统发行版。|无|
|DiskDeviceMapping|List|否|否|镜像和快照的关系。|无|
|Architecture|String|否|否|指定数据盘快照做镜像的系统盘后，需要通过Architecture确定系统盘的系统架构。|取值范围： -   i386
-   x86\_64（默认）

 |

## Tag语法 {#section_0mx_ilv_77x .section}

``` {#codeblock_8k8_q7m_kv3 .language-json}
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag属性 { .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|Key|String|否|否|镜像的标签键。|一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。|
|Value|String|否|否|镜像的标签值。|一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。|

## DiskDeviceMapping { .section}

```language-json
"DiskDeviceMapping": [
  {
    "Device": String,
    "SnapshotId": String,
    "Size": Integer,
    "DiskType": String
  }
]
```

## DiskDeviceMapping属性 { .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|Device|String|否|否|指定 DiskDeviceMapping在自定义镜像中的设备名称。|取值范围：/dev/xvda~/dev/xvdz|
|SnapshotId|String|否|否|根据指定的快照创建自定义镜像。|无|
|Size|Integer|否|否| DiskDeviceMapping磁盘的大小，单位为GiB。

 | 取值范围：5~2000。

-   如果不指定磁盘大小，默认为快照（DiskDeviceMapping.N.SnapshotId）的大小。
-   如果没有指定快照（DiskDeviceMapping.N.SnapshotId），默认磁盘大小为5 GiB。
-   如果指定了磁盘大小，必须大于等于对应快照（DiskDeviceMapping.N.SnapshotId）的大小。

 |
|DiskType|String|否|否|指定DiskDeviceMapping在新镜像中的磁盘类型。您可以通过该参数使用数据盘快照做为镜像的系统盘，如果不指定，默认为快照对应的磁盘类型。| 取值范围：

 -   system：系统盘。
-   data：数据盘。

 |

## 返回值 { .section}

 **Fn::GetAtt** 

ImageId：自定义镜像 ID。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "VpcId": "vpc-2zevx9ios1rszqv0a****",
        "MinAmount": 1,
        "SecurityGroupId": "sg-2ze7pxymaix640qr****",
        "ImageId": {
          "Ref": "CustomImage"
        },
        "IoOptimized": "optimized",
        "SystemDisk_Description": "SystemDisk.Description",
        "SystemDisk_DiskName": "SystemDisk.DiskName",
        "SystemDisk_Category": "cloud_ssd",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec****",
        "Password": "Wenqiao****",
        "InstanceType": "ecs.n1.medium",
        "MaxAmount": 1
      }
    },
    "CustomImage": {
      "Type": "ALIYUN::ECS::CustomImage",
      "Properties": {
        "InstanceId": "i-2zefq1f3ynnrr89q****",
        "SnapshotId": "s-2ze0ibk1pvak4mw6****",
        "ImageName": "image-test-****",
        "ImageVersion": "verison-6-1"
      }
    }
  },
  "Outputs": {
    "CustomImage": {
      "Value": {
        "Fn::GetAtt": [
          "CustomImage",
          "ImageId"
        ]
      }
    },
    "InstanceIds": {
      "Value": {
        "Fn::GetAtt": [
          "WebServer",
          "InstanceIds"
        ]
      }
    }
  }
}            
```


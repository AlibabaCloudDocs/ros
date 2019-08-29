# ALIYUN::SLS::MachineGroup {#concept_48491_zh .concept}

ALIYUN::SLS::MachineGroup 类型用于创建所有需要通过 Logtail 客户端收集日志的日志服务 ECS 机器组。

## 语法 {#section_oh1_cd1_mfb .section}

```language-json
{
  "Type": "ALIYUN::SLS::MachineGroup",
  "Properties": {
    "GroupType": String,
    "ProjectName": String,
    "MachineList": List,
    "GroupName": String,
    "MachineIdentifyType": String,
    "GroupAttribute": String
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupType|String|否|否|机器组类型。|可选值: 空 或 Armory。|
|ProjectName|String|否|否|日志服务项目名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点号（.）和连字符（-）。|
|MachineList|List|否|否|机器 IP 或者自定义的标签。|IP 使用 ECS 内网 IP。请勿把 Windows 云主机和Linux 云主机添加到同一机器组。|
|GroupName|String|否|否|机器组名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点号（.）和连字符（-）。|
|MachineIdentifyType|String|否|否|机器识别类型。|可选值：ip 和 userdefined。|
|GroupAttribute|String|否|否|机器组的属性。|无|

## 返回值 { .section}

**Fn::GetAtt**

-   ProjectName：日志服务项目名称。
-   GroupName：日志服务机器组名称。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MachineGroup": {
      "Type": "ALIYUN::SLS::MachineGroup",
      "Properties": {
        "ProjectName": "rostest-beijing",
        "GroupName": "machine-group-test2",
        "GroupType": "",
        "MachineIdentifyType": "ip",
        "GroupAttribute": '{
                "groupTopic": "testtopic",
                "externalName": "testgroup"
            }',
        "MachineList": ['192.168.XX.XX']
      }
    }
  },
  "Outputs": {
    "ProjectName": {
         "Value": {"Fn::GetAttr": ["MachineGroup","ProjectName"]}
    },
	"GroupName": {
         "Value": {"Fn::GetAttr": ["MachineGroup","GroupName"]}
    }
  }
}			
```


# ALIYUN::ECS::SNatEntry {#concept_48475_zh .concept}

ALIYUN::ECS::SNatEntry 类型用于配置 NAT 网关中的源地址转换表。

## 语法 {#section_mqx_ccf_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::SNatEntry",
  "Properties": {
    "SNatTableId": String,
    "SNatIp": String,
    "SourceVSwitchId": String
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SNatTableId|string|是|是|指定源地址转换表 ID。|无|
|SNatIp|string|是|是|用于源地址转换的公网 IP。|必须是 NAT 网关中带宽包的 IP；每个 NAT Gateway上的公网IP，不能既存在于端口转发表中，也存在于 SNAT 表中。|
|SourceVSwitchId|string|是|是|可通过 NAT 网关的 SNAT 功能访问互联网的 ECS 实例所在的 VSwitch ID。|无|

## 返回值 { .section}

**Fn::GetAtt**

SNatEntryId：源地址转换表中的表项 ID。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SNatEntry": {
      "Type": "ALIYUN::ECS::SNatEntry",
      "Properties": {
        "SNatTableId": "stb-3er41e05p",
        "SourceVSwitchId": "vsw-25rc1****",
        "SNatIp": "101.201.XX.XX"
      }
    }
  },
  "Outputs": {
    "SNatEntryId": {
         "Value": {"Fn::GetAttr": ["SNatEntry","SNatEntryId"]}
    }
}
```


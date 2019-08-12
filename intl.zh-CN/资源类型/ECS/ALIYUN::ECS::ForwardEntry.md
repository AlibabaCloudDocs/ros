# ALIYUN::ECS::ForwardEntry {#concept_e1p_j12_lfb .concept}

ALIYUN::ECS::ForwardEntry 类型用于配置 NAT 网关的DNAT表。

## 语法 {#section_vds_412_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::ForwardEntry",
  "Properties": {
    "ExternalIp": String,
    "ExternalPort": String,
    "ForwardTableId": String,
    "InternalIp": String,
    "IpProtocol": String,
    "InternalPort": String,
  }
}
```

## 属性 {#section_pym_y12_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ExternalIp|String|是|否|公网IP。|该 IP 必须已加入该DNAT所属NAT网关上的共享带宽包。|
|ExternalPort|String|是|否|连接公网的端口。|取值范围：\[1, 65535\]。|
|ForwardTableId|String|是|否|DNAT表的 ID。|无。|
|InternalIp|String|是|否|转发请求的目标 IP。|该 IP 是私网 IP。|
|IpProtocol|String|是|否|协议类型。|取值范围：TCP、UDP、 Any。|
|InternalPort|String|是|否|目标私网端口。|取值范围：\[1, 65535\]。|

## 返回值 {#section_q1l_cb2_lfb .section}

**Fn::GetAtt**

ForwardEntryId：DNAT中每一个条目的 ID。

## 示例 {#section_ax4_3b2_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ForwardEntry": {
      "Type": "ALIYUN::ECS::ForwardEntry",
      "Properties": {
        "ForwardTableId": "my_forwardtable",
        "ExternalIp": "101.201.XX.XX",
        "ExternalPort": "8080",
        "IpProtocol": "TCP",
        "InternalIp": "10.2.XX.XX",
        "InternalPort": "80"
      }
    }
  },
  "Outputs": {
    "ForwardEntryId": {
      "Value" : {"Fn::GetAttr": ["ForwardEntry","ForwardEntryId"]}
    }
  }
}
```


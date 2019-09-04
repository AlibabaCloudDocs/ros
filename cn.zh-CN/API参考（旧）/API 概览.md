# API 概览 {#concept_28899_zh .concept}

## 资源栈相关接口 {#section_iq1_jp1_mfb .section}

|URI|Method|描述|
|---|------|--|
|/stacks|POST|[创建资源栈](intl.zh-CN/API参考（旧）/资源栈相关接口/创建资源栈.md#)。|
|/stacks|GET|[查询资源栈列表](intl.zh-CN/API参考（旧）/资源栈相关接口/查询资源栈列表.md#)。|
|/stacks/\{StackName\}/\{StackId\}|GET|[查询资源栈信息](intl.zh-CN/API参考（旧）/资源栈相关接口/查询资源栈信息.md#)。|
|/stacks/\{StackName\}/\{StackId\}|PUT|[更新资源栈](intl.zh-CN/API参考（旧）/资源栈相关接口/更新资源栈.md#)。|
|/stacks/\{StackName\}/\{StackId\}|DELETE|[删除资源栈](intl.zh-CN/API参考（旧）/资源栈相关接口/删除资源栈.md#)。|
|/stacks/\{StackName\}/\{StackId\}/abandon|DELETE|[废弃资源栈](intl.zh-CN/API参考（旧）/资源栈相关接口/废弃资源栈.md#)。|
|/stacks/preview|POST|[预览资源栈](intl.zh-CN/API参考（旧）/资源栈相关接口/预览资源栈.md#)。|

## 资源相关接口 {#section_tmz_mp1_mfb .section}

|URI|Method|描述|
|---|------|--|
|/stacks/\{StackName\}/\{StackId\}/resources|GET|[查询资源列表](intl.zh-CN/API参考（旧）/资源相关接口/查询资源列表.md#)。|
|/stacks/\{StackName\}/\{StackId\}/resources/\{ResourceName\}|GET|[查询资源信息](intl.zh-CN/API参考（旧）/资源相关接口/查询资源详情.md#)。|
|/resource\_types|GET|[查询资源类型列表](intl.zh-CN/API参考（旧）/资源相关接口/查询资源类型列表.md#)。|
|/resource\_types/\{TypeName\}|GET|[查询资源类型信息](intl.zh-CN/API参考（旧）/资源相关接口/查询资源类型信息.md#)。|
|/resource\_types/\{TypeName\}/template|GET|[查询资源类型模板信息](intl.zh-CN/API参考（旧）/资源相关接口/查询资源类型模板信息.md#)。|

## 模板相关接口 {#section_bv1_vp1_mfb .section}

|URI|Method|描述|
|---|------|--|
|/stacks/\{StackName\}/\{StackId\}/template|GET|[查询模板信息](intl.zh-CN/API参考（旧）/模板相关接口/查询模板信息.md#)。|
|/validate|POST|[验证模板信息](intl.zh-CN/API参考（旧）/模板相关接口/验证模板信息.md#)。|

## 其他接口 {#section_vyy_xp1_mfb .section}

|URI|Method|描述|
|---|------|--|
|/stacks/\{StackName\}/\{StackId\}/events|GET|[查询事件列表](intl.zh-CN/API参考（旧）/其他接口/查询事件列表.md#)。|
|/regions|GET|[查询 Region 列表](intl.zh-CN/API参考（旧）/其他接口/查询地域列表.md#)。|


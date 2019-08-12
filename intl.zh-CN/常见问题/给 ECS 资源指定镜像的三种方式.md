# 给 ECS 资源指定镜像的三种方式 {#concept_66902_zh .concept}

当通过资源编排的如下四个资源类型：

-    [ALIYUN::ECS::Instance](../../../../intl.zh-CN/资源类型/ECS/ALIYUN::ECS::Instance.md#) 
-    [ALIYUN::ECS::InstanceClone](../../../../intl.zh-CN/资源类型/ECS/ALIYUN::ECS::InstanceClone.md#) 
-    [ALIYUN::ECS::InstanceGroup](../../../../intl.zh-CN/资源类型/ECS/ALIYUN::ECS::InstanceGroup.md#) 
-    [ALIYUN::ECS::InstanceGroupClone](../../../../intl.zh-CN/资源类型/ECS/ALIYUN::ECS::InstanceGroupClone.md#) 

创建 ECS 时，需要给相应的 ECS 资源指定镜像。在编辑资源栈模板时，可通过以下三种方式去指定 ImageId。

-   直接指定需要的具体镜像 ID
-   通过模糊的方式指定需要的镜像
-   通过镜像参数的 AssociationProperty 属性，选择当前可用的镜像

## 直接指定需要的具体镜像 ID {#section_tht_sxx_kfb .section}

如果明确知道需要的镜像 ID，那么直接指定这个 ImageId 即可。每一个 Region 下，当前用户可用的镜像 ID 都可以在资源编排控制台查到。

1.  登录 [资源编排控制台](http://ros.console.aliyun.com) 。
2.  在左侧导航栏中，单击 **ECS 实例相关信息**，再在页面上单击 **ECS 镜像**。页面上即展示当前用户可用的镜像 ID。![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/66902/cn_zh/1518321425241/%E6%9F%A5%E6%89%BEimage.png)
3.  在模板中，指定 ImageId 为您需要的某个镜像 ID。

    **示例**


```
"ImageId": { "Type": "String", "Description": "Image Id, represents the image resource to startup one ECS instance", "Default": "centos_7_04_64_20G_alibase_201701015.vhd" },
```

## 通过模糊的方式指定需要的镜像 { .section}

如果对镜像的版本没有要求，只需要是 CentOS 或者 Ubuntu 系列就行，那么就可以使用模糊指定的方式指定镜像 ID。资源编排服务会根据输入的镜像值，去匹配最合适的镜像 ID。

 **匹配的规则如下：** 

-   如果只指定镜像的系列，例如 CentOS、 Win、或 Ubuntu，则会匹配当前最高版本的 64 位镜像。
-   如果指定镜像同时指定了镜像的大版本号，例如 CentOS\_6，Ubutun\_14，或 Win2008r2，则会选择在 CentOS 6 中 64 位的最新版本；Ubuntu 14 中 64 位的最新版本；Win2008r2 中 64 位的最新版本。
-   可以使用星号（\*）替代镜像 ID 中的某个字段，例如 centos\_6\_09\_64\_20G\_alibase\*.vhd，则会使用公共镜像中最新的 centos\_6\_09\_64\_20G\_alibase 版本。

    在 ROS 的模板样例中就使用的模糊匹配的方式。很多涉及到指定镜像的地方，都是以 CentOS\_7 或者 Ubuntu\_14 指定。

     **示例** 


```language-json
"ImageId": {
   "Type": "String",
   "Description": "ECS Image",
   "Label": "ECS Image",
   "Default": "centos_7"
 },

```

## 通过镜像参数的 AssociationProperty 属性，选择当前可用的镜像 { .section}

如果通过在模板的[参数（Parameter）](../../../../intl.zh-CN/用户指南/模板语法/参数（Parameters）.md#)段，把 ECS 的镜像 ID 定义成一个参数，则可以在定义参数的时候添加 `AssociationProperty` 来指定。资源编排服务在做参数解析的时候，能自动以列表的形式，展示当前 Region 下有哪些可用的镜像 ID，您只需要选择即可。

使用 `AssociationProperty` 定义参数的示例

```
   "ImageId": {
      "AssociationProperty":"ALIYUN::ECS::Instance:ImageId",
      "Type" : "String",
      "Default": "centos_7_04_64_20G_alibase_201701016.vhd",
      "Description": " 自动获取可选择的镜像 ID"
    }


```

当在资源编排控制台中根据模板创建资源栈时，需要输入镜像 ID 时候，当前 Region 下所有的镜像 ID 都会如下图展示：

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/66902/cn_zh/1518334353137/image_id_%E5%8F%AF%E9%80%89%E5%B1%95%E7%A4%BA.png)

除显示可选镜像参数以外，同时会提示镜像 ID 参数的默认值，或者 AllowedValues 中指定的值是否可用。选择合适的镜像 ID 就可以创建 ECS 资源。


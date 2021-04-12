# 使用Alibaba Cloud Toolkit管理模板及资源栈（IntelliJ IDEA）

在IntelliJ IDEA中安装和配置Alibaba Cloud Toolkit（以下简称Cloud Toolkit）后，您可以通过Alibaba ROS Templates和Alibaba Cloud ROS模块实现对ROS模板及资源栈便捷、高效的管理。

-   下载并安装[JDK1.8或更高版本](https://www.oracle.com/technetwork/java/javase/downloads/index.html)。
-   下载并安装[IntelliJ IDEA（2018.2或更高版本）](https://www.jetbrains.com/idea/download)。
-   已在IntelliJ IDEA中安装和配置Cloud Toolkit，请参见[在IntelliJ IDEA中安装和配置Cloud Toolkit]()。

Cloud Toolkit是一个插件工具，可以帮助开发者更高效地部署、测试、开发和诊断应用。Cloud Toolkit详情，请参见[什么是Alibaba Cloud Toolkit]()。

ROS已经与Cloud Toolkit集成，当您在IntelliJ IDEA中安装和配置Cloud Toolkit后，您可以通过Alibaba ROS Templates模块管理模板，通过Alibaba Cloud ROS模块管理资源栈。

## 使用Alibaba ROS Templates模块管理模板

Alibaba ROS Templates模块通过一个资源配置文件（.ros.config.yml），协助您对模板文件进行管理。

**说明：** .ros.config.yml文件是Alibaba ROS Templates模块用于管理模板的源文件。

1.  在IntelliJ IDEA中打开您的工程。

2.  创建模板。

    -   方法一（推荐）：打开IntelliJ IDEA右边框Alibaba ROS Templates工具，单击**Create**，输入模板的名称，选择模板的类型，创建本地模板。
    -   方法二：在IntelliJ IDEA中右键单击您的工程名称，单击**New** \> **AlibabaCloud ROS YAML Template**或单击**New** \> **AlibabaCloud ROS JSON Template**。

        **说明：** 使用这种方式创建的模板不会被Alibaba ROS Templates模块管理。如需使用Alibaba ROS Templates模块管理，则需要在.ros.config.yml文件中增加模板路径，并将模板移动至JSON和YAML文件夹下。

3.  在Resources参数中输入资源类型。

    -   **AlibabaCloud ROS YAML Template**示例

        ![YAML模板管理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7390919951/p128552.gif)

    -   **AlibabaCloud ROS JSON Template**示例

        ![模板管理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8390919951/p128544.gif)

    **说明：** 使用Ctrl+鼠标左键可实现参数位置与参数之间的跳转，使用Ctrl+鼠标悬浮可显示参数信息。

    模板管理的参数如下表所示：

    |功能|说明|
    |--|--|
    |**Refresh**|刷新目录。|
    |**Create**|创建本地模板。首次使用此插件创建模板默认会创建.ros.config.yml文件及JSON和YAML文件夹。|
    |**Delete**|删除选中模板功能。|
    |**Local Templates**|本地模板虚拟目录。|
    |**Remote Templates**|远端模板虚拟目录。|

4.  右键单击本地模板，可根据需求进行操作。

    ![本地模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8390919951/p128405.png)

    功能操作说明如下：

    -   **Upload**：上传模板。

        **说明：** 上传模板后，本地模板将显示在Alibaba ROS Templates模块的远端模板列表中。

        您可以登录资源编排控制台，单击**模板** \> **我的模板**。当**描述**列显示**--- The template is from Alibaba Cloud Toolkit**时，说明模板通过Cloud Toolkit的Alibaba ROS Templates模块创建。

    -   **Rename**：重命名模板名称。
    -   **Delete**：删除本地模板。
5.  右键单击远端模板，可根据需求进行操作。

    ![远程模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8390919951/p128410.png)

    功能操作说明如下：

    -   **Download**：下载模板。
    -   **Properties**：查看模板属性信息。
    -   **Delete**：删除远端模板。
    **说明：** 双击远端模板，默认会打开一个临时文件，右键菜单单击**Alibaba Cloud ROS** \> **Update Template**，显示对比远端模板修改情况，可更新远端模板。


## 使用Alibaba Cloud ROS模块管理资源栈

Alibaba Cloud ROS模块帮助您便捷地管理远端资源栈（资源编排控制台的资源栈）。

1.  在IntelliJ IDEA中打开您的工程。

2.  在IntelliJ IDEA窗口中单击**Alibaba Cloud View** \> **Alibaba Cloud ROS**，根据您的需求进行相关操作。

    ![alibaba cloud view](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8390919951/p128381.png)

    资源栈管理的参数如下表所示：

    |参数|说明|
    |--|--|
    |**地域**|选择资源栈的所在地域。|
    |**Search**|在当前地域下，搜索资源栈ID或资源栈名称；若未输入，则刷新当前地域资源栈列表。|
    |**Create Stack**|创建资源栈 ，自动跳转至ROS控制台创建资源栈页面。|
    |**Stack ID/Name**|单击名称，显示该资源栈属性信息。|
    |**Status**|显示该资源栈当前状态。|
    |**Create at**|显示该资源栈创建时间。|
    |**Outputs**|显示该资源栈的输出值信息。|
    |**Delete**|删除该资源栈。|
    |**More**|    -   **Properties**：显示该资源栈的属性信息。
    -   **Resources**：显示该资源栈内的所有资源信息。
    -   **Parameters**：显示该资源栈的参数信息。 |


## 联系我们

如果您有相关需求或反馈，可以添加钉钉群联系阿里云支持人员，钉钉群号为11783495。

![客户支持](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0724918161/p262296.jpg)


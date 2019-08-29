# 通过ROS模板一键部署WordPress和phpMyAdmin {#concept_67256_zh .concept}

本文档介绍如何根据一个 ROS 资源栈模板一键部署 WordPress 站点和 phpMyAdmin 应用。

## 背景信息 {#section_k2g_xvc_lfb .section}

如果您只有管理网站内容人员，而无专业技术人员来做网站建立和管理的技术支持，这只适用于基础网站。如果您的网站有更高的需求，需要订制化服务，高可用性和高弹性，您就需要寻求其他解决方案。

本文介绍的 ROS 资源栈模板（[WordPressCluster-phpMyAdmin.ros](http://ros-sample-templates.oss-eu-central-1.aliyuncs.com/WordPressCluster-phpMyAdmin.ros)）可帮助您实现对高可用性和高弹性的需求。通过此模板，您只需单击一键，即能部署整个 VPC 、负载均衡、弹性伸缩、ECS、云数据库 RDS 版等实例组成的资源栈。同时，部署 WordPress 和 phpMyAdmin，并配置弹性伸缩。这样，系统会根据需要，自动添加、配置新的实例，而无须您手动操作。

## 前提条件 { .section}

-   拥有可用的 OSS 存储空间（Bucket）。
-   RAM 用户具有 OSS 存储空间的读、写访问权限。
-   了解 ROS，并能通过 ROS 控制台创建模板和资源栈。

## 架构原理概览 {#section_yd1_q5c_lfb .section}

下图为通过 ROS 资源栈模板（[WordPressCluster-phpMyAdmin.ros](http://ros-sample-templates.oss-eu-central-1.aliyuncs.com/WordPressCluster-phpMyAdmin.ros)） 创建资源栈架构概览图。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23203/155912430848093_zh-CN.png)

有三类用户将会访问这些基础设施：

-   **端用户**

    端用户通过 URL 访问托管在 WordPress 上的网站。

    WordPress 部署在 Apache Web 服务器中。服务器的文档根目录为 `/wwwroot`。根目录所在的 OSS Bucket 是 Web 服务器通过 OSSFS（阿里云官方提供的基于 FUSE 的文件系统）共用的一个存储空间。

    RAM 用户具有 OSS Bucket 的访问权限，可将 OSS Bucket 挂载到 ECS 实例上。

    RDS for MySQL 数据库存放 WordPress 的内容。通过内网连接字符串从 Web 服务器访问数据库。

-   **系统管理员**

    系统管理员通过 SSH 登录 JumpBox （堡垒机），进入 VPC 环境。

    JumpBox 具有弹性公网 IP，可通过 Internet 访问。

    通过 JumpBox 访问可管理 VPC 中的产品实例。

    phpMyAdmin 安装在 JumpBox 上，通过 Internet 访问。

    如此，系统管理员便可管理云数据库 RDS 版。

-   **内容负责人**

    内容负责人可通过 Internet 访问 WordPress 管理控制台。

    所有服务的访问权限可通过安全组，根据环境配置来控制。


## 资源站模板概览 {#section_b21_q5c_lfb .section}

单击 [WordPressCluster-phpMyAdmin.ros](http://ros-sample-templates.oss-eu-central-1.aliyuncs.com/WordPressCluster-phpMyAdmin.ros) 下载该资源栈模板。

**说明：** 本模板中，设置 ZoneId为 eu-central-1a，设置ImageId 为 m-gw8efmfk0y184zs0m0aj。这可能对您不适用。您可以根据您的资源编排控制台中支持的 ECS 可用区和镜像，在模板中修改 ZoneId 和 ImageId。支持的可用区和镜像查询方法：登录 [资源编排控制台](http://ros.console.aliyun.com) ，单击 **ECS 实例相关信息**，选择地域，然后单击 **ECS 可用区** 或 **ECS 镜像**，即可查看支持的可用区或镜像。

根据 WordPressCluster-phpMyAdmin.ros 这个资源栈模板，系统将创建和配置 VPC、负载均衡、VSwitch、NAT 网关、ECS 实例、弹性公网 IP、ECS 实例弹性伸缩和 云数据库 RDS 版实例等。

在创建资源栈时，以下参数可满足任何地域的用户需要。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23203/155912430848094_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23203/155912430848096_zh-CN.png)

根据模板，系统将在 JumpBox 上安装 httpd、mysql-client、PHP、OSSFS、phpMyAdmin、和 WordPress，并通过资源 ALIYUN::ECS::Instance 的 UserData 段配置这些应用。

以下是 UserData 段节选：

```language-json
"ossbucketendpoint=",
 {
 "Ref": "OSSBucketEndPoint"
 },
 "\n",
 "DatabaseUser=",
 {
 "Ref": "MasterUserName"
 },
 "\n",
 "DatabasePwd=",
 {
 "Ref": "MasterDBPassword"
 },
 "\n",
 "DatabaseName=",
 {
 "Ref": "DBName"
 },
 "\n",
 "DatabaseHost=",
 {
 "Fn::GetAtt": ["Database", "InnerConnectionString"]
 },
 "\n",
 "yum install -y curl httpd mysql-server php php-common php-mysql\n",
 "yum install -y php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc\n",
 "yum install -y phpmyadmin\n",
 "sed -i \"s%localhost%$DatabaseHost%\" /etc/phpMyAdmin/config.inc.php\n",
 "sed -i \"s%Deny,Allow%Allow,Deny%\" /etc/httpd/conf.d/phpMyAdmin.conf\n",
 "sed -i \"s%Deny from All%Allow from All%\" /etc/httpd/conf.d/phpMyAdmin.conf\n",
 "sed -i \"/<RequireAny>/a Require all Granted\" /etc/httpd/conf.d/phpMyAdmin.conf\n",
 "chkconfig httpd on\n",
 "service httpd stop\n",
 "wget  
 https://github.com/aliyun/ossfs/releases/download/v1.80.3/ossfs_1.80.3_centos6.5_x86_64.rpm\n",
 "yum install -y ossfs_1.80.3_centos6.5_x86_64.rpm\n",
 "echo $ossbucket:$ossbucketaccesskey:$ossbucketsecret >> /etc/passwd-ossfs\n",
 "chmod 600 /etc/passwd-ossfs\n",
 "mkdir $ossbucketmountpoint\n",
 "chmod -R 755 $ossbucketmountpoint\n",
 "echo #This script will automount the ossbucket\n",
 "echo umount $ossbucketmountpoint >> /usr/local/bin/ossfs-automount.sh\n",
 "echo #Mounting OSS Bucket\n",
            "echo ossfs $ossbucket $ossbucketmountpoint -ourl=http://$ossbucketendpoint -o allow_other -o mp_umask=0022 -ouid=48 -ogid=48 >> /usr/local/bin/ossfs-automount.sh\n",
"chmod 755 /usr/local/bin/ossfs-automount.sh\n",
"echo /usr/local/bin/ossfs-automount.sh >> /etc/rc.d/rc.local\n",
"chmod +x /etc/rc.d/rc.local\n",
"/usr/local/bin/./ossfs-automount.sh\n",
"wget http://WordPress.org/latest.tar.gz\n",
"tar -xzvf latest.tar.gz\n",             
"sed -i \"s%database_name_here%$DatabaseName%\" WordPress/wp-config-sample.php\n",
"sed -i \"s%username_here%$DatabaseUser%\" WordPress/wp-config-sample.php\n",
"sed -i \"s%password_here%${DatabasePwd:-$DatabasePwdDef}%\" WordPress/wp-config-sample.php\n",
"sed -i \"s%localhost%$DatabaseHost%\" WordPress/wp-config-sample.php\n",
"mv WordPress/wp-config-sample.php WordPress/wp-config.php\n",
"cp -a WordPress/* $ossbucketmountpoint\n",
"chmod -R 755 /wwwroot/*\n",
"rm -rf WordPress*\n",
"service httpd start\n",
"done\n"
```

通过 UserData 段，将 WordPress 部署在 OSS Bucket 上。OSS Bucket 可挂载到弹性伸缩创建的 Web 服务器上。如此可保证所有 Web 服务器都具有来自根目录的最新内容。

通过弹性伸缩配置的 UserData 段，实现 httpd、PHP、和 ossutil 的安装和配置，挂载 DocumentRoo，和启动所有服务。

以下是弹性伸缩配置的 UserData 段节选：

```language-json
 "DatabaseHost=",
              {
                "Fn::GetAtt": ["Database", "InnerConnectionString"]
              },
              "\n",
              "yum install -y curl httpd mysql-server php php-common php-mysql\n",
              "yum install -y php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc\n",
              "chkconfig httpd on\n",
              "service httpd stop\n",
              "DocumentRoot='/var/www/html'\n",
              "sed -i \"s%$DocumentRoot%$ossbucketmountpoint%\" /etc/httpd/conf/httpd.conf\n",
              "Directory='/var/www'\n",
              "sed -i \"s%$Directory%$ossbucketmountpoint%\" /etc/httpd/conf/httpd.conf\n",
"wget https://github.com/aliyun/ossfs/releases/download/v1.80.3/ossfs_1.80.3_centos6.5_x86_64.rpm\n",
              "yum install -y ossfs_1.80.3_centos6.5_x86_64.rpm\n",
              "echo $ossbucket:$ossbucketaccesskey:$ossbucketsecret >> /etc/passwd-ossfs\n",
              "chmod 600 /etc/passwd-ossfs\n",
              "mkdir $ossbucketmountpoint\n",
              "chmod -R 755 $ossbucketmountpoint\n",
              "echo #This script will automount the ossbucket\n",
              "echo umount $ossbucketmountpoint >> /usr/local/bin/ossfs-automount.sh\n",
              "echo #Mounting OSS Bucket\n",
              "echo ossfs $ossbucket $ossbucketmountpoint -ourl=http://$ossbucketendpoint -o allow_other -o mp_umask=0022 -ouid=48 -ogid=48 >> /usr/local/bin/ossfs-automount.sh\n",
              "chmod 755 /usr/local/bin/ossfs-automount.sh\n",
              "echo /usr/local/bin/ossfs-automount.sh >> /etc/rc.d/rc.local\n",
              "chmod +x /etc/rc.d/rc.local\n",
              "/usr/local/bin/./ossfs-automount.sh\n",
              "chmod -R 755 /wwwroot/*\n",
              "service httpd start\n",
              "done\n"
            ]
```

## 更多信息 { .section}

-   [创建资源栈](../../../../intl.zh-CN/用户指南/资源栈管理/创建资源栈.md#)
-   [使用可视化编辑器编辑模板](../../../../intl.zh-CN/用户指南/可视化编辑器示例.md#)
-   [通过 RAM 控制资源访问](../../../../intl.zh-CN/快速入门/使用 RAM 控制资源访问.md#)
-   [根据样例模板创建资源栈](../../../../intl.zh-CN/快速入门/通过模板创建资源.md#)


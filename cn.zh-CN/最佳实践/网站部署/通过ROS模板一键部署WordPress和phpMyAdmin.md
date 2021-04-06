# 通过ROS模板一键部署WordPress和phpMyAdmin

本文为您介绍如何使用ROS模板一键部署WordPress站点和phpMyAdmin应用。

## 背景信息

如果您只有管理网站内容的人员，而无专业技术人员来进行网站建立和管理，则只能部署基础网站。如果您的网站有更高的需求，需要定制化服务、高可用性和高弹性，则需寻求其他解决方案。

本文介绍的ROS资源栈模板（WordPressCluster-phpMyAdmin.ros）可以帮助您实现对高可用性和高弹性的需求。通过此模板，您可以快速部署整个VPC、负载均衡、弹性伸缩、ECS、云数据库RDS版等实例组成的资源栈。同时部署WordPress和phpMyAdmin，并配置弹性伸缩。系统会根据需要，自动添加、配置新的实例，无须您手动操作。

## 架构原理概览

下图为通过ROS资源栈模板（WordPressCluster-phpMyAdmin.ros）创建资源栈的架构图。

![framework](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0869919951/p48093.png)

有三类用户将会访问这些基础设施：

-   终端用户：通过URL访问托管在WordPress上的网站。具体如下：
    -   WordPress：部署在Apache Web服务器，服务器的文档根目录为`/wwwroot`。根目录所在的OSS Bucket是Web服务器通过OSSFS（阿里云官方提供的基于FUSE的文件系统）共用的一个存储空间。
    -   RAM用户：具有OSS Bucket的访问权限，可以将OSS Bucket挂载到ECS实例上。
    -   RDS MySQL数据库：存放WordPress的内容。通过内网连接字符串从Web服务器访问数据库。
-   系统管理员：通过SSH登录JumpBox（堡垒机），进入VPC环境。

    JumpBox具有弹性公网IP，通过JumpBox访问可管理VPC中的产品实例。您可以将phpMyAdmin安装在JumpBox上，通过Internet访问JumpBox，从而管理云数据库RDS版。

-   内容负责人：通过Internet访问WordPress管理控制台。

    所有服务的访问权限可通过安全组，根据环境配置来控制。


## 资源站模板概览

单击[WordPressCluster-phpMyAdmin.ros](https://ros-userdata-resources.oss-cn-beijing.aliyuncs.com/WordPress/WordPressCluster-phpMyAdmin.ros)下载该资源栈模板。

**说明：** 您可以根据资源编排控制台中支持的ECS可用区和镜像，在模板中修改ZoneId和ImageId。

根据WordPressCluster-phpMyAdmin.ros，系统将创建和配置VPC、负载均衡、VSwitch、NAT网关、ECS实例、弹性公网IP、弹性伸缩和云数据库RDS版实例等。

在创建资源栈时，以下参数可满足任何地域的用户需要。

![ECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0869919951/p148461.png)

![RDS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0869919951/p148462.png)

根据模板，系统将在JumpBox上安装httpd、mysql-client、PHP、OSSFS、phpMyAdmin和WordPress，并通过资源ALIYUN::ECS::Instance的UserData段配置这些应用。

以下是UserData段部分代码：

```
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

通过UserData段，将WordPress部署在OSS Bucket上。OSS Bucket可挂载到弹性伸缩创建的Web服务器上，确保所有Web服务器都具有来自根目录的最新内容。

通过弹性伸缩配置的UserData段，实现httpd、PHP和ossutil的安装和配置、挂载DocumentRoo以及启动所有服务。

以下是弹性伸缩配置的UserData段部分代码：

```
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

## 更多信息

-   [创建资源栈](/cn.zh-CN/资源栈/创建资源栈.md)
-   [通过示例模板创建资源栈](/cn.zh-CN/快速入门/通过示例模板创建资源栈.md)
-   [使用可视化编辑器编写模板](/cn.zh-CN/常用工具/插件工具/使用可视化编辑器编写模板.md)
-   [使用RAM控制资源访问](/cn.zh-CN/快速入门/使用RAM控制资源访问.md)


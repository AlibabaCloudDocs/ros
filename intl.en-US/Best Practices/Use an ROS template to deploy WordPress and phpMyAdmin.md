# Use an ROS template to deploy WordPress and phpMyAdmin {#concept_67256_zh .concept}

This topic describes how to use an ROS resource stack template to deploy WordPress and phpMyAdmin.

## Background information {#section_k2g_xvc_lfb .section}

If you do not have the technical abilities to build and manage a website in-house but have a content management team, you can use an ROS resource stack template to manage your website. If you have higher requirements for customization, high availability, and high scalability of your website, you must resort to other solutions.

The ROS resource stack template \([WordPressCluster-phpMyAdmin.ros](http://ros-sample-templates.oss-eu-central-1.aliyuncs.com/WordPressCluster-phpMyAdmin.ros)\) discussed in this topic helps address your high availability and scalability requirements. You can use this template to create a resource stack with resources such as VPC, SLB, Auto Scaling, ECS, and ApsaraDB for RDS instances. Additionally, you can deploy WordPress and phpMyAdmin and configure Auto Scaling to add and configure new instances as needed.

## Prerequisites {#section_mvj_o3p_x7a .section}

-   An OSS bucket is available.
-   You can log on to the ROS console as a RAM user and have permissions on the OSS bucket to read and write data.
-   You have a working knowledge of ROS and can create templates and resource stacks in the ROS console.

## Architecture overview {#section_yd1_q5c_lfb .section}

The following figure shows how to use the [WordPressCluster-phpMyAdmin.ros](http://ros-sample-templates.oss-eu-central-1.aliyuncs.com/WordPressCluster-phpMyAdmin.ros) template to create a resource stack.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23203/156869061648093_en-US.png)

Three types of users can access the infrastructure shown in the preceding figure:

-   **End users**

    Web content can be stored and hosted on WordPress.

    WordPress is deployed on Apache Web servers. The root directory for storing files from the Web servers is `/wwwroot`. Next, the OSS bucket where the root directory is located is shared by the Web servers through OSSFS, a FUSE-based file system provided by Alibaba Cloud.

    RAM users can be granted permissions to access the OSS bucket and mount it onto their ECS instances.

    An ApsaraDB RDS for MySQL database is used to store WordPress content. End users can access the database from Web servers by using an intranet connection string.

-   **System administrators**

    System administrators can log on to JumpBox \(bastion host\) through SSH and access a VPC.

    JumpBox has an Elastic IP Address \(EIP\) and is accessible through the Internet.

    After system administrators access a VPC by using JumpBox, they can manage instances within the VPC.

    phpMyAdmin is installed on JumpBox and is therefore also accessible through the Internet.

    System administrators can use phpMyAdmin to manage their ApsaraDB for RDS databases.

-   **Content owners**

    Content owners can log on to the WordPress console through the Internet.

    They can manage all service access permissions through security groups based on system configurations.


## Template overview {#section_b21_q5c_lfb .section}

You can click [WordPressCluster-phpMyAdmin.ros](http://ros-sample-templates.oss-eu-central-1.aliyuncs.com/WordPressCluster-phpMyAdmin.ros) to download the ROS resource stack template.

**Note:** In this template, ZoneId is set to eu-central-1a and ImageId is set to m-gw8efmfk0y184zs0m0aj. The zones and images available in your ROS console may differ. You can reconfigure the ZoneId and ImageId parameters in the template as needed. To check the available zones and images, you can take these steps: Log on to the [ROS console](http://ros.console.aliyun.com). In the left-side navigation pane, click **ECS Instance Information**. In the main workspace, click the **ECS Zone** or **ECS Image** tab.

The WordPressCluster-phpMyAdmin.ros template enables the system to create and configure such resources as VPC, SLB, VSwitch, NAT Gateway, ECS, EIP, Auto Scaling, and ApsaraDB for RDS instances.

When creating a resource stack, set the following parameters as needed.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23203/156869061648094_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23203/156869061648096_en-US.png)

The system installs the following applications on JumpBox based on the template: httpd, mysql-client, PHP, OSSFS, phpMyAdmin, and WordPress. Additionally, the system uses the UserData segment in the ALIYUN::ECS::Instance resource to configure these applications.

The following is a snippet of the UserData segment:

``` {#codeblock_ngs_ul7_xuf .language-json}
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

The system deploys WordPress in an OSS bucket by using the UserData segment. Then the system mounts the OSS bucket to the Web servers that are created by Auto Scaling. This ensures that all the Web servers can obtain the latest content from the root directory.

The system uses the UserData segment of the Auto Scaling configuration to install and configure httpd, PHP, and ossutil, mount DocumentRoo, and start all services.

The following is a snippet of the UserData segment of the Auto Scaling configuration:

``` {#codeblock_yp3_ns5_o3c .language-json}
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


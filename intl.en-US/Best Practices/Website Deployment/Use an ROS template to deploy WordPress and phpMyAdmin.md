# Use an ROS template to deploy WordPress and phpMyAdmin

This topic describes how to use an Resource Orchestration Service \(ROS\) template to deploy WordPress and phpMyAdmin.

## Background information

If you do not have the technical abilities to build and manage a website in-house but do have a content management team, you can use an ROS template to manage only a simple website. If your website has higher requirements for customization, availability, and scalability, you must use a different solution to manage your website.

The WordPressCluster-phpMyAdmin.ros template that is described in this topic can address high availability and scalability requirements. You can use this template to create a stack that contains resources such as VPCs, SLB instances, Auto Scaling groups, ECS instances, and ApsaraDB for RDS instances. You can also configure Auto Scaling and deploy WordPress and phpMyAdmin to create and configure instances.

## Architecture overview

The following figure shows how to use the WordPressCluster-phpMyAdmin.ros template to create a stack.

![framework](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4404498951/p48093.png)

The following types of users can access the infrastructure that is shown in the preceding figure:

-   End users

    End users can access websites that are hosted on WordPress through URLs.

    WordPress is deployed on Apache web servers. The root directory for storing files from the web servers is `/wwwroot`. The OSS bucket where the root directory is located is shared by the web servers through OSSFS, which is a FUSE-based file system that is provided by Alibaba Cloud.

    RAM users can be granted permissions to access the OSS bucket and attach it to ECS instances.

    An ApsaraDB RDS for MySQL database is used to store WordPress content. End users can access the database from web servers through an internal connection string.

-   System administrators

    System administrators can log on to JumpBox \(bastion host\) through SSH and access a VPC.

    JumpBox has an elastic IP address \(EIP\) and is accessible from the Internet.

    System administrators can access a VPC through JumpBox and then manage instances within the VPC.

    phpMyAdmin is installed on JumpBox and is therefore also accessible through the Internet.

    System administrators can use phpMyAdmin to manage their ApsaraDB for RDS databases.

-   Content owners

    Content owners can log on to the WordPress console through the Internet.

    They can manage all service access permissions through security groups based on system configurations.


## Template overview

To download the template, click [WordPressCluster-phpMyAdmin.ros](https://ros-userdata-resources.oss-cn-beijing.aliyuncs.com/WordPress/WordPressCluster-phpMyAdmin.ros).

**Note:** You can reconfigure the ZoneId and ImageId parameters in the template.

The WordPressCluster-phpMyAdmin.ros template enables the system to create and configure resources such as VPCs, SLB instances, VSwitches, NAT gateways, ECS instances, EIPs, Auto Scaling groups, and ApsaraDB for RDS instances.

When you create a stack, configure the following parameters.

![ECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4404498951/p111185.png)

![RDS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4404498951/p111186.png)

The system installs the following applications on JumpBox based on the template: httpd, mysql-client, PHP, OSSFS, phpMyAdmin, and WordPress. The system uses the UserData segment in the ALIYUN::ECS::Instance resource to configure these applications.

The UserData segment contains the following snippet:

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

The system uses the UserData segment to deploy WordPress in an OSS bucket. Then, the system attaches the OSS bucket to the web servers that are created by Auto Scaling. This ensures that the latest content from the root directory can be accessed by using all web servers.

The system uses the UserData segment of the Auto Scaling configuration to install and configure httpd, PHP, and ossutil, attach DocumentRoo, and start all services.

The UserData segment of the Auto Scaling configuration contains the following snippet:

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

## Related topics

-   [Create stacks](/intl.en-US/Stack Management/Create a stack.md)
-   [Use sample templates to create stacks](/intl.en-US/Quick Start/Use sample templates to create stacks.md)
-   [Use RAM to control resource access](/intl.en-US/Quick Start/Use RAM to control resource access.md)


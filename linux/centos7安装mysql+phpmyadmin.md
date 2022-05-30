# Centos7安装配置

# Apache（httpd）+php+mysql+phpMyAdmin

安装前提：centos7可以连接外网

# MySQL

## 1.mysql安装检查

rpm -qa \| grep -i mysql

![](media/image1.png){width="5.458333333333333in" height="1.5625in"}

## 2.关闭mysql服务

查看MySQL服务运行状态：

service mysql status

停止mysql服务

Service mysql stop

## **3.查看mysql对应的文件夹**

find / -name mysql

## **4.卸载并删除mysql安装的组建服务**

rpm -ev mysql-community-common-5.6.44-2.el7.x86_64

rpm -ev mysql-community-release-el7-5.noarch

rpm -ev mysql-community-client-5.6.44-2.el7.x86_64

rpm -ev mysql-community-server-5.6.44-2.el7.x86_64

rpm -ev mysql-community-libs-5.6.44-2.el7.x86_64

## **删除系统中所有mysql文件夹**

通过 find / -name mysql 查找出了所有文件夹，使用

rm -rf + 文件路径直接删除即可

## **5.验证mysql是否删除完成**

rpm -qa \| grep -i mysql

没有任何提示则卸载完成

![](media/image2.png){width="4.0625in" height="0.5104166666666666in"}

## **6.安装mysql**

wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm

rpm -ivh mysql-community-release-el7-5.noarch.rpm

执行安装

yum -y install mysql mysql-server mysql-devel

安装完成再次执行得到以下信息

![](media/image3.png){width="5.760416666666667in"
height="1.5458333333333334in"}

打开mysql服务

service mysqld start

进入mysql客户端

mysql -u root -p

不用输入密码直接回车进入

选择数据库

use mysql

修改root用户密码

update user set password=password(\'root\') where
user=\'root\';(5.6版本)

update user set authentication_string=password(\'root\') where
user=\'root\';(5.7版本)

出现如下提示修改成功

![](media/image4.png){width="5.7625in" height="0.4840277777777778in"}

执行flush privileges;

![](media/image5.png){width="4.0in" height="0.84375in"}

退出 quit

重新登陆

mysql -u root -p 输入修改的密码成功登陆

# Apache(httpd)

1. ## 安装apache服务
   
   yum install httpd

2. ## 执行启动命令
   
   service httpd start
   
   ![](media/image6.png){width="4.854166666666667in"
   height="0.46875in"}
   
   浏览器输入ip地址出现如下界面
   
   ![](media/image7.png){width="5.756944444444445in"
   height="2.9340277777777777in"}

# PHP

1. ## 安装php
   
   yum install php php-mysql php-gd libjpeg\* php-ldap php-odbc
   php-pear php-xml php-xmlrpc php-mbstring php-bcmath php-mhash
   
   安装完成重启服务
   
   service httpd restart

2. ## 测试安装结果
   
   vim /var/www/html/index.php
   
   按 i 或者 insert进入输入模式，输入一下内容
   
   \<?php
   
   phpinfo();
   
   ?\>
   
   esc 退出编辑模式， :wq 保存退出
   
   重启服务
   
   service httpd restart
   
   浏览器输入IP地址，出现如下界面
   
   ![](media/image8.png){width="5.767361111111111in"
   height="2.9194444444444443in"}

# phpMyAdmin

1. ## 先安装epel，不然安装pgpmyadmin时会出现找不到包。
   
   yum install epel-release
   
   rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

2. ## yum安装phpmyadmin
   
   yum install phpmyadmin php-mcrypt

3. ## 修改配置文件
   
   phpMyAdmin 的默认安装目录是 /usr/share/phpMyAdmin，同时会在 Apache
   的配置文件目录中自动创建虚拟主机配置文件
   /etc/httpd/conf.d/phpMyAdmin.conf（区分大小写）。默认情况下，CentOS
   7上的phpMyAdmin只允许从回环地址(127.0.0.1)访问。为了能远程连接，你需要改动它的配置。
   
   vim /etc/httpd/conf.d/phpMyAdmin.conf
   
   将出现Require ip 的地方注释掉,然后添加Require all granted
   
   一共注释四处地方，添加两行
   
   ![](media/image9.png){width="3.8958333333333335in"
   height="3.7604166666666665in"}
   
   ![](media/image10.png){width="4.020833333333333in"
   height="3.46875in"}
   
   :wq保存退出，重启服务
   
   service httpd restart
   
   浏览器输入ip/phpmyadmin 进入登陆页面,输入数据库用户名密码登陆.
   
   ![](media/image11.png){width="5.7625in"
   height="2.4472222222222224in"}
   
   ![](media/image12.png){width="5.7625in"
   height="2.759027777777778in"}

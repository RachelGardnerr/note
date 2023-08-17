# linux

## 一、常用操作

### 1.终端基本操作

**1.1切换界面******

切换命令行界面

```
Ctrl+Alt+F2 #可以使用F2-F6
```

切换图形化界面

```
Crtl+Alt+F1
```

**1.2 调整终端字体大小**

```
Crtl+Shift++ #增大
Ctrl+- #减小
```

### 2.vim编辑器

**2.1 一般模式**

| 语法         | 功能描述                 |
|:----------:|:-------------------- |
| y          | 数字 y 复制一段（从第几行到第几行）  |
| yy         | 复制光标当前一行             |
| p          | 箭头移动到目的行粘贴           |
| u          | 撤销上一步                |
| dd         | 删除光标当前行              |
| X          | 剪切一个字母，相当于 Backspace |
| yw         | 复制一个词                |
| dw         | 删除一个词                |
| shift+6(^) | 移动到行头                |
| shift+4($) | 移动到行尾                |
| 1+shift+g  | 移动到页头，数字             |
| shift+g    | 移动到页尾                |
| 数字+shift+g | 移动到目标行               |

**2.2 编辑模式**

| 按键  | 功能        |
|:---:|:--------- |
| i   | 当前光标前     |
| a   | 当前光标后     |
| o   | 当前光标行的下一行 |
| I   | 光标所在行最前   |
| A   | 光标所在行最后   |
| O   | 当前光标行的上一行 |

**退出编辑模式**

按『Esc』键 退出编辑模式，之后所在的模式为一般模式

**2.3 指令模式**

在一般模式当中，输入『 : / ?』3个中的任何一个按钮，就可以将光标移动到最底下那
一行。

| 命令            | 功能                 |
|:-------------:|:------------------ |
| :w            | 保存                 |
| :q            | 退出                 |
| :!            | 强制执行               |
| /要查找的词        | n 查找下一个，N 往上查找     |
| :noh          | 取消高亮显示             |
| :set nu       | 显示行号               |
| :set nonu     | 关闭行号               |
| :%s/old/new/g | 替换内容 /g 替换匹配到的所有内容 |

### 3.清空日志文件

```linux
cat /dev/null > file_name
```

## 二、网络配置

## 三、系统管理

### 3.1 service服务管理

 1.centos6

```
service 服务名 start|stop|restart|status
```

2.centos7

```
systemctl start|stop|restart|status 服务名
```

设置服务后台自启配置

```
systemctl list-units-files # 查看服务开机自启状态
systemctl disable 服务名 # 关闭指定服务的自动启动
systemctl enable  服务名 # 开启指定服务的自动启动
```

### 3.2 系统运行级别

linux运行级别（Centos6）

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/2022/08/10-11-20-57-linux1.png)

Centos7的运行级别简化为

multi-user.target 等价于原运行级别 3（多用户有网，无图形界面）
graphical.target 等价于原运行级别 5（多用户有网，有图形界面）

### 3.3 关闭防火墙

```
systemctl stop firewalld # 临时关闭防火墙
systemctl status firewalld # 查看防火墙状态
```

开机启动时关闭防火墙

```
systemctl enable firewalld.service # 查看防火墙启动状态
systemctl disable firewalld.service# 设置开机时关闭防火墙
```

### 3.4 关机重启命令

（1）sync：将数据由内存同步到硬盘中
（2）halt：停机，关闭系统，但不断电
（3）poweroff：关机，断电）
（3）reboot：就是重启，等同于 shutdown -r now）
（4）shutdown [选项] 时间

```
shutdown -H # 相当于halt 停机
shutdown -r # -r=reboot 
```

```
shutdown now # 立刻关机
shutdown 60 # 六十分钟后关机
shutdown 13:00 # 13：00关机
```

  

## 四、常用基本命令

### 4.1 文件目录类

#### pwd

pwd:显示当前工作目录的绝对路径

-#### ls

ls 列出目录的内容

```
ls -a # 全部的文件，连同隐藏档( 开头为 . 的文件) 一起列出来(常用)
ls -l # 长数据串列出，包含文件的属性与权限等等数据；(常用)等价于“ll”
```

每行列出的信息依次是： 

文件类型与权限 链接数 文件属主 文件属组 

文件大小用byte来表示 建立或最近修改的时间 名字

#### cd

cd:Change Directory 切换路径

| 参数        | 功能                 |
|:---------:|:------------------ |
| cd 绝对路径   | 切换路径               |
| cd 相对路径   | 切换路径               |
| cd ~或者 cd | 回到自己的家目录           |
| cd -      | 回到上一次所在目录          |
| cd ..     | 回到当前目录的上一级目录       |
| cd -P     | 跳转到实际物理路径，而非快捷方式路径 |

#### mkdir

mkdir:Make directory 建立目录

```
mkdir 目录名称 #创建目录
mkdir -p #创建多层目录
```

#### rmdir

rmdir:Remove directory 移除目录

```
rmdir 要删除的空目录
```

#### touch 创建空文件

```
touch 文件名称
touch /xx/xx/文件名称
```

#### cp 复制文件或目录

cp [选项] source dest  (功能描述：复制source文件到dest）

```
cp -r #递归复制整个文件夹
```

#### rm 删除文件或目录

rm [选项] deleteFile（功能描述：递归删除目录中所有内容）

```
rm -r #递归删除目录中所有内容
rm -f #强制执行删除操作，而不提示用于进行确认
rm -v #显示指令的详细执行过程
rm -rf
rm -rv
rm -rfv
```

#### mv 移动文件与目录或重命名

```
mv oldNameFile newNameFile #功能描述：重命名
mv /temp/movefile /targetFolder #功能描述：移动文件
```

#### cat 查看文件内容

查看文件内容，从第一行开始显示。

cat [选项] 要查看的文件

```
cat 文件名
cat -n 文件名 #显示所有行的行号，包括空行
```

#### more 文件内容分屏查看器

more 指令是一个基于 VI 编辑器的文本过滤器，它以全屏幕的方式按页显示文本文件
的内容。

```
more 要查看的文件
```

| 操作          | 功能说明                    |
|:-----------:|:----------------------- |
| 空白键 (space) | 代表向下翻一页；                |
| Enter       | 代表向下翻『一行』；              |
| q           | 代表立刻离开 more ，不再显示该文件内容。 |
| Ctrl+F      | 向下滚动一屏                  |
| Ctrl+B      | 返回上一屏                   |
| =           | 输出当前行的行号                |
| :f          | 输出文件名和当前行的行号            |

#### less 分屏显示文件内容

ess 指令用来分屏查看文件内容，它的功能与 more 指令类似，但是比 more 指令更加
强大，支持各种显示终端。less 指令在显示文件内容时，并不是一次将整个文件加载之后
才显示，而是根据显示需要加载内容，对于显示大型文件具有较高的效率。

```
less 要查看的文件
```

| 操作         | 功能说明                      |
|:----------:|:------------------------- |
| 空白键        | 向下翻动一页                    |
| [pagedown] | 向下翻动一页                    |
| [pageup]   | 向上翻动一页                    |
| /字串        | 向下搜寻『字串』的功能；n：向下查找；N：向上查找 |
| ?字串        | 向上搜寻『字串』的功能；n：向上查找；N：向下查找 |
| q          | 离开 less 这个程序              |

ps: 用SecureCRT时[pagedown]和[pageup]可能会出现无法识别的问题。

#### echo 输出内容到控制台

echo [选项] [输出内容]

-e： 支持反斜线控制的字符转换:

| 控制字符 | 作用            |
|:----:|:------------- |
| \\\  | 输出\本身         |
| \n   | 换行符           |
| \t   | 制表符，也就是 Tab 键 |

```
[root@localhost ~]# clear
[root@localhost ~]# echo -e 'hello\\word'
hello\word
[root@localhost ~]# echo -e 'hello\tword'
hello    word
[root@localhost ~]# echo -e 'hello\nword'
hello
word
```

#### head 显示文件头部内容

head 用于显示文件的开头部分内容，默认情况下 head 指令显示文件的前 10 行内容。

```
head 文件       # 查看文件头10行内容
head -n 5 文件  # 查看文件头5行内容，5可以是任意行数
```

#### tail 输出文件尾部内容

tail 用于输出文件中尾部的内容，默认情况下 tail 指令显示文件的后 10 行内容。

| 选项     | 功能                 |
|:------:|:------------------ |
| -n<行数> | 输出文件尾部 n 行内容       |
| -f     | 显示文件最新追加的内容，监视文件变化 |

#### >输出重定向和>>追加

```
ls -l > 文件       # 列表的内容写入文件 a.txt 中（覆盖写）
ls -al >> 文件     # 列表的内容追加到文件 aa.txt 的末尾）
cat 文件 1 > 文件 2 # 将文件 1 的内容覆盖到文件 2）
echo “内容” >> 文件
```

#### ln 软链接

软链接也称为符号链接，类似于 windows 里的快捷方式，有自己的数据块，主要存放
了链接其他文件的路径。

```
ln -s [原文件或目录] [软链接名] # 给原文件创建一个软链接）
```

删除软链接： rm -rf 软链接名，而不是 rm -rf 软链接名/
如果使用 rm -rf 软链接名/ 删除，会把软链接对应的真实目录下内容删掉
查询：通过 ll 就可以查看，列表属性第 1 位是 l，尾部会有位置指向

```
[root@localhost test]# ln -s test abc
[root@localhost test]# ll
total 0
lrwxrwxrwx 1 root root 4 Aug 10 02:41 abc -> test
drwxr-xr-x 2 root root 6 Aug 10 02:41 test
```

#### history 查看已经执行过历史命令

```
history # 查看已经执行过历史命令）
```

### 4.2 时间日期类

date [OPTION]... [+FORMAT]

| 选项        | 功能                       |
|:---------:|:------------------------ |
| -d<时间字符串> | 显示指定的“时间字符串”表示的时间，而非当前时间 |
| -s<日期时间>  | 设置系统日期时间                 |

| 参数        | 功能             |
|:---------:|:-------------- |
| <+日期时间格式> | 指定显示时使用的日期时间格式 |

#### 4.2.1 date 显示当前时间

```
date                         # 功能描述：显示当前时间
date +%Y                     # 显示当前年份
date +%m                     # 显示当前月份）
date +%d                     # 显示当前是哪一天）
date "+%Y-%m-%d %H:%M:%S"    # 显示年月日时分秒）
```

#### 4.2.2 date 显示非当前时间

```
date -d '1 days ago'          # 显示前一天时间）
（2）date -d '-1 days ago'     # 显示明天时间）
```

#### 4.2.3 date 设置系统时间

```
date -s 字符串时间 # 重启后失效
```

#### 4.2.4 cal 查看日历

```
cal [选项] # 不加选项，显示本月日历）
```

| 选项    | 功能       |
| ----- | -------- |
| 具体某一年 | 显示这一年的日历 |

### 4.3 用户管理类

#### 4.3.1 useradd 添加新用户

```
useradd 用户名         # 添加新用户
useradd -g 组名 用户名  # 添加新用户到某个组
```

#### 4.3.2 passwd 设置用户密码

```
passwd 用户名

root@localhost home]# passwd redis
Changing password for user redis.
New password: 
Retype new password: 
passwd: all authentication tokens updated successfully.
```

#### 4.3.3 id 查看用户是否存在

```
id 用户名
```

#### 4.3.4 cat /etc/passwd 查看创建了哪些用户

#### 4.3.5 su 切换用户

```
su 用户名称   # 切换用户，只能获得用户的执行权限，不能获得环境变量）
su - 用户名称 # 切换到用户并获得该用户的环境变量及执行权限）
```

```
[root@localhost ~]# su redis
[redis@localhost root]$ echo $PATH
/usr/local/java/jdk1.8.0_333/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
[redis@localhost root]$ su - redis
Password: 
Last login: Thu Aug 11 03:59:09 EDT 2022 on pts/1
[redis@localhost ~]$ echo $PATH
/usr/local/java/jdk1.8.0_333/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/redis/.local/bin:/home/redis/bin
```

#### 4.3.6 userdel 删除用户

```
userdel 用户名    #删除用户但保存用户主目录
userdel -r 用户名 #用户和用户主目录，都删除
```

| 选项  | 功能                    |
|:---:|:---------------------:|
| -r  | 删除用户的同时，删除与用户相关的所有文件。 |

#### 4.3.7 who 查看登录用户信息

```
whoami    #显示自身用户名称
who am i  #显示登录用户的用户名以及登陆时间
```

#### 4.3.8 sudo 设置普通用户具有 root 权限

**1)添加用户**

**2)修改配置文件**

```
vim /etc/sudoers
```

修改 /etc/sudoers 文件，找到下面一行(91 行)，在 root 下面添加一行，如下所示：

```
## Allow root to run any commands anywhere
root    ALL=(ALL)    ALL
le      ALL=(ALL)    ALL
```

或者配置成采用 sudo 命令时，不需要输入密码

```
## Allow root to run any commands anywhere
root    ALL=(ALL)    ALL
le      ALL=(ALL)    NOPASSWD:ALL
```

修改完毕，现在可以用 le帐号登录，然后用命令 sudo ，即可获得 root 权限进行

#### 4.3.9 usermod 修改用户

```
usermod -g 用户组 用户名
```

| 选项  | 功能                             |
| --- | ------------------------------ |
| -g  | 修改用户的初始登录组，给定的组必须存在。默认组 id 是 1 |

### 4.4 用户组管理命令

        每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同
Linux 系统对用户组的规定有所不同，
如Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。

        用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对
/etc/group文件的更新。

#### 4.4.1  cat /etc/group 查看创建了哪些组

#### 4.4.2 groupadd/del 新增、删除组

```
groupadd 组名 #新增组
groupdel 组名 #删除组
```

#### 4.4.3 groupmod 修改组

```
groupmod -n 新组名 旧组名 #修改组
```

| 选项      | 功能描述      |
|:-------:|:---------:|
| -n<新组名> | 指定工作组的新组名 |

### 4.5 文件权限类

#### 4.5.1 文件属性

Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。
为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做
了不同的规定。在Linux中我们可以使用ll或者ls -l命令来显示一个文件的属性以及文件所属
的用户和组。

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208310948082.png)

如果没有权限，就会出现减号[ - ]。从左至右用0-9这些数字来表示:

- 0 首位表示类型
      在Linux中第一个字符代表这个文件是目录、文件或链接文件等等

            - 代表文件
            d 代表目录
            l 链接文档(link file)；

- 第1-3位确定属主（该文件的所有者）拥有该文件的权限。---User

- 第4-6位确定属组（所有者的同组用户）拥有该文件的权限，---Group

- 第7-9位确定其他用户拥有该文件的权限 ---Other

**rwx 作用文件和目录的不同解释**

**（1）作用到文件：**
[ r ]代表可读(read): 可以读取，查看
[ w ]代表可写(write): 可以修改，但是不代表可以删除该文件，删除一个文件的前
提条件是对该文件所在的目录有写权限，才能删除该文件.
[ x ]代表可执行(execute):可以被系统执行
**（2）作用到目录：**
[ r ]代表可读(read): 可以读取，ls查看目录内容
[ w ]代表可写(write): 可以修改，目录内创建+删除+重命名目录
[ x ]代表可执行(execute):可以进入该目录

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208191011543.png)

（1）如果查看到是文件：链接数指的是硬链接个数。
（2）如果查看的是文件夹：链接数指的是子文件夹个数。

#### 4.5.2 chmod改变权限

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208261009457.png)

方式一

```linux
chmod [{ugoa}{+-=}{rwx}] 文件或目录
```

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208261450715.png)

方式二

```linux
chmod [mode=421] [文件或目录]
```

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208261455231.png)

#### 4.5.3 chown 改变所有者

```linux
chown [选项] [最终用户] [文件或目录] # 改变文件或者目录的所有者
```

| 选项  | 功能   |
| --- | ---- |
| -R  | 递归操作 |

```
chown le test #修改文件所有者
chown -R le:le test #修改所有者和所有组
```

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208261517470.png)

#### 4.5.4 chgrp 改变所属组

```
chgrp [最终用户组] [文件或目录] # 改变文件或者目录的所属组）
```

### 4.6 搜索查找类

#### 4.6.1 find查找文件或者目录

find 指令将从指定目录向下递归地遍历其各个子目录，将满足条件的文件显示在终端。

```
find [搜索范围] [选项]
```

| 选项          | 功能                                                                                                  |
| ----------- | --------------------------------------------------------------------------------------------------- |
| -name<查询方式> | 按照指定的文件名查找模式查找文件                                                                                    |
| -user<用户名>  | 查找属于指定用户名所有文件                                                                                       |
| -size<文件大小> | 按照指定的文件大小查找文件,单位为:<br>b —— 块（512 字节）<br>c —— 字节<br>w —— 字（2 字节）<br>k —— 千字节<br>M —— 兆字节<br>G —— 吉字节 |

#### 4.6.2 locate 定位文件

locate 指令利用事先建立的系统中所有文件名称及路径的 locate 数据库实现快速定位给
定的文件。Locate 指令无需遍历整个文件系统，查询速度较快。为了保证查询结果的准确
度，管理员必须定期更新 locate 时刻。

```linux
updatedb # 第一次和要定位新文件时执行
locate 搜索文件
```

#### 4.6.3 grep 过滤查找及“|”管道符

管道符，“|”，表示将前一个命令的处理结果输出传递给后面的命令处理

| 选项  | 功能        |
| --- | --------- |
| -n  | 显示匹配行及行号。 |

```
grep 选项 查找内容 源文件
```

```
[root@localhost ~]# ls |grep -n test
4:test
[root@localhost ~]# ls
abc.txt  anaconda-ks.cfg  initial-setup-ks.cfg  test  tomcat8.5.81
```

### 4.7 压缩和解压类

#### 4.7.1 gzip/gunzip 压缩

```
gzip 文件 # 压缩文件，只能将文件压缩为*.gz 文件）
gunzip 文件.gz # 解压缩文件命令）
```

（1）只能压缩文件不能压缩目录
（2）不保留原来的文件
（3）同时多个文件会产生多个压缩包

#### 4.7.2 zip/unzip 压缩

```
zip [选项] XXX.zip 将要压缩的内容 # 压缩文件和目录的命令）
unzip [选项] XXX.zip # 解压缩文件
```

| zip选项 | 功能   |
| ----- | ---- |
| -r    | 压缩目录 |

| unzip 选项 | 功能           |
| -------- | ------------ |
| -d<目录>   | 指定解压后文件的存放目录 |

zip 压缩命令在windows/linux都通用，可以压缩目录且保留源文件。

#### 4.7.3  tar 打包

tar [选项] XXX.tar.gz 将要打包进去的内容 # 打包目录，压缩后的
文件格式.tar.gz）

| 选项     | 功能          |
| ------ | ----------- |
| -c     | 产生.tar 打包文件 |
| -v     | 显示详细信息      |
| -f     | 指定压缩后的文件名   |
| -z     | 打包同时压缩      |
| -x     | 解包.tar 文件   |
| -C(大写) | 解压到指定目录     |

**压缩多个文件**

```
[root@localhost test]# ls
a.txt  b.txt  c.txt
[root@localhost test]# tar -zcvf abc.tar.gz a.txt b.txt c.txt 
a.txt
b.txt
c.txt
[root@localhost test]# ls
abc.tar.gz  a.txt  b.txt  c.txt
[root@localhost test]# 
```

**压缩目录**

```
[root@localhost ~]# ls
abc.txt  anaconda-ks.cfg  initial-setup-ks.cfg  test  tomcat8.5.81
[root@localhost ~]# tar -zcvf test.tar.gz test
test/
test/abc.tar.gz
[root@localhost ~]# ls
abc.txt  anaconda-ks.cfg  initial-setup-ks.cfg  test  test.tar.gz  tomcat8.5.81
[root@localhost ~]# 
```

**解压到当前目录**

```
[root@localhost test]# ls
abc.tar.gz
[root@localhost test]# tar -zxvf abc.tar.gz 
a.txt
b.txt
c.txt
[root@localhost test]# ls
abc.tar.gz  a.txt  b.txt  c.txt
[root@localhost test]# 
```

**解压到指定目录**

```
[root@localhost test]# ls
abc.tar.gz  a.txt  b.txt  c.txt
[root@localhost test]# tar -zxvf abc.tar.gz -C /root
a.txt
b.txt
c.txt
[root@localhost test]# cd
[root@localhost ~]# ls
anaconda-ks.cfg  a.txt  b.txt  c.txt  initial-setup-ks.cfg  test  test.tar.gz  tomcat8.5.81
[root@localhost ~]# 
```

### 4.9 磁盘查看和分区类

#### 4.9.1 du 查看文件和目录占用的磁盘空间

du: disk usage 磁盘占用情况

```
du 目录/文件 # 显示目录下每个子目录的磁盘使用情况
```

| 选项            | 功能                                       |
| ------------- | ---------------------------------------- |
| -h            | 以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示； |
| -a            | 不仅查看子目录大小，还要包括文件                         |
| -c            | 显示所有的文件和子目录大小后，显示总和                      |
| -s            | 只显示总和                                    |
| --max-depth=n | 指定统计子目录的深度为第 n 层                         |

#### 4.9.2 df 查看磁盘空间使用情况

df: disk free 空余磁盘

```
df 选项 # 列出文件系统的整体磁盘使用量，检查文件系统的磁盘空间占
用情况
```

| 选项  | 功能                                       |
| --- | ---------------------------------------- |
| -h  | 以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示； |

#### 4.9.3 lsblk 查看设备挂载情况

```
lsblk # 查看设备挂载情况
```

| 选项  | 功能                   |
| --- | -------------------- |
| -f  | 查看详细的设备挂载情况，显示文件系统信息 |

#### 4.9.4 fdisk 分区

```
fdisk -l # 查看磁盘分区详情）
fdisk 硬盘设备名 # 对新增硬盘进行分区操作）
```

| 选项  | 功能          |
| --- | ----------- |
| -l  | 显示所有硬盘的分区列表 |

该命令必须在 root 用户下才能使用

**(1）Linux 分区**

Device：分区序列
Boot：引导
Start：从X磁柱开始
End：到Y磁柱结束
Blocks：容量
Id：分区类型ID
System：分区类型
**（2）分区操作按键说明**
m：显示命令列表
p：显示当前磁盘分区
n：新增分区
w：写入分区信息并退出
q：不保存分区信息直接退出

### 4.10 进程管理类

#### 4.10.1 ps 查看当前系统进程状态

ps:process status 进程状态

```
ps aux | grep xxx    # 查看系统中所有进程
ps -ef | grep xxx    # 可以查看子父进程之间的关系
```

| 选项  | 功能                    |
|:---:|:--------------------- |
| -a  | 列出带有终端的所有用户的进程        |
| -x  | 列出当前用户的所有进程，包括没有终端的进程 |
| -u  | 面向用户友好的显示风格           |
| -e  | 列出所有进程                |
| -u  | 列出某个用户关联的所有进程         |
| -f  | 显示完整格式的进程列表           |

**（1）ps aux 显示信息说明**
**USER**：该进程是由哪个用户产生的**PID**：进程的 ***ID*** 号
**%CPU**：该进程占用 ***CPU*** 资源的百分比，占用越高，进程越耗费资源；
**%MEM**：该进程占用物理内存的百分比，占用越高，进程越耗费资源；
**VSZ**：该进程占用虚拟内存的大小，单位 KB；
**RSS**：该进程占用实际物理内存的大小，单位 KB；
**TTY**：该进程是在哪个终端中运行的。对于 ***CentOS*** 来说，***tty1*** 是图形化终端，
***tty2-tty6*** 是本地的字符界面终端。***pts/0-255*** 代表虚拟终端。
**STAT**：进程状态。常见的状态有：***R***：运行状态、***S***：睡眠状态、***T***：暂停状态、
***Z***：僵尸状态、***s***：包含子进程、**l**：多线程、**+**：前台显示
**START**：该进程的启动时间
**TIME**：该进程占用 ***CPU*** 的运算时间，注意不是系统时间
**COMMAND**：产生此进程的命令名
**（2）ps -ef 显示信息说明**
UID：用户 ID
PID：进程 ID
PPID：父进程 ID
C：CPU 用于计算执行优先级的因子。数值越大，表明进程是 CPU 密集型运算，
执行优先级会降低；数值越小，表明进程是 I/O 密集型运算，执行优先级会提高
STIME：进程启动的时间
TTY：完整的终端名称
TIME：CPU 时间
CMD：启动进程所用的命令和参数

如果想查看进程的 CPU 占用率和内存占用率，可以使用 aux;
如果想查看进程的父进程 ID 可以使用 ef;

#### 4.10.2  kill 终止进程

```
kill [选项] 进程号 # 通过进程号杀死进程
killall 进程名称 # 通过进程名称杀死进程，也支持通配符，这
在系统因负载过大而变得很慢时很有用
```

| 选项  | 功能         |
| --- | ---------- |
| -9  | 表示强迫进程立即停止 |

#### 4.10.3 pstree 查看进程树

```
pstree [选项]
```

| 选项  | 功能        |
| --- | --------- |
| -p  | 显示进程的 PID |
| -u  | 显示进程的所属用户 |

#### 4.10.4 top 实时监控系统进程状态

```
top [选项]
```

| 选项    | 功能                                             |
| ----- | ---------------------------------------------- |
| -d 秒数 | 指定 top 命令每隔几秒更新。默认是 3 秒在 top 命令的交互模式当中可以执行的命令： |
| -i    | 使 top 不显示任何闲置或者僵死进程。                           |
| -p    | 通过指定监控进程 ID 来仅仅监控某个进程的状态。                      |

| 操作  | 功能                 |
| --- | ------------------ |
| P   | 以 CPU 使用率排序，默认就是此项 |
| M   | 以内存的使用率排序          |
| N   | 以 PID 排序           |
| q   | 退出 top             |

##### 查询结果字段解释

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208310930219.png)

**第一行信息为任务队列信息**

| 内容                          | 说明                        |
| --------------------------- | ------------------------- |
| 21：30：12                    | 系统当前时间                    |
| up 15 min                   | 系统运行时间，本机已运行15分钟          |
| 2 users                     | 当前登陆了两个用户                 |
| load average 0.00 0.04 0.10 | 系统在之前 1 分钟，5 分钟，15 分钟的平均负 |
| <br/>载。一般认为小于 1 时，负载较小。如果大于 |                           |
| <br/>1，系统已经超出负荷。            |                           |

**第二行为进程信息**

| 内容              | 描述                     |
| --------------- | ---------------------- |
| Tasks:223 total | 系统中的进程总数               |
| 2 running       | 正在运行的进程数               |
| 221 sleeping    | 正在睡眠的进程                |
| 0 stoped        | 正在停止的进程                |
| 0 zombie        | 僵尸进程。如果不是 0，需要手工检查僵尸进程 |

**第三行为 CPU 信息**

| 内容             | 描述                                                     |
| -------------- | ------------------------------------------------------ |
| Cpu(s): 0.1%us | 用户模式占用的 CPU 百分比                                        |
| 0.1%sy         | 系统模式占用的 CPU 百分比                                        |
| 0.0%ni         | 改变过优先级的用户进程占用的 CPU 百分比                                 |
| 99.8 id        | 空闲 CPU 的 CPU 百分比                                       |
| 0.0 wa         | 等待输入/输出的进程的占用 CPU 百分比                                  |
| 0.0 hi         | 硬中断请求服务占用的 CPU 百分比                                     |
| 0.1 si         | 软中断请求服务占用的 CPU 百分比                                     |
| 0.0 st         | st（Steal time）虚拟时间百分比。就是当有虚拟机时，虚拟 CPU 等待实际 CPU 的时间百分比。 |

**第四行为物理内存信息**

| 内容                        | 描述            |
| ------------------------- | ------------- |
| KiB Mem :  3861292 total, | 物理内存的总量，单位 KB |
| 1199292 used              | 已经使用的物理内存数量   |
| 1037456 free              | 空闲的物理内存数量     |
| 1624544 buff/cache        | 作为缓冲的内存数量     |

**第五行为交换分区（swap）信息**

| 内容                       | 描述             |
| ------------------------ | -------------- |
| KiB Swap:  4063228 total | 交换分区（虚拟内存）的总大小 |
| 0 used.                  | 已经使用的交互分区的大小   |
| 4063228 free             | 空闲交换分区的大小      |
| 2409488 avail Mem        | 作为缓存的交互分区的大小   |

#### 4.10.5 netstat 显示网络状态和端口占用信息

```
netstat -anp | grep 进程号 # 查看该进程网络信息
netstat –nlp | grep 端口号 # 查看网络端口号占用情况）
```

| 选项  | 功能                               |
| --- | -------------------------------- |
| -a  | 显示所有正在监听（listen）和未监听的套接字（socket） |
| -n  | 拒绝显示别名，能显示数字的全部转化成数字             |
| -l  | 仅列出在监听的服务状态                      |
| -p  | 表示显示哪个进程在调用                      |

查看某端口号是否被占用

```
netstat -nltp | grep 22
```

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208311007830.png)

#### 4.10.6  crontab 系统定时任务

## 五、软件包管理

### 5.1 PRM

#### 5.1.1 RPM 概述

RPM（RedHat Package Manager），RedHat软件包管理工具，类似windows里面的setup.exe是Linux这系列操作系统里面的打包安装工具，它虽然是RedHat的标志，但理念是通用的。
RPM包的名称格式
Apache-1.3.23-11.i386.rpm

- “apache” 软件名称

- “1.3.23-11”软件的版本号，主版本和此版本

- “i386”是软件所运行的硬件平台，Intel 32位处理器的统称

- “rpm”文件扩展名，代表RPM包

#### 5.1.2 RPM 查询命令

```
rpm -qa # 查询所安装的所有 rpm 软件包）
```

由于软件包比较多，一般都会采取过滤。rpm -qa | grep rpm软件包

**查询firefox软件安装情况**

```
[root@localhost ~]# rpm -qa|grep firefox
firefox-68.10.0-1.el7.centos.x86_64
```

#### 5.1.3 RPM 卸载命令

```
rpm -e RPM软件包
rpm -e --nodeps 软件包
```

| 选项       | 功能                                          |
| -------- | ------------------------------------------- |
| -e       | 卸载软件包                                       |
| --nodeps | 卸载软件时，不检查依赖。这样的话，那些使用该软件包的软件在此之后可能就不能正常工作了。 |

#### 5.1.4 RPM 安装命令

```
rpm -ivh RPM 包全名
```

| 选项       | 功能               |
| -------- | ---------------- |
| -i       | install，安装       |
| -v       | --verbose，显示详细信息 |
| -h       | --hash，进度条       |
| --nodeps | 安装前不检查依赖         |

### 5.2 YUM 仓库配置

#### 5.2.1 YUM 概述

        YUM（全称为 Yellow dog Updater, Modified）是一个在 Fedora 和 RedHat 以及 CentOS中的 Shell 前端软件包管理器。基于 RPM 包管理，能够从指定的服务器自动下载 RPM 包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装

![](https://raw.githubusercontent.com/RachelGardnerr/image/main/img/202208311024487.png)

#### 5.2.2 YUM 的常用命令

```
yum [选项] [参数]
```

| 选项  | 功能            |
| --- | ------------- |
| -y  | 对所有提问都回答“yes” |

| 参数           | 功能                 |
| ------------ | ------------------ |
| install      | 安装 rpm 软件包         |
| update       | 更新 rpm 软件包         |
| check-update | 检查是否有可用的更新 rpm 软件包 |
| remove       | 删除指定的 rpm 软件包      |
| list         | 显示软件包信息            |
| clean        | 清理 yum 过期的缓存       |
| deplist      | 显示 yum 软件包的所有依赖关系  |

# windows

## oracle

```cmd
检查监听器状态
lsnrctl status

启动监听程序
lsnrctl start

启动oracle服务实例
net start oracleServiceOrcl

关闭oracle服务实例
net stop oracleServiceOrcl

关闭监听
lsnrctl stop
```

## 测试ip和端口

```cmd
telnet ip 端口
```

netstat -tnl

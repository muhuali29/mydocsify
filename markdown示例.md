# markdown示例
## linux安装
- [ ] vmware`注意` 中网卡选择’定义vmnet1，意思与windows中的vmnet1对应，等于一条网线连接两电脑，设ip为同一网段`即可通讯`。<font color=red>我是红色</font>
- [x] 在安装centos途中可设置**centos网卡的ip**<font face="微软雅黑">我是微软雅黑</font>
- [ ] 去掉Desktop-Gnome的√，点击Add additional software repostitories,选择Development->Developpent Tools<table><tr><td bgcolor=PowderBlue>这里的背景色是：PowderBlue</td></tr></table>
- [ ] 安装系统，第一次进入系统到Setup Agent界面是时，有倒计时，选择Firewall configuration关掉两个防火墙security level 和selinux，都是这disabled

## linux操作

![sdgfsd](.\images\image-20211023231905841.png)



![screenshots](.\images\screenshots.gif)

1. 查看网卡ip ifconfig
2. iptables -L查看第一道防火墙  sestatus第二道防火墙
3. 验证开发工具包是否安装rpm -qa |grep gcc 如果出现4条gcc记录证明安装好了
4. 用putty连接centos
5. nslookup域名反查命令，即根据域名查ip
6. 用WinSCP传输文件到centos


## linux基础命令  linux只有一个根目录/  所有文件都在根目录下
1. ls查看当前目录下的文件
2. pwd查看在哪个目录
3. 刚装完系统的root下有3个文件可删除，
4. ~代表用户的家目录，/代表根目录  /home普通用户家目录
5. cd -切换最近使用过的两个目录
6. <u>清空屏幕clear</u>   或ctrl+l
7. ctrl+c终端当前程序或操作
8. passwd user1修改用户user1的密码

## 认识linus目录
1. /home 普通用户家目录 除了root用户，其他用户都在/home下
2. cd    直接来到家目录
3. /mnt  测试目录
4. /tmp  临时目录日入文件上传时
5. /var  存放软件日志
6. /boot 系统启动文件 相当于windows
7. /etc  配置文件
8. /bin 所有用户都能执行的文件
9. /sbin 只有root才能执行的程序
10. /usr 用户自己的软件
11. /sys
12. /dev 存放硬件设备的地方
13. /medic 挂载光盘时

## 挂载光驱
1. mount /dev/cdrom /media
2. 进入光盘下运行rpm -ivh httpd-2.2.3-43.el5.centos.i386.rpm
3. 启动阿帕服务service httpd restart 然后在浏览器中输入linux服务器ip
4. df 查看光盘是否挂载


## 技巧命令
1. 查看命令在哪，如which init

## 文件管理
1. touch  file1 创建文件
2. vi file1修改文件
3. cat file查看文件   cat file1 | head -3  查看后3行  tail -3 后三行
4. mv file1 file2 把file移动到file2即剪贴或重命名
5. touch file{1..1000}创建1000个文件
6. history 查看历史命令
7. q!在编辑中强制退出不保存
8. :x保持退出
9. find /etc -name httpd.conf  查找文件
10. 1）updatedb 2）locate httpd.conf 快速查找文件
11. cat httpd.conf | grep -i Listen  查找文件中内容

## 目录操作
1. 创建目录mkdir dir1 dir2  连创两个目录    mkdir -p a/b/c/c/
2. 递归查看目录 tree  a
3. 删除目录 rm -rf dir dir2


## 用户管理
1. 添加用户useradd user1  passwd user1添加密码
2. 查看用户id user
3. 删除用户 userdel -r user1   r为递归式删除

## 别名管理
1. 把长命令简化为一个别名alias  kkkk='cat /etc/httpd/conf/httpd.conf'  kkk为别名
2. 删除别名 unalias kkk
3. 查看别名  alias


## 压缩包操作
1. 制作gz压缩包 tar czf filename.tar.gz  filename
2. 解压gz压缩包 tar xzf filename.tar.gz
3. 查看         tar tf filename.tar.gz

## zip压缩包
1. zip制作 zip -r 压缩文件名.zip   压缩文件名
2. 解压 unzip 文件名.zip
3. 查看压缩文件   unzip -l  文件名.zip



## 网络设置
1. 查看ip    ifconfig
2. 临时设置ip  ifconfig  eth0 192.168.60.9 
3. 永久设置ip vi /etc/sysconfig/network-scripts/ifcfg-eth0
`Advanced Micro Devices [AMD] 79c970 [PCnet32 LANCE]
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
HWADDR=00:0c:29:35:79:63`
改成 IPADDR=192.168.20.3
     NETMASK=255.255.255.0
	
## shell技巧
1. tab补全   按两下tab可以列出联想的词
2. history 查看历史命令
3. !203调用历史中第203号命令
4. !h调用历史中最后一次以h开头的命令
5. 用vi进入文本时可用查找命令  例子/Linster   再按n查找下一个
6. 输出当前日期date +%Y.%m.%d
7. ls | wc -l统计有多少文件


## 登入界面前运行程序
1. /ect.rc.d/rc.local 在里面写脚本如service httpd start
2. linux密码破解 分两次按下a,空格输1 进入单用户模式，设置密码

## yum
1. cd /etc/yum.repos.d/
2. 删掉网络源rm -rf CentOS-Base.repo
3. 编辑修改一下内容vi CentOS-Media.repo
4. baseurl=file:///media/CentOS/  删掉下面两行，去掉CentOS
        file:///media/cdrom/		删掉
        file:///media/cdrecorder/   删掉
		gpgcheck=1  改成0
		enabled=0   改成1


## 安装mysql 阿帕奇
1. yum -y install mysql-server*
2. 一键安装lamp yum -y install mysql*  httpd* php*
3. yumx卸载安装 yum -y remove mysql*
4. yum list 查看盘里的安装文件  yum list |grep httpd

## 权限管理 rwx读写执行
1. 查看文件权限 ls -l file
2. chmod o+x,o+w mnt
3. 目录的rwx  r查看目录里的文件4，w在目录创建和删除2，x切换进目录1
4. 文件的rwx  r查看文件内容，w在文件里写内容，x执行该文件（是程序或脚本）
5. chmod a+x my.sh  让所有用户对my.sh都拥有x权限
6. chmod o+x my.sh  让其他用户对my.sh都拥有x权限
7. setfacl -m u:user1:r mnt
8. setfacl -m u:user2:rx mnt
9. setfacl -m u:user3:rw mnt
10. setfacl -m u:user4:rwx mnt让user4拥有所以权限
11. 查看mnt拥有的权限 getfacl -m mnt
12. 删除user1对mnt权限		setfacl -x u:user1 mnt
13. 删除所有人的权限   setfacl -b mnt/
	
	
	
	
## sudo
1. 给非root用户添加命令权限 visudo 
 %users  localhost=/usr/sbin/useradd,/usr/sbin/userdel
2. 使用
sudo /usr/sbin/useradd user4
sudo /usr/sbin/userdel user4



## 软件安装
1. 查看已开端口netstat -tunpl
2. 查看进程pstree   pstree |grep httpd  查看阿帕奇进程  pstree -p该命令有进程号
3. 进入/etc/rc.d/init.d   下运行./httpd start    ./httpd stop  ./httpd.restart 绝大多数软件可以./运行
4. service httpd start  service能直接找到/etc/rc.d/init.d 
5. 修改阿帕奇端口vi /etc/httpd/conf/httpd.conf     Linten 8888
6. 查看进程  pstree | grep httpd
7. 查看端口 netstat -tunpl |grep  httpd
8. 关闭进程pkill httpd   查看有没有关掉 pstree  | grep httpd



## 实时观察cpu 内存情况top
1.  load average: 0.00, 0.00, 0.00  1分钟，5分钟，15分钟负载
2.  uptime命令 服务器工作时间  在线用户   平均负载信息
3.  who 获取目前在线用户的详细信息
4.  last 获取最近系统的重要操作
5.  按ctrl+c或q退出


## 任务计划
### date显示当前时间
1. 一次性计划在18:20重启ctrl+d为输完命令后结束
1）at 18：20
2）init 6
3）ctrl+d
4）查看任务atq
5）删除任务 atrm 2    2为任务序号
2. 周期计划crontab 
1）添加crontab -e
2) 查看crontab -l
3）删除crontab -r
3. 例子
* * * * * 分时日月周
00 03 * * * 每天3点
30 23 * * * 每天23:30
*/5 * * * * 每隔五分钟
59 23 * * 1-5 周一到周五
59 23 * * 1,3,5 周一、周三和周五的23:59


## 创建一个执行脚本
1. 创建一个执行脚本:
`vi web.sh
#!/bin/bash
DATE=`date +%Y-%m-%d`
tar czf /tmp/web-${DATE}.tar.gz
/var/www/html
rsync -a /tmp/web-${DATE}.tar.gz /mnt`

2. 对网站压缩备份
#### 每周一3点进行备份
touch backup.sh
vi backup.sh
chmod a+x backup.sh
zip -r 压缩名.zip   /var/www/html/网站文件名 &>/dev/null   &>/dev/null是不在屏幕输出内容

### 第一步写backup.sh脚本中的内容html下的wbb文件夹是网站内容，脚本在根目录下，执行时要切换到根目录
t=`date +%Y-%m-%d`
f="wbb-${t}.zip"
cd /var/www/html/
zip -r $f wbb &>/dev/null
mv $f /mnt                 //这一行可去掉，直接压缩到网站根目录下，方便下载
### 第二步写任务计划
00 03 * * 1  /root/backup.sh
### 第三步查看备份文件
ls /mnt
查看备份的压缩包文件unzip -l wbb-2020-06-20.zip  |more



## linux源代码（C语言）编译
free -m查内存
fdisk -l查硬盘  df -h查分区情况
1. 生成编译配置文件（MakeFile）解压源程序包到/mnt 进入解压后的httpd-2.2.9文件夹中运行如下命令
./configure --prefix=/usr/local/apache     //安装到/usr/local/apache
2. 开始编译(Make)
3. 开始安装(Make install) 完成后cd /usr/local/   下有个apache目录
4. apache目录下 cd bin     ./apachectl start     开启阿帕奇服务   ./apachectl start关闭服务
5. pstree |grep httpd 查看进程httpd服务是否开启
6. netstat -tunpl |grep httpd查看端口
7. 浏览器输入ip地址打开主页看到It works！
8. rpm -qa |grep gcc查看系统中是否安装过gcc编译器，若没有使用yum安装 yum -y instll gcc*
9. 检查系统中是否安装了lamp环境rpm -qa |grep httpd,  rpm -qa |grep mysql,  rpm -qa |grep php 
 10. 如果已安装则把rpm安装的lamp环境卸载 yum remove httpd， yum remove mysql ， yum remove php
 11. 源代码安装的apache如何卸载，直接到安装目录删除apache文件夹rm -rf apache/   再pkill httpd杀掉进程


## linux源码包解压安装  先解压gz压缩包，再进入文件夹运行语句
1）libxml2
./configure --prefix=/usr/local/libxml2 && make&& make install 
2）libmcrypt
./configure --prefix=/usr/local/libmcrypt && make&& make install 
3)libltdl
./configure --enable-ltdl-install && make&& make install
4)zlib
./configure && make && make install
5)libpng
./configure --prefix=/usr/local/libpng/  && make&& make install
6)jpge 先创建5个目录，下面5个mkdir可一起复制运行
mkdir /usr/local/jpeg6
mkdir /usr/local/jpeg6/bin
mkdir /usr/local/jpeg6/lib
mkdir /usr/local/jpeg6/include
mkdir -p /usr/local/jpeg6/man/man1
./configure --prefix=/usr/local/jpeg6/ --enable-shared --enable-static && make && makeinstall
7)freetype
./configure --prefix=/usr/local/freetype/ && make && make install
8)autoconf
./configure && make && make install
9)GD库 首先把#include “png.h”替换如下
gd安装文件夹中编辑vi gd_png.c把其中一条改成#include "/usr/local/libpng/include/png.h" 
./configure --prefix=/usr/local/gd2/ --with-jpeg=/usr/local/jpeg6/ --with-freetype=/usr/local/freetype/ --with-png=/usr/local/libpng/ && make&& make install
若出现error上面一条语句再执行一遍
.


### 安装apache
./configure --prefix=/usr/local/apache2/ --sysconfdir=/usr/local/apache2/etc/ --with-included-apr --enable-dav  --enable-so --enable-deflate=shared --enable-expires=shared  --enable-rewrite=shared   && make&& make install
安装完到cd /usr/local/apache2/bin   执行命令 ./apachectl start开启httpd服务
 查看httpd进程ps -le | grep httpd
然后再设置开机启动httpd服务 vi /etc/rc.d/rc.local   添加脚本一行/usr/local/apache2/bin/apachectl start


### 安装mysql  rpm -qa  查看系统了安装多少包
1. 安装ncurses   
rpm安装方法） 
进系统光盘 mount /dev/cdrom /media ,   cd CentOS ,  查找 ls ncurse*   ,rpm -ivh ncurses-devel-5.5-24.20060715.i386.rpm
yum安装方法
yum –y install ncurses*

2. 安装mysql
./configure --prefix=/usr/local/mysql --without-debug
--enable-thread-safe-client --with-pthread --enable-assembler
--enable-profiling --with-mysqld-ldflags=-all-static
--with-client-ldflags=-all-static --with-extra-charsets=all
--with-plugins=all --with-mysqld-user=mysql --without-embedded-server
--with-server-suffix=-community
--with-unix-socket-path=/tmp/mysql.sock  &&  make && make install


以上即./configure --prefix=/usr/local/mysql --without-debug  --enable-thread-safe-client --with-pthread --enable-assembler  --enable-profiling --with-mysqld-ldflags=-all-static  --with-client-ldflags=-all-static --with-extra-charsets=all  --with-plugins=all --with-mysqld-user=mysql --without-embedded-server  --with-server-suffix=-community --with-unix-socket-path=/tmp/mysql.sock  && make && make install
#### 安装完mysql后
 1. useradd mysql添加用户
 2. setfacl -m u:mysql:rwx -R /usr/local/mysql/设置权限
 3. setfacl -m d:u:mysql:rwx -R /usr/local/mysql/
 4. cp /usr/local/mysql/share/mysql/my-medium.cnf /etc/my.cnf
		修改mysql 配置文件
		[client]
		default-character-set=utf8
		[ mysqld]
		character-set-server = utf8
		collation-server = utf8_general_ci
5. 安装mysql 和test 数据库 执行mysql_install_db命令，执行晚后 cd /usr/local/mysql/  多了个var文件夹 /usr/local/mysql/bin/mysql_install_db --user=mysql
6. 启动mysql服务器 /usr/local/mysql/bin/mysqld_safe --user=mysql &   运行后回车
7. 修改MySQL密码   /usr/local/mysql/bin/mysqladmin -uroot password kkk
8. 登入mysql测试  /usr/local/mysql/bin/mysql -u root -pkkk test
9. 修改mysql 的登录密码 /usr/local/mysql/bin/mysqladmin -uroot password kkk
10. 干掉mysql进程 pkill mysqld ,查看进程pstree |grep mysqld
11. 启动进程 [](http://192.168.60.128/phpMyAdmin)
12. 设置mysql 开机启动 vi /etc/rc.local  ,/usr/local/mysql/bin/mysqld_safe --user=mysql &      不加$z的话屏幕会挂住不释放


### 安装php
#### 先安装libtool-ltdl 软件包                                                                 
rpm -qa|grep libtool  查看已安装的，安装了1个，进盘查看cd /media/CentOS,  ls libtool*  ,还有两个包安装rpm -ivh libtool-ltdl-*
开始安装
	./configure --prefix=/usr/local/php/  --with-config-file-path=/usr/local/php/etc/  --with-apxs2=/usr/local/apache2/bin/apxs --with-mysql=/usr/local/mysql/  --with-libxml-dir=/usr/local/libxml2/ --with-jpeg-dir=/usr/local/jpeg6/  --with-png-dir=/usr/local/libpng/ --with-freetype-dir=/usr/local/freetype/  --with-gd=/usr/local/gd2/ --with-mcrypt=/usr/local/libmcrypt/  --with-mysqli=/usr/local/mysql/bin/mysql_config --enable-soap  --enable-mbstring=all --enable-sockets && make && make install
安装完后cd /mnt/php-5.2.6
	cp /php-5.2.6/php.ini-dist  /usr/local/php/etc/php.ini
	进入/usr/local/apache2/etc   ,vi httpd.conf   查找/index.html  ,在他之前添加index.php,重启httpd命令为/usr/local/apache2/bin/apachectl restart
让Apache 支持PHP 扩展库
	修改httpd.conf
	vi /usr/local/apache2/etc/httpd.conf
	AddType application/x-httpd-php .php .phps //在文件最后添加这一行shift+g到最后一行
	
	
## 安装php扩展如pdo扩展
进入解压缩后的扩展文件夹运行/usr/local/php/bin/phpize  运行后文件夹多了个configure
编译安装pdo
./configure --with-php-config=/usr/local/php/bin/php-config --with-pdo-mysql=/usr/local/mysql && make && make install
安装完后复制进入最后一行所指路径 /usr/local/php/lib/php/extensions/no-debug-non-zts-20060613/  会看到php_mysql.so
进入php的配置文件cd /usr/local/php/etc/    vi php.ini  查找/extension
	修改为如下：
	extension_dir ="/usr/local/php/lib/php/extensions/no-debug-non-zts-20060613/"
	extension="pdo_mysql.so";这行是添加
重启apache    /usr/local/apache2/bin/apachectl restart


## 安装完lamp后小面脚本可能已做过 检查一下 
### vi /etc/rc.d/rc.local   添加如下命令
mount /dec/cdrom /media
/usr/local/apache2/bin/apachectl start
echo 'qidong apache'
sleep 3
echo 'qidong mysql'
sleep 3
/usr/local/mysql/bin/mysqld_safe --user=mysql &


## 设置
 设置daemon用户对网站根目录的权限 setfacl -m u:daemon:rwx -R htdocs/  ,  setfacl -m d:u:daemon:rwx -R htdocs/   d代表以后新建的都有这个权限，这样php上传下载文件才能用
 ## 安装discuz
把bbs的文件夹放到网站目录下，浏览器访问bbs目录，点同意安装，检查目录权限状态显示不可写时，给个权限如下命令：运行时先进入apache目录
setfacl -m u:daemon:rwx -R htdocs/  ,  setfacl -m d:u:daemon:rwx -R htdocs/














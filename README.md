## 常用Linux环境安装集合

### VirtualBox安装
注:此处安装演示环境为OS X EI Capitan 10.11.6<br/>
1.从官网下载最新版的安装包进行安装<br/>
&nbsp;&nbsp;&nbsp;安装包下载地址:https://www.virtualbox.org<br/>
2.双击.dmg进行安装<br/>
3.将.app文件放置在/Applications目录下<br/>

##### VirtualBox-OpenSuSE安装增强功能
	注:需要使用文件共享、粘贴复制等功能时的需要<br/>
	1.从安装包中的iso挂载<br/>
	2.在实例窗口中选择(设备->安装增强功能)<br/>
	3.挂载相关的扩展包内容到制定磁盘(如下命令)<br/>
	mount /dev/cdrom /mnt/<br/>
	4.依赖环境安装检查与安装(如下命令)<br/>
	yum install -y gcc gcc-devel gcc-c++-devel make kernel-devel<br/>
	5.进行增加功能的安装(如下命令)<br/>
	1.cd /mnt/<br/>
	2../VBoxLinuxAdditions.sh<br/>
	6.当安装成功后会有提示让您输入(reboot)命令进行重启

### OpenSuSE安装
注:此处使用VirtualBox进行安装并且OpenSuse使用在线安装模式<br/>
1.安装镜像源下载地址:<br/>
&nbsp;&nbsp;&nbsp;镜像下载地址:<br/>
2.使用VirtualBox虚拟机装载iso镜像文件<br/>

#### 重点截图
1.当出现如下画面后选择[<b>安装</b>]<br/>
![图片加载](Linux/img1.png)
2.当出现如下画面后请根据图片步骤进行操作
![图片加载](Linux/img2.png)
![图片加载](Linux/img3.png)
![图片加载](Linux/img4.png)
注:opensuse中科大镜像地址为:http://mirrors.ustc.edu.cn/opensuse/
![图片加载](Linux/img5.png)
![图片加载](Linux/img6.png)
![图片加载](Linux/img7.png)
![图片加载](Linux/img8.png)
![图片加载](Linux/img9.png)
![图片加载](Linux/img10.png)
3.zypper install -t pattern kde4 kde4\_basis(安装图形化界面)</br>


### Sun Jdk安装与配置
1.从http://www.oracle.com/technetwork/java/javase/downloads/index.html下载(jdk-8u121-linux-x64.tar.gz)<br/>
2.在Linux的/home目录下创建java的目录(mkdir /home/java)<br/>
3.将jdk-8u121-linux-x64.tar.gz使用cp命令复制到/home/java目录下<br/>
4.使用tar -xf jdk-8u121-linux-x64.tar.gz 进行解压<br/>
5.使用 vi /etc/profile 环境变量配置（配置内容如下)<br/>
  JAVA\_HOME=/home/java/jdk1.8.0\_121<br/>
  CLASSPATH=.:$JAVA\_HOME/lib/tools.jar:$JAVA\_HOEM/lib/dt.jar<br/>
  PATH=$JAVA\_HOME/bin:$PATH<br/>
  export JAVA\_HOME CLASSPATH PATH<br/>
6.修改系统默认的java指向<br/>
alternatives --install /usr/bin/java java /home/java/jdk1.8.0\_121/bin/java 500<br/>
7.使用java -version查看命令是否可用<br/>

### Oracle 11g安装
##### 非静默安装
1.从官网下载2个文件分别为linux.x64\_11gR2\_database\_1of2.zip与linux.x64\_11gR2\_database\_2of2.zip(https://www.oracle.com/downloads/index.html)<br/>
2.在Linux的/home路面下面创建oracle的目录(mkdir /home/oracle)<br/>
3.将压缩包zip使用cp 命令复制到/home/oracle目录下<br/>
4.使用unzip命令解压文件 unzip linux.x64\_11gR2\_database\_1of2.zip<br/>
5.使用unzip命令解压文件 unzip linux.x64\_11gR2\_database\_2of2.zip<br/>
6.内核参数修改如下<br/>
&nbsp;&nbsp;&nbsp;vi /etc/sysctl.conf<br/>
&nbsp;&nbsp;&nbsp;fs.aio-max-nr = 1048576<br/>
&nbsp;&nbsp;&nbsp;fs.file-max = 6815744<br/>
&nbsp;&nbsp;&nbsp;kernel.shmall = 2097152<br/>
&nbsp;&nbsp;&nbsp;kernel.shmmax = 536870912<br/>
&nbsp;&nbsp;&nbsp;kernel.shmmni = 4096<br/>
&nbsp;&nbsp;&nbsp;kernel.sem = 250 32000 100 128<br/>
&nbsp;&nbsp;&nbsp;net.ipv4.ip\_local\_port\_range = 9000 65500<br/>
&nbsp;&nbsp;&nbsp;net.core.rmem\_default = 262144<br/>
&nbsp;&nbsp;&nbsp;net.core.wmem\_default = 262144<br/>
&nbsp;&nbsp;&nbsp;net.core.rmem\_max = 4194304<br/>
&nbsp;&nbsp;&nbsp;net.core.wmem\_max = 1048586 <br/>
7.要使/etc/sysctl.conf 更改立即生效，执行以下命令 sysctl -p <br/>
8.vi /etc/security/limits.conf,修改操作系统对oracle用户资源的限制<br/>
&nbsp;&nbsp;&nbsp;oracle	soft	nproc	2047<br/>
&nbsp;&nbsp;&nbsp;oracle	hard	nproc	16384<br/>
&nbsp;&nbsp;&nbsp;oracle	soft	nofile	1024<br/>
&nbsp;&nbsp;&nbsp;oracle	hard	nofile	65536<br/>
&nbsp;&nbsp;&nbsp;oracle	hard	stack	10240<br/>
9.安装vncserver服务 yum -y install tigervnc-server<br/>
10.启动vncserver服务(vncserver)<br/>
10.export DISPLAY=localhost:1<br/>
11.xhost +<br/>
12.groupadd oracle(添加oracle群组)<br/>
13.useradd -g oracle oracle(添加oracle群组下的oracle用户)<br/>
14.passwd oracle(设置oracle的密码)<br/>
15.安装前所需要的依赖包：<br/>
&nbsp;&nbsp;&nbsp;binutils-2.17.50.0.6-2.el5<br/>
&nbsp;&nbsp;&nbsp;compat-libstdc++-33-3.2.3-61<br/>
&nbsp;&nbsp;&nbsp;elfutils-libelf-0.125-3.el5<br/>
&nbsp;&nbsp;&nbsp;elfutils-libelf-devel-0.125<br/>
&nbsp;&nbsp;&nbsp;elfutils-libelf-devel-static<br/>
&nbsp;&nbsp;&nbsp;glibc-2.5-12<br/>
&nbsp;&nbsp;&nbsp;glibc-common-2.5-12<br/>
&nbsp;&nbsp;&nbsp;kernel-headers<br/>
&nbsp;&nbsp;&nbsp;ksh<br/>
&nbsp;&nbsp;&nbsp;libaio-0.3.106<br/>
&nbsp;&nbsp;&nbsp;libaio-devel-0.3.106<br/>
&nbsp;&nbsp;&nbsp;libgcc-4.1.1-52<br/>
&nbsp;&nbsp;&nbsp;libgomp<br/>
&nbsp;&nbsp;&nbsp;libstdc++-4.1.1<br/>
&nbsp;&nbsp;&nbsp;libstdc++-devel-4.1.1-52.e15<br/>
&nbsp;&nbsp;&nbsp;make-3.81-1.1<br/>
&nbsp;&nbsp;&nbsp;mpfr-2.4.1-6.el6.i686.rpm<br/>
&nbsp;&nbsp;&nbsp;ppl-0.10.2-11.el6.i686.rpm<br/>
&nbsp;&nbsp;&nbsp;sysstat-7.0.0<br/>
&nbsp;&nbsp;&nbsp;unixODBC-2.2.11<br/>
&nbsp;&nbsp;&nbsp;unixODBC-devel-2.2.11<br/>
&nbsp;&nbsp;&nbsp;glibc-headers-2.5-12<br/>
&nbsp;&nbsp;&nbsp;glibc-devel-2.5-12<br/>
&nbsp;&nbsp;&nbsp;cloog-ppl-0.15.7-1.2.el6.i686.rpm<br/>
&nbsp;&nbsp;&nbsp;cpp-4.4.4-13.el6.i686.rpm<br/>
&nbsp;&nbsp;&nbsp;gcc-4.1.1-52<br/>
&nbsp;&nbsp;&nbsp;gcc-c++-4.1.1-52<br/>
&nbsp;&nbsp;&nbsp;numactl-devel-0.9.8.i386<br/>
16.编辑配置文件vi .bash_profile,添加如下配置<br/>
umask 022<br/>
export ORACLE_BASE=/home/oracle/app <br/>
export ORACLE_HOME=$ORACLE_BASE/oracle/product/11.2.0/dbhome_1 <br/>
export ORACLE_SID=orcl <br/>
export PATH=\$PATH:\$HOME/bin:$ORACLE\_HOME/lib:/usr/lib <br/>
export LD\_LIBRARY\_PATH=\$ORACLE\_HOME/lib:/usr/lib</br>
17.su oracle(使用oracle进行安装)<br/>
18.export LANG=en\_US.UTF-8<br/>
19.创建数据库软件目录和数据文件存放目录，目录的位置，根据自己的情况来定，注意磁盘空间即可，这里我把其放到oracle用户下<br/>
mkdir /home/oracle/app<br/>
mkdir /home/oracle/app/oracle<br/>
mkdir /home/oracle/app/oradata<br/>
mkdir /home/oracle/app/oracle/product</br>
20.更改目录属主为Oracle用户所有，输入命令：chown -R oracle:oracle /home/oracle/ <br/>
21.进入到安装目录下运行脚本	 cd /home/oracle/database<br/>
22.运行安装程序 ./runInstaller <br/>
23.安装完后执行配置脚本

### Hadoop 安装

1.从http://www.oracle.com/technetwork/java/javase/downloads/index.html下载(jdk-8u121-linux-x64.tar.gz)<br/>
2.在Linux的/home目录下创建java的目录(mkdir /home/java)<br/>
3.将jdk-8u121-linux-x64.tar.gz使用cp命令复制到/home/java目录下<br/>
4.使用tar -xf jdk-8u121-linux-x64.tar.gz 进行解压<br/>
5.使用 vi /etc/profile 环境变量配置（配置内容如下)<br/>
JAVA\_HOME=/home/java/jdk1.8.0\_121<br/>
CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA\_HOEM/lib/dt.jar<br/>
PATH=$JAVA\_HOME/bin:$PATH<br/>
export JAVA\_HOME CLASSPATH PATH<br/>
6.修改系统默认的java指向 alternatives --install /usr/bin/java java /home/java/jdk1.8.0\_121/bin/java 500 <br/>
7.使用java -version查看命令是否可用<br/>
8.mkdir /home/hadoop 创建hadoop文件夹信息 并且使用cd /home/hadoop进入到该文件夹当中<br/>
9.从http://mirrors.cnnic.cn/apache/hadoop/common/下载(hadoop-2.7.3.tar)<br/>
10.使用tar xf hadoop-2.7.3.tar进行解压<br/>
11.vi /home/hadoop/etc/hadoop/hadoop-env.sh 编写如下配置信息<br/>找到JAVA变量进行相关的内容
JAVA\_HOME=/home/java/jdk1.8.0\_121<br/>
12.进入/home/hadoop/sbin(cd /home/hadoop/sbin)<br/>
13.执行启动文件进行启动测试(./start-all.sh)


### Redis 安装

### Hbase 安装

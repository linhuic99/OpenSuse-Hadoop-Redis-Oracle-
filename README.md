## 常用Linux环境安装集合

### VirtualBox安装
注:此处安装演示环境为OS X EI Capitan 10.11.6<br/>
1.从官网下载最新版的安装包进行安装<br/>
&nbsp;&nbsp;&nbsp;安装包下载地址:https://www.virtualbox.org<br/>
2.双击.dmg进行安装<br/>
3.将.app文件放置在/Applications目录下<br/>

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
&nbsp;&nbsp;&nbsp;net.core.rmem\_max = 4194304<br/>
&nbsp;&nbsp;&nbsp;net.core.wmem\_default = 262144<br/>
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
15.su oracle(使用oracle进行安装)<br/>
16.export LANG=en\_US.UTF-8<br/>
18.创建数据库软件目录和数据文件存放目录，目录的位置，根据自己的情况来定，注意磁盘空间即可，这里我把其放到oracle用户下<br/>
mkdir /home/oracle/app<br/>
mkdir /home/oracle/app/oracle<br/>
mkdir /home/oracle/app/oradata<br/>
mkdir /home/oracle/app/oracle/product</br>
19.更改目录属主为Oracle用户所有，输入命令：chown -R oracle:oracle /home/oracle/ <br/>
20.进入到安装目录下运行脚本	 cd /home/oracle/database<br/>
21.运行安装程序 ./runinstall

### Hadoop 安装

### Redis 安装

### Hbase 安装

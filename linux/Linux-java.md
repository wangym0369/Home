# <a name="top">Web应用程序的部署</a>

+ <a href="#jdk">**JDK安装**</a>


+ <a href="#mysql_install">**MySQL安装**</a>


+ <a href="#redis">**Redis的安装**</a>




-----

## <a name="jdk">JDK安装</a>

+ 解压 `jdk` 到指定目录

  ```shell
  mkdir -p /home/hurrican/jdk
  cd /home/hurrican/jdk

  # 将 jdk 压缩包解压到 /home/hurrican/jdk 目录
  tar -zxvf jdk-8u144-linux-x64.tar.gz -C ./
  ```

+ 配置 `java` 环境变量

  ```shell
  vim /etc/profile

  # 在最后面追加以下内容，其中jdk解压路径(/home/hurrican/jdk)以各自具体的路径为准
  export JAVA_HOME=/home/hurrican/jdk/jdk1.8.0_181
  export CLASSPATH=.:$JAVA_HOME/lib
  export PATH=JAVA_HOME/bin:PATH

  ```

+ **使配置的环境变量生效**

  ```shell
  source /etc/profile

  # 查看是否成功配置 java 环境变量
  java -version
  ```

+ 配置加快 `Tomcat` 启动的**Java**系统属性

  ```shell
  # 查找 java.security 所在的文件路径
  locate java.security

  # 若未找到 java.security 文件，先检查是否安装了jdk
  # 安装 jdk 还是没有找到可以使用 updatedb 命令刷新一下 Linux 文件数据库
  updatedb

  # 在运行 locate java.security 命令后输出内容示例如下：
  # /home/hurrican/jdk/jdk1.8.0_181/jre/lib/security/java.security

  vim /home/hurrican/jdk/jdk1.8.0_181/jre/lib/security/java.security

  # 搜索 securerandom.source
  #  将 securerandom.source=file:/dev/random 改为 securerandom.source=file:/dev/./urandom
  ```

  ​

    

<p align="right"><a href="#jdk">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a></p>

-----

## <a name="mysql_install">**MySQL5.7安装**</a>

+ **准备** ：
```shell
apt update

# 查看 apt-get install mysql-server 可以安装的 MySQL 版本
apt-cache search mysql|grep mysql-server

# 获取 MySQL5.7 版本相关文件
wget -P /home/mysql http://dev.mysql.com/get/mysql-apt-config_0.8.0-1_all.deb
dpkg -i /home/mysql/mysql-apt-config_0.8.0-1_all.deb

apt-get update

# 安装 MySQL 服务器，过程略
apt-get install mysql-server

```

***安装过程中有个输入 root 账户密码的步骤，需要记住这个密码***



+ **配置MySQL5.7**
登录 `MySQL` 服务器
```mysql
mysql -u root -p
Enter password: 

# 以 root 身份登录进去后创建1个允许远程访问的用户
# 语法： create user '用户名'@'IP' identified by '密码';
# IP 选项中 % 是通配符，表示允许所有用户登录
create user 'Hurrican'@'%' identified by 'Xmx256Xms128';

# 刷新用户权限
flush privileges;

```
**备注**:
+ 若进行上述操作任**无法使用外网访问服务器**上的 `MySQL` 时可以参考<a href="https://www.cnblogs.com/funnyboy0128/p/7966531.html">这篇博客</a>




<p align="right"><a href="#mysql_install">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a></p>


----
## <a name="redis">Redis的安装</a>

<a href="http://download.redis.io/releases/">**Redis源码压缩包下载地址**</a>

需要装 `redis-4.0.0` 可以使用 ` wget http://download.redis.io/releases/redis-4.0.0.tar.gz` 将资源下载到服务器，然后再**编译安装**

+ 解压下载后的 `redis` 压缩包 —— `tar -zxvf redis-4.0.0.tar.gz -C /usr/redis`

+ 进入解压后的目录，执行 `make` 命令

+ 接着执行 `make test`

+ 继续执行 `make install`

+ **启动** & **停止** Redis服务
```sh
# 启动 redis 服务端：redis-server 配置文件名
redis-server /etc/redis/redis.conf

# 停止 redis 服务
redis-cli -h 127.0.0.1 -p 6379 shutdown
```


**make test** 过程中若出现 `You need tcl 8.5 or newer in order to run the Redis test` 错误需要先安装 `tcl`
```shell
wget http://downloads.sourceforge.net/tcl/tcl8.6.1-src.tar.gz 
tar xzvf tcl8.6.1-src.tar.gz  -C /usr/local/
cd  /usr/local/tcl8.6.1/unix/  
./configure  
make  
make install   
```





<p align="right"><a href="#redis">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a></p>


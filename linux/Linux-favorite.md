# <a name="top">Linux常用命令</a> 

+ <a href="#netstat">`netstat`</a>

+ <a href="#ps">**进程**</a>

+ <a href="#echo">`echo`</a>

+ <a href="#disk">**磁盘**</a>

+ <a href="#userManage">**用户管理**</a>

+ <a href="#head_tail">`head & tail`</a>

+ <a href="#network_monitor">**网络监控**</a>

+ <a href="#iptables">**防火墙**</a>

----

## <a name="netstat">netstat</a>

+ `netstat` **-ntlp**  —— 显示**TCP相关**的进程监听的端口信息
  + `-a (all)`：显示所有选项，默认不显示LISTEN相关
  + `-t (tcp)`：仅显示tcp相关选项
  + `-u (udp)`：仅显示udp相关选项
  + `-n`：拒绝显示别名，能显示数字的全部转化成数字
  + `-l `：仅列出有在 Listen (监听) 的服務状态
  + `-p`：显示建立相关链接的程序名
  + `-s`：按各个协议进行统计
  + `-T (show threads)`：显示线程





+  `netstat -nlt | grep 330[67]` —— 查看`3306、3307`端口监听情况
    ![netstat-nlt](https://github.com/HurricanGod/Home/blob/master/linux/img/netstat-nlt.png)

+  `netstat -tulp n` —— 显示对应进程**pid**的网络端口


+ `nbtstat -A x.x.x.x` —— `x.x.x.x`为ip地址，该命令用于获取ip地址对应的域名


+ `lsof -i:端口号` —— 根据端口号查看进程
  ![](https://github.com/HurricanGod/Home/blob/master/linux/img/lsof.png)


+ `ps -T -p pid` —— 显示进程 `pid` 包含的线程
  ![thread_in_pid]()

<p align="right"><a href="#netstat">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

----

## <a name="ps">进程</a>

+ ***查找进程***
  `ps -ef|grep 搜索串` —— 查看含有**搜索串**的进程信息


+ ***查找僵尸进程并kill掉***

```shell
# 列出进程表中的僵尸进程
ps aux|grep Z

# 杀掉僵尸进程
kill -s SIGCHLD pid
```



<p align="right"><a href="#ps">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

----

## <a name="echo">echo命令</a>



+ **清空文件**  →  `echo '' > 文件名`


+ **控制输出** —— `-e`选项后面的参数(**字符串**)可以有转义字符
  + `\c` —— 出现在参数最后的位置，在`\c`之前的参数被显示后，光标不换行，新输出的内容接在该行的后面

    ```shell
    echo -e "Hello\t\c" && echo "World"
    # Hello	World
    ```

    ​
+ `-n换行输出`




<p align="right"><a href="#echo">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

----

## <a name="type">**type** —— 找出给定命令的信息</a>

+ `type -p command` —— 找出给定命令的绝对路径
+ `type -a command` —— 找出并显示命令的所有信息

![type](https://github.com/HurricanGod/Home/blob/master/linux/img/type.png)



------

## <a name="disk">磁盘</a>

### <a name="du">磁盘使用情况 —— **du**</a>

> du(disk usage)——用于查找文件或目录的磁盘使用情况

```shell
#  显示 `/home`目录下的所有文件和目录以及显式块大小
du -h /home

# 目录的总磁盘大小
du -sh /home

```

![du-h](https://github.com/HurricanGod/Home/blob/master/linux/img/du-h.png)



------

### <a name="df">磁盘利用率 —— **df**</a>

```shell
# 显示设备名称、总块数、总磁盘空间、已用磁盘空间、可用磁盘空间和文件系统上的挂载点
df -h

# 显示特定分区信息
df -hT /home
```


![](https://github.com/HurricanGod/Home/blob/master/linux/img/dfh.png)

<p align="right"><a href="#disk">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

------

<a name="calulateFileCount">**统计当前目录的文件**</a>

 `ls -l .|egrep -c '^-'`

+ `-l` —— 以列表形式显式
+ `.` —— 指定 `ls` 命令操作的路径，`.`表示当前路径
+ `-c` —— 通用输出控制
+ `^-` —— 以`-`开头的行，`ls -l`命令的结果**若行首为 - 代表普通文件**




----

<a name="kill">**kill**命令</a>

```shell
kill [-alpsu] pid
a: 当处理当前进程时，不限制命令名和进程号的对应关系
l: l参数会列出全部的信息名称
p: kill 命令只打印相关进程的进程号，而不发送任何信号
s: 指定要送出的信息
```



<a href="http://man.linuxde.net/kill">参考博客</a>

-----

<a name="history">**history**</a>

> 显示用户之前执行的bash脚本历史记录



-----

## <a name="userManage">用户管理</a>

| 命令                           | 描述            |
| :--------------------------- | :------------ |
| `useradd new-user`           | 创建一个先的linux用户 |
| `passwd username`            | 重置Linux用户密码   |
| `deluser username`           | 删除一个用户        |
| `chgrp username filename -R` | 改变文件所属用户组     |
| `chown username filename -R` | 改变文件所属用户      |



<p align="right"><a href="#userManage">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

------

## <a name="head_tail">head & tail</a>

**通过管道截取上一条命令的前n行**
```shell
head -n 10 file
head -10 file
# file 为文件名
# 管道组合使用：
ll |head -2	# 输出ll命令结果的前2行
```

**通过管道截取上一条命令的最后n行**

```shell
tail -n 10 file
tail -10 file
# file 为文件名
ll |tail -2	# 输出ll命令结果的最后两行
```

<p align="right"><a href="#head_tail">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

-----
## <a name="network_monitor">网络监控</a>
```shell
# 安装 iftop 工具
apt install iftop

# 查看网卡信息
ifconfig

# 监控网络
iftop -i eth0
```


<p align="right"><a href="#network_monitor">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p>

----

## <a name="iptables">防火墙</a>

+ 添加过滤规则

  ```shell
  iptables -t filter -A INPUT -p tcp -m tcp --dport 8080 -s localhost -j ACCEPT

  iptables -t filter -A INPUT -p tcp -m tcp --dport 8080 -j REJECT
  ```

  + `-p` 参数：用于指定协议
  + `-dport`参数： 指定目标端口，指数据从外网访问服务器使用的端口号
  + `-sport`参数：数据源端口，指从服务器出去的端口
  + `-j`参数：**ACCEPT**表示接收

 <p align="right"><a href="#iptables">返回</a>&nbsp&nbsp|&nbsp&nbsp<a href="#top">返回目录</a><p> 

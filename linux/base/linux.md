# <a name="top">Linux常识</a>

+ <a href="#user">**用户**</a>


+ <a href="#file">**文件**</a>


+ <a href="#command">**常用命令**</a>


+ <a href="#tip">**事半功倍的小提示**</a>


------

## <a name="file">**文件**</a>

**背景**：

> 在Linux系统中不管是可执行文件、软件、压缩包还是文件夹都统称为文件。
>
> 跟现实世界一样，一个物品属于一个人或群体，在Linux系统中文件也有这个属性，即文件会属于某一个用户。
>
> 

<a name="priviledges">**Linux**中文件有3种权限：</a>

+ `读权限`

  +  **什么是读权限？** —— 哪`Windows`系统来类比，当你打开一个文件查看内容时就是**在使用读权限** ，`Linux`中也一样你查看文件中的内容就是要**有读权限** ，若**没有读权限**将不能打开文件读取内容
  +  **谁可以读文件？**
     + <a href="#user">`root用户`</a>
     + 文件的主人——使用 `ls -l(有些地方可以简写为ll)`查看文件所属主人
     + ![file_ll](https://github.com/HurricanGod/Home/blob/master/linux/base/img/file_ll.png)
     + **待补充...**

+ `写权限`

  + **写权限是什么？**——**写权限**是指用户对**文件内容的修改**、 **重命名**、**删除文件**等权限
  + **谁可以写文件？**
    + <a href="#user">`root用户`</a>
    + 文件的主人

+ `执行权限`

  + **怎样理解执行权限？**——**执行权限**相当于`Windows`下**双击软件运行**的权限

  + 一般具有执行权限的文件都是**绿色**的

    ![enable_exec](https://github.com/HurricanGod/Home/blob/master/linux/base/img/enable_exec.png)



<p align="right"><a href="#priviledges">返回</a>|<a href="#top">返回目录</a></p>

----

## <a name="user">用户</a>



`Linux` 用户概括地来说很两种：

+ 普通用户
+ 超级用户 —— `root` ，具有最高权限。可以理解为管理员，**可以用户行使所有用户的权限**，比如可以读写执行其它用户的文件。

![root_flag](https://github.com/HurricanGod/Home/blob/master/linux/base/img/root_flag.png)



<p align="right"><a href="#user">返回</a>|<a href="#top">返回目录</a></p>

----

## <a name="command">**常用命令**</a>

+ `cd` —— 切换文件夹，使用方法见下图：

  ![cd](https://github.com/HurricanGod/Home/blob/master/linux/base/img/cd.gif)

  ```shell
  # 假设当前路径为 /hurrican/linux/test
  # 使用 pwd 检验当前路径是否为  /hurrican/linux/test
  # cd .. 跳转到 /hurrican/linux 目录
  cd ..

  # cd ../../ 跳转到 /hurrican 目录
  cd ../../

  # 假设 /hurrican 目录有 maven 目录，可以使用如下目录记录 /hurrican/maven
  cd ../maven
  ```

  ​


+ `pwd` —— 显示当前目录，见上图


<p align="right"><a href="#command">返回</a></p>



+ `mkdir` —— 创建文件夹

  + `mkdir /hurrican` —— 将创建`hurrican`文件夹
  + `mkdir -p /hurrican/linux/test` ——  `-p`选项用户递归创建文件夹。例如在存在`hurrican`文件夹情况下，若`linux文件夹`不存在则会**先创建linux文件夹**， 创建成功后再创建 `test` 文件夹

  ![mkdir](https://github.com/HurricanGod/Home/blob/master/linux/base/img/mkdir.gif)


<p align="right"><a href="#command">返回</a></p>

+ `touch` —— **新建文件**

  ```shell
  # 创建 hello.txt 文件，里面什么内容也没有
  touch hello.txt
  ```

  ​




<p align="right"><a href="#command">返回</a></p>

+ `mv` —— **移动文件** or **文件重命名**

  ```shell
  # 假设当前目录为 /hurrican/linux/test
  # 使用 pwd 检验当前路径是否为  /hurrican/linux/test
  # /hurrican/linux 下有 test 文件夹 和 my 文件夹
  # /hurrican/linux/test 目录下有 a.txt b.txt

  # 将 a.txt移动到 my 文件夹下的命令如下：
  mv a.txt ../my

  # 将 b.txt 重命名为 c.txt 的方法如下：
  mv b.txt c.txt
  # /hurrican/linux
  ```

  ​




<p align="right"><a href="#command">返回</a></p>

+ `locate` + `updatedb` —— **查找文件的路径**




<p align="right"><a href="#command">返回</a></p>

+ `cp` —— **复制文件**

  ```shell
    # 假设当前目录为 /hurrican/linux/test
    # 使用 pwd 检验当前路径是否为  /hurrican/linux/test
    # /hurrican/linux/test 目录下有 c.txt
    
    # 复制 c.txt 到当前文件夹，复制后的名字为 d.txt 的命令如下：
    cp c.txt d.txt
    
    # 将 c.txt复制到 /hurrican/linux 的命令如下：
    cp c.txt ../
    
    # 或者可以使用全路径
    cp c.txt  /hurrican/linux
  ```

  ​




<p align="right"><a href="#command">返回</a></p>

+ `ls`

  + `ls -l`——有些系统可以简写为`ll`

    ![](https://github.com/HurricanGod/Home/blob/master/linux/base/img/ll_detail.png)






<p align="right"><a href="#command">返回</a>|<a href="#top">返回目录</a></p>

-----

## <a name="tip">**事半功倍的小提示**</a>



+ `↑` 可以重新执行已执行过的命令，可以一直按`↑` 查找执行过的历史命令
+ `↓` —— 试试就知道有什么作用了
+ `Tab` —— **智能补全路径、命令**，想少敲键盘**一定要常用Tab键**






<p align="right"><a href="#command">返回</a>|<a href="#top">返回目录</a></p>


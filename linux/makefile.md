### make工作原理
1. make被调用后会在当前目录下找名字叫"Makefile"或"makefile"的文件.
2. 如果找到,它会找文件中的第一个目标文件(target),在下面的例子中,它会找到"myapp"这个文件,并把这个文件作为最终的目标文件.
3. 如果myapp文件不存在,或是myapp所依赖的后面的 .o 文件的文件修改时间要比myapp这个文件新,那么,它就会执行后面所定义的命令来生成myapp这个文件.
4. 如果myapp所依赖的.o文件也不存在,那么make会在当前文件中找目标为.o文件的依赖性,如果找到则再根据那一个规则生成.o文件.(这有点像一个堆栈的过程)
5. .C文件和.H文件是存在的并且跟makefile文件在同一个目录,于是make会生成 .o 文件,然后再用 .o 文件生成make的最终目标myapp.

```makefile
myapp: main.o 2.o 3.o
	gcc -o myapp main.o 2.o 3.o

main.o: main.c a.h
	gcc -c main.c

2.o: 2.c a.h b.h
	gcc -c 2.c

3.o: 3.c b.h c.h
	gcc -c 3.c

```
 
**make**的变量又称宏定义，变量名中不能含有“#”、“;”、“ ”、“@”具有特殊意义的字符 
引用 `make变量`的方法是用"()"将变量名括起来，并在前面加“**$**”符号。
例 ：
```makefile
all: myapp
CC = gcc
INSTDIR = /usr/local/bin
INCLUDE = .
myapp: main.o 2.o 3.o
	$(CC) -o myapp main.o 2.o 3.o
```
<hr/>


|变量名 |含义 |
|:-------------:|:------:|
|$@|表示规则中的目标文件集合|
|$%|仅当目标文件是一个静态库成员时，表示规则中的目标成员名|
|$?|所有比目标文件还新的那些依赖文件的集合，以空格分开|


##### 常用make命令选项


| 选项 | 说明 |
|:-------------:|:------:|
| -C dir | 在读取makefile文件或做其他任何事情前`切换到dir目录`,若有多个-C选项，后面的路径以前面的路径作为相对路径，并以最后的目录作为指定目录 |
|-f file| 指定file文件作为makefile文件 |
| -n |打印要执行的命令，但不执行 |
| -s |不输出被执行的命令|
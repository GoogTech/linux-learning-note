# Unix中常用的命令

⚠️注意 : 下述命令的实验环境为`MacOS(M2)`，版本为`13.5 (22G74)`，即`Unix`操作系统，而 Shell 使用的`zsh`，即默认 Shell .

对了，可能有些未实验的命令参数是错误的，因为参考的资料大多为 Linux 操作系统，而 Unix 与 Linux 中命令的使用还是有差别的 .

```shell
hwte@sw ~ % echo $SHELL
/bin/zsh
```



### ❤️man

其全称为 "manual"，是一个内置的帮助文档查看器，例如当你想要了解一个特定命令的使用方式时，你可以使用`man <command>`来查看该命令的帮助文档 . 

例如查看 `vim` 命令的帮助文档（因输出信息过多，故可结合 `less` 命令便捷浏览输出内容哟～）:  

```shell
$ man vim | less
```

注 : `|` 符号被称为管道（`pipe`），它用于连接两个或多个命令，使得前一个命令的输出成为后一个命令的输入，这种机制允许用户构建复杂的命令序列，以处理数据流 .



## 命令简单介绍

1. 操作文件或目录

   1. `cd` : 用于切换到指定目录
   2. `mkdir` : 用于创建指定名称的目录
   3. `rm` : 用于删除指定文件，当然也可以用于删除指定目录
   4. `rmdir` : 用于删除指定目录
   5. `mv` :  用于移动指定文件或目录
   6. `cp` : 用于复制指定文件或目录
   7. `touch` : 用于更改文件的访问时间和修改时间，多用于创建指定文件
   8. `cat` : 用于连接和输出文件内容
   9. `nl` : 用于在输出的文件内容前自动地加上行号，**常常结合其它命令一起使用**
   10. `more` : 同`less`命名，即用于查看文件里的内容，但没有 less 命令强大
   11. `less` : 同`more`命令，即用于查看文件里的内容，但相比`more`命令，提供了更多便捷的功能，**常常结合其它命令一起使用**
   12. `vim`  : 一款广受程序员们喜爱的文本编辑器，真的巨好用啊阿啊～
   13. `head` : 用于显示文件的前几行内容，默认是前 10 行，**常常结合其它命令一起使用**
   14. `tail` : 与`head`命令相反，用于显示文件的最后几行内容，默认是最后 10 行，**常常结合其它命令一起使用**
   15. `echo` : 它是`shell`的内置命令，通常用于输出信息，如输出环境变量的值，当然也可用于将信息输入到文件
   16. `ln` : 用于创建链接，这是一种特殊的文件，它指向另一个文件或目录
   17. `diff` : 用于比较两个文件或两个目录的内容差异

   

2. 文件查找
   1. `which` : 用于在`PATH`变量指定的路径中，搜索某个`系统命令`的位置
   1. `whereis` : 用于查找指定程序的二进制文件、手册页（man page）的位置
   1. `locate` : 用于快速地的搜寻指定的文件 .
   1. `find` : 用于沿着文件层次结构向下遍历，匹配符合条件的文件
   
   
   
3. 文件解压缩

   1. `tar` : 用于处理档案文件，以及解压缩档案文件，通常与`gzip`或`bzip2`等解压缩工具结合使用
   2. `gzip` : 使用广泛的解压缩程序，文件经它压缩后，其名称后面会多出`.gz`的扩展名
   3. `zip` : 使用广泛的解压缩程序，用来创建和操作`ZIP`格式的压缩文件
   4. `zipinfo` : 用于查看`ZIP`格式文件的详细信息
   5. `unzip` : 用于列出、测试和提取`ZIP`归档中的压缩文件

   

4. 文件权限设置

   1. `chmod` : 用于改变文件的访问权限

   2. `chgrp` : 用于改变文件的`组`

   3. `chown` : 用于更改文件的`所有者`和`组`

      

5. 磁盘存储

   1. `df` : 显示剩余的磁盘空间
   2. `du` : 显示磁盘使用情况的统计信息

   

6. 系统监控和优化

   1. `top` : 显示按序排列的进程信息
   2. `free` :  查看系统的内存使用情况，包括物理内存和交换分区的已使用空间和空闲空间
   3. `vmstat` : 查看虚拟内存统计信息
   4. `lsof` : 查看当前正在被进程打开的文件
   6. `ps` : 查看当前进程的详细信息

   

7. 网络命令

   1. `ipconfig` : 用来查看网络接口信息，以及为网络接口分配地址 & 配置网络接口参数

   2. `route` : 查看及手动管理网络路由表 .

   3. `ping` : 发送`ICMP ECHO_REQUEST`数据包到指定网络主机

   4. `traceroute` : 打印数据包到达指定网络主机的路径信息

   5. `netstat` : 查看网络状态，例如显示与`TCP`、`UDP`和`ICMP`等协议相关的连接信息

   6. `telnet` : 允许你通过`Telnet`协议连接到远程计算机或设备

   7. `ssh` : 用于远程登录和在远程机器上执行命令的程序

   8. `scp` : 用于在网络上的主机之间复制文件

      注 : 它使用`ssh`协议进行数据传输，并且使用相同的身份验证 & 提供与登录会话相同的安全性

   9. `curl` : 用于下载文件、发送`HTTP`请求、文件上传等，其支持多种协议

   

8. 定时任务

   1. `at` : 在一个指定的时间执行一个指定的任务，**且只能执行一次** 

   2. `crontab` : 用于管理`cron`作业，即定期执行的作业

      注 : `cron`是实际执行任务的`进程`，用户通过编辑自己的`crontab`来设置任务，这些任务会被`cron`守护进程周期性检查和执行

      

9. 其它命令

   1. `pwd` : 查看当前工作目录的路径
   
   2. `grep` : 搜索指定的文件内容，匹配指定字符串所在行，**常常结合其它命令一起使用，用于匹配指定字符串**
   
      注 : **也可用于匹配文件内容中包含指定字符串的行**
   
   3. `wc` : 计算单词、行数、字节数，**常常结合其它命令一起使用**
   
   4. `watch` : 允许你周期性地运行一个命令，并将结果输出在屏幕上
   
   5. `make` : 用于自动化编译、链接和安装等步骤，其是基于一个名为`Makefile`的文件来工作的
   
   6. `sort` : 排序或合并文本，及二进制文件中的记录（行），**常常结合其它命令一起使用**
   
   7. `export` : 设置或导出环境变量，环境变量是可以在`shell`会话期间访问的值，它可以影响`shell`和在其上运行的程序的行为
   
   8. `history` : 列出用户之前在终端中输入过的命令
   
   9. `chsh` : 切换到其它可用的 `Shell`



goodNight : 22 : 28


## 操作文件或目录

### ls

用于列出当前目录下文件和目录 .

* `-a` 或 `--all`：列出所有文件和目录，包括隐藏文件
* `-l` 或 `--list`：以长列表格式显示文件和目录信息，包括文件权限、所有者、大小等信息
* `-h` 或 `--human-readable`：以人类可读的方式显示文件大小，比如1K, 234M这样的格式
* `-t` 或 `--sort=time`：按文件修改时间排序
* `-r` 或 `--reverse`：反向排序（可与`-t`结合使用，按修改时间反向排序）
* `-d` 或 `--directory`：仅列出目录本身，而不是列出目录的文件数据
* `-I` 或 `--ignore=PATTERN`：忽略符合指定模式的文件
* `-S` 或 `--sort=size`：按文件大小排序
* `-X` 或 `--sort=extension`：按文件扩展名排序
* `--color` 或 `--no-color`：控制是否使用彩色输出
* `-R` : 连同子目录的内容一起列出(递归列出)，即该目录下的所有文件都会显示出来

1. 查看当前路径下的所有文件和目录的详细信息 : 

   ```shell
   hwte@sw note % ls -la
   total 16
   drwxr-xr-x  6 hwte  staff   192  6 26 11:07 .
   drwxr-xr-x  8 hwte  staff   256  6 26 11:06 ..
   -rw-r--r--@ 1 hwte  staff  6148  6 26 22:08 .DS_Store
   drwxr-xr-x  7 hwte  staff   224  6 26 11:12 others
   drwxr-xr-x  3 hwte  staff    96  6 26 15:05 python
   drwxr-xr-x  3 hwte  staff    96  6 26 11:07 report
   ```

2. 以长列表格式显示当前路径下的文件和目录信息 & 按照修改时间正向排序 : 

   ```shell
   hwte@sw note % ls -ltr 
   total 0
   drwxr-xr-x  3 hwte  staff   96  6 26 11:07 report
   drwxr-xr-x  7 hwte  staff  224  6 26 11:12 others
   drwxr-xr-x  3 hwte  staff   96  6 26 15:05 python
   ```

3. 以长列表格式显示当前路径下的文件和目录信息 & 按文件大小逆向排序 : 

   ```shell
   hwte@sw note % ls -lS 
   total 0
   drwxr-xr-x  7 hwte  staff  224  6 26 11:12 others
   drwxr-xr-x  3 hwte  staff   96  6 26 15:05 python
   drwxr-xr-x  3 hwte  staff   96  6 26 11:07 report
   ```

4. 以长列表格式显示当前路径下的文件和目录信息 & 连同子目录的内容一起列出 & 按文件大小正向排序 : 

   ```shell
   hwte@sw note % ls -lSRr 
   total 0
   drwxr-xr-x  3 hwte  staff   96  6 26 11:07 report
   drwxr-xr-x  3 hwte  staff   96  6 26 15:05 python
   drwxr-xr-x  7 hwte  staff  224  6 26 11:12 others
   
   ./report:
   total 8
   -rw-r--r--@ 1 hwte  staff  3519  5 24 16:21 firstMonthReport.md
   
   ./python:
   total 304
   -rw-rw-r--@ 1 hwte  staff  154106  6 26 15:05 python-learning-note-newest.md
   
   ./others:
   total 80
   -rw-r--r--@ 1 hwte  staff   1106  4 12 16:53 useful-command-in-linux.md
   -rw-r--r--@ 1 hwte  staff   2084  5 26 13:10 Diff_Request_Session_In_Python.md
   -rw-r--r--@ 1 hwte  staff   5924  5 29 15:21 matchbox-to-schooner-learning-note.md
   -rw-r--r--@ 1 hwte  staff   6142  6 26 11:12 userful-git-command-in-real-dev.md
   -rw-r--r--@ 1 hwte  staff  13835  6 10 13:22 sqlite3-learning-note.md
   ```



### cd

用于切换当前目录至dirName .

* `cd /` 命令用于将当前工作目录切换到系统的根目录
* `cd ~`命令是用来切换到用户的主目录
* `cd ..`命令是用来切换到当前工作目录的上级目录，例如 `cd ../../..` 返回上上上层目录



### mkdir

用来创建指定的名称的目录 .

* `-p` 或 `--parents`：这个参数允许你一次创建多个目录层次
* `-m` 或 `--mode`：这个参数可以用来设置目录的权限模式

1. 创建多个目录 : 

   ```shell
   mkdir directory1 directory2 directory3
   ```

2. 使用**绝对路径**创建目录 : 

   ```shell
   mkdir /path/to/new_directory
   ```

3. 使用**相对路径**创建目录 : 

   ```shell
   mkdir ./new_directory
   ```

4. 创建**多级目录**结构 : 

   ```shell
   mkdir -p parent/child/grandchild
   ```

5. 创建目录的同时指定权限 : 

   ```shell
   mkdir -m 755 new_directory
   ```

   ❗️注 : 权限模式. . .



### rm

用于删除文件和目录 .

注 : `rm -rf` 可以强制递归地删除任何文件或目录 .

* `-f` 或 `--force`：强制删除文件，即使它是只读的或者没有权限访问
* `-i` 或 `--interactive`：交互式询问是否删除每个指定的文件
* `-r` 或 `--recursive`：递归地删除目录及其内容，这通常用于删除整个目录结构
* `-v` 或 `--verbose`：在删除每个文件或目录时，显示详细信息
* `-d` 或 `--dir`：仅删除空目录
* `-p` 或 `--parents`：在删除目录时，如果需要，也删除它的父目录

1. 删除指定目录及其中的内容（子目录与文件）: 

   ```shell
   hwte@sw folder_1 % ls -lR
   total 0
   -rw-r--r--  1 hwte  staff    0  7  5 09:05 file_1.txt
   drwxr-xr-x  4 hwte  staff  128  7  5 09:05 folder_2
   
   ./folder_2:
   total 0
   -rw-r--r--  1 hwte  staff   0  7  5 09:05 file_2.txt
   drwxr-xr-x  3 hwte  staff  96  7  5 09:05 folder_3
   
   ./folder_2/folder_3:
   total 0
   -rw-r--r--  1 hwte  staff  0  7  5 09:05 file_3.txt
   
   hwte@sw ~ % rm -rfv folder_1                   
   folder_1/file_1.txt
   folder_1/folder_2/file_2.txt
   folder_1/folder_2/folder_3/file_3.txt
   folder_1/folder_2/folder_3
   folder_1/folder_2
   folder_1
   ```

2. 删除当前目录中的所有所有子目录及文件 : 

   ```shell
   hwte@sw other_folder % rm -rfv *
   ```



### rmdir

用于删除一个空的目录，与`rm`命令不同，**`rmdir`不会删除非空目录或者文件 .**

* `-p` 或 `--parents`：删除目录名所指向的目录以及其所有父目录，这通常用于递归地删除目录树
* `-v` 或 `--verbose`：这个选项会让`rmdir`命令在删除每个目录之前打印出目录名

```shell
hwte@sw ~ % rmdir -pv folder_1/folder_2/folder_3 
folder_1/folder_2/folder_3
folder_1/folder_2
folder_1
```



### mv

用于移动指定文件或目录 .

* `-f` 或 `--force`：强制移动文件，如果目标文件已经存在，`mv`**会覆盖它而不提示**
* `-i` 或 `--interactive`：当目标文件已经存在时，**提示用户是否覆盖**
* `-n` 或 `--no-clobber`：类似于`-i`，但当目标文件已经存在时，不提示用户，而是不执行移动操作（即**不覆盖现有文件**）
* `-u` 或 `--update`：只当源文件比目标文件**新**时才移动
* `-t` 或 `--target-directory=DIRECTORY`：移动多个源文件到一个目录，此时目标目录在前，源文件在后
* `-b` 或 `--backup` : 先对即将被覆盖的文件进行**备份**，然后再执行移动操作
* `-r` 或 `--recursive` : 把源目录下的所有文件和子目录移动到目标目录中
* `-v` 或 `--verbose`：显示移动的文件列表

1. 重命名文件或文件夹 : 

   ```shell
   hwte@sw ~ % mv old_file_name.txt new_file_name.txt
   hwte@sw ~ % mv old_folder_name new_folder_name
   ```

2. 移动多个文件到同一目录 : 

   ```shell
   hwte@sw ~ % mv file_1.txt file_2.txt folder_name
   ```

3. 移动目录到另一个目录 :

   ```shell
   hwte@sw ~ % mv folder_3 folder_1/folder_2
   ```

4. 将当前目录中的所有文件移动到另一个目录中，或者更精确地，移动所有以`.txt`结尾的文件 : 

   ```shell
   hwte@sw folder % mv * ~/folder_2/folder_3/
   hwte@sw folder % mv *.md ~/folder_2/folder_3/
   ```



### cp

用于复制指定文件或目录 .

* `-r` 或 `--recursive`：递归地复制目录及其内容
* `-a` 或 `--archive` 或 `--all`：以归档模式复制，通常用于备份，它保留了文件的访问时间和修改时间
* `-i` 或 `--interactive`：在**覆盖**现有文件之前询问用户
* `-n` 或 `--no-clobber`：**如果目标文件已经存在，不覆盖它**
* `-I` 或 `--ignore-errors`：忽略在复制过程中遇到的错误，继续复制其他文件
* `-u` 或 `--update`：只复制那些比目标文件更新的源文件
* `-v` 或 `--verbose`：在执行时显示每个文件被复制的情况
* `-f` 或 `--force`：行复制文件或目录，**不论目的文件或目录是否已经存在**
* `-p` 或 `--preserve`：保留源文件的修改时间和访问时间

1. 拷贝多个文件到一个目录 : 

   ```shell
   hwte@sw folder % cp doc.pdf doc.txt ~/other_folder
   ```

2. 拷贝文件并重命名 : 

   ```shell
   hwte@sw folder % cp doc.txt ~/other_folder/doc_newest.txt
   ```

3. 将当前目录中的所有文件拷贝到另一个目录中，或者更精确地，拷贝所有以`.txt`结尾的文件 :

   ```shell 
   hwte@sw folder % cp * ~/other_folder
   hwte@sw folder % cp *.txt ~/other_folder 
   ```



### ⭐️touch

用于更改文件的访问时间和修改时间，多用于创建指定文件 .

* . . .

1. 创建一个新文件 : 

   ```shell
   touch new_file_name.txt
   ```

2. 修改文件的访问时间和修改时间 : 

   ```shell
   
   ```

3. 修改文件的创建时间 : 

   ```shell
   
   ```



### cat

用于连接和输出文件内容 .

* `-n` 或 `--number`：在每行前面加上行号
* `-s` 或 `--squeeze-blank`：忽略连续的空白行

1. 查看文件内容 : 

   ```shell
   hwte@sw folder % cat file.txt 
   hello file.txt
   ```

2. 查看文件内容，并显示行号 : 

   ```shell
   hwte@sw folder % cat -n file.txt
        1	update the file.txt content
        2	add new info into file.txt
        3
   ```

3. 连接多个文件并输出 : 

   ```shell
   hwte@sw folder % cat file.txt file_2.txt 
   hello file.txt
   hello file_2.txt
   ```

4. 直接在终端中打开文件 : 

   这个命令会打开一个交互模式，允许你直接在终端中输入内容到`file.txt`文件中，按下 Ctrl+D（EOF，End Of File）键来结束输入并保存文件 .

   ```shell
   hwte@sw folder % cat file.txt
   hwte@sw folder % cat > file.txt 
   update the file.txt content
   hwte@sw folder % cat file.txt  
   update the file.txt content
   ```

5. 追加内容到文件末尾 : 

   这个命令会打开一个交互模式，允许你向`file.txt`文件追加内容，按下 Ctrl+D 键来结束输入并保存文件 .

   ```shell
   hwte@sw folder % cat file.txt 
   update the file.txt content
   hwte@sw folder % cat >> file.txt 
   add new info into file.txt        
   hwte@sw folder % cat file.txt   
   update the file.txt content
   add new info into file.txt
   ```

6. 翻页查看大型文件 :

   这个命令会将`file.txt`的内容输出到`less`命令，`less`是一个分页查看器，可以帮助你更方便地查看大型文件的内容 .

   ```shell
   cat file.txt | less
   ```

7. 查看文件的前几行 : 

   这个命令会显示`file.txt`的前10行，加上行号，`head`命令用于显示文件的前几行 .

   ```shell
   cat -n file.txt | head -n 10
   ```

8. 查看文件的最后几行 : 

   这个命令会显示`file.txt`的最后10行，`tail`命令用于显示文件的最后几行 .

   ```shell
   cat file.txt | tail -n 10
   ```



### nl

输出的文件内容自动的加上行号！其默认的结果与 `cat -n` 有点不太一样， nl 可以将行号做比较多的显示设计，包括位数与是否自动补齐 0 等功能 .

`-b` ：指定行号指定的方式，主要有如下两种 : 

* `-b a` ：表示不论是否为空行，也同样列出行号（**类似 cat -n**）
* `-b t` ：如果有空行，空的那一行不要列出行号（默认值）

`-n` ：列出行号表示的方法，主要有如下三种 : 

* `-n ln` ：行号在萤幕的最左方显示
* `-n rn` ：行号在自己栏位的最右方显示，且不加 0
* `-n rz` ：行号在自己栏位的最右方显示，且加 0

```shell
hwte@sw folder % nl file.txt 
     1	update the file.txt content
     2	add new info into file.txt
      	
hwte@sw folder % nl -b a file.txt 
     1	update the file.txt content
     2	add new info into file.txt
     3	
hwte@sw folder % nl -b t file.txt
     1	update the file.txt content
     2	add new info into file.txt
      	
hwte@sw folder % nl -n ln file.txt 
1     	update the file.txt content
2     	add new info into file.txt
      	
hwte@sw folder % nl -n rn file.txt
     1	update the file.txt content
     2	add new info into file.txt
      	
hwte@sw folder % nl -n rz file.txt
000001	update the file.txt content
000002	add new info into file.txt
```



### more

more 命令和 cat 的功能一样都是查看文件里的内容，但有所不同的是 more 可以按页来查看文件的内容，还支持直接跳转到指定行等功能 .

#### 常用参数

* `-n` : 定义在每页所显示的行数
* `+n` : 从笫 n 行开始显示
* `+/pattern` : 在显示前匹配该字符串，若匹配到则从该字符串所在行 / 段落开始显示
* `-i` : 忽略大小写，也就是说，在搜索或者翻页时忽略大小写差异
* `-s` : 将连续的多个空行显示为一行

#### 操作指令

* `Enter` : 向下滚动 n 行，需要定义，默认为 1 行
* `空格键` : 向下滚动一页
* `Ctrl+F` : 向下滚动一页
* `Ctrl+B` : 向上滚动一页
* `=` : 输出当前页的行号范围及当前阅读进度的百分比
* `v` : 调用 vim 编辑器
* `!` : 可编写 Shell 命令并执行
* `q` : 退出 more 命令

1. 定义在每页显示 5 行

   ```shell
   more -n 5 file.txt
   ```

2. 从笫 1000 行开始显示

   ```shell
   more +1000 file.txt
   ```

3. 在显示前匹配字符串 pattern_str，若匹配到则从该字符串所在行/段落开始显示

   ```shell
   more +/pattern_str file.txt
   ```

4. 在搜索或者翻页时忽略大小写差异

   ```shell
   more -i +/PYDOC_STR file.txt
   ```

5. 将连续的多个空行显示为一行

   ```shell
   more -s file.txt
   ```



###  ⭐️less

less 命令的作用和 more 十分类似，都用来浏览文本文件中的内容，不同之处在于，为了方面用户浏览文本内容，less 命令还提供了以下几个功能 : 

使用光标键可以在文本文件中前后（左后）滚屏；用行号或百分比作为书签浏览文件；提供更加友好的检索、高亮显示等操作；兼容常用的字处理程序（如 Vim、Emacs）的键盘操作；阅读到文件结束时，less 命令不会退出；屏幕底部的信息提示更容易控制使用，而且提供了更多的信息 .

### 与`more`的区别

* less 可以按键盘上下方向键显示上下内容，而 more 不能通过上下方向键控制显示
* less 不必读整个文件，加载速度会比 more 更快
* less 退出后 shell 不会留下刚显示的内容，而 more 退出后会在 shell 上留下刚显示的内容
* 阅读到文件结束时，less 不会退出，而 more 会
* less 可用行号或百分比作为书签浏览文件，而 more 不行
* 相比 more，less 提供更加友好的检索、高亮显示等操作

#### 常用参数

注 : 这些参数也可以在使用 less 浏览文本内容的过程中使用，其用法相同 .

| `-N`              | 显示每行的行号                                       |
| ----------------- | ---------------------------------------------------- |
| `-S`              | 行过长时将超出部分舍弃                               |
| `-e`              | 当文件显示结束后，自动离开                           |
| `-Q`              | 不使用警告音                                         |
| `-i`              | 忽略搜索时的大小写                                   |
| `-m`              | 显示类似 more 命令的百分比                           |
| `-f`              | 强迫打开特殊文件，比如外围设备代号、目录和二进制文件 |
| `-s`              | 显示连续空行为一行                                   |
| `-b <缓冲区大小>` | 设置缓冲区的大小                                     |
| `-o <文件名>`     | 将 less 输出的内容保存到指定文件中                   |
| `-x <数字>`       | 将 Tab 键显示为规定的数字空格                        |

#### 操作命令

##### 移动

* `z` : 向后翻一页
* `空格键` : 向后翻一页
* `w` : 向前翻一页
* `d` : 向后翻半页
* `u` : 向前翻半页
* `回车键` : 向下滚动一行
* `[pagedown]` : 向下滚动一行
* `[pageup]` : 向上滚动一行

##### 搜索

* `/pattern` : 向下搜索匹配的 "字符串"

* `?pattern` : 向上搜索匹配的 "字符串"

* `&/pattern` : Display only matching lines

  `n` : 重复前一个搜索，即正向继续匹配（`/` 或 `?` 均可使用）

  `N` : 反向重复前一个搜索，即反向继续匹配（`/` 或 `?` 均可使用）

##### 跳转

* `<` : 跳转到文件的开头
* `>` : 跳转到文件的末尾

##### 其它

* `v` : 调用 vim 编辑器
* `h` : 显示帮助界面
* `q` : 退出 less 命令



### ❤️vim

一款广受程序员们喜爱的文本编辑器，真的巨好用啊阿啊～（**注 : vim 也可以打开文件夹哟～**）

非编辑模式（普通模式）下的常用操作 : 

常规操作 : 

* `yy` 复制当前行，`p` 粘贴
* `dd` 删除当前行
* `u` 撤销以前的操作
* `i` : 从普通模式切换到插入模式，在当前光标的位置前进行插入
* `o` : 从普通模式切换到插入模式，在当前行的下一行进行插入
* `gg` 移动到文件首，`G` 移动到文件尾
* `<Esc>` : 从编辑模式切换到普通模式
* `:help` 查看帮助文档
* `:q` 不保存退出
* `:w` : 保存但不退出
* `:wq` : 保存并退出

行号操作 : 

* `:set number` : 显示行号
* `:set relativenumber` : 显示相对行号，即光标所在行的行号为0，上和下一行为1，以此递增
* `:set ruler` : 显示位置指示器，即实时显示光标所在位置的行号及字符序号
* `:line_number` : 跳转到指定的行
* `:set cursorline` : 突出显示光标所在行，即为光标所在行加一条下划线

缩进操作 : 

* `:set tabstop=4` : 设置制表符长度，即 tab 键长度，`tabstop=4`对于编写代码刚刚好
* `:set smartindent` : 使用智能缩进，例如代码换行时会自动参考上一行的缩进来进行缩进

搜索操作 : 

* `/pattern` 搜索字符串，按`n`继续搜索下一个匹配的文本
* `:set ignorecase` : 搜索时忽略大小写
* `:set hlsearch` : 搜索时高亮显示匹配项
* `:set incsearch` : 增量搜索，即随着你输入更多的字符，搜索结果会实时更新. 搭配 `:set hlsearch` 食用更佳～

替换操作 : 

* `:s/old_str/new_str` : 替换当前行匹配到的单词
* `:global/old_str/s//new_str` : 替换所有匹配行匹配到的单词

编程操作 : 

* `:syntax on` : 编程语言语法高亮显示

编码操作 : 

* `:set encoding=utf-8` : 使用 UTF-8 编码

其它操作 : 

* `:set autoread` : 当文件发生变换时，自动读取新文件

注意事项 : 

1. 以上 Vim 配置项都可以直接复制到配置文件中，进而无需每次打开文件后手动配置 .

2. 在使用 vim 打开文件后，若想要知道 `:set 选项`中选项的状态，可使用`:set 选项?`命令，该命令将返回一个提示，告诉你该`选项`是启用态还是禁止态，举例 : 

   ```shell
   :set number? # return `number` or `nonumber`
   ```

   当然，如果想要将`:set 选项`中的选项改为禁止态，只需在`选项`此单词前加`no`即可，举例 : 

   ```shell
   :set nonumber
   ```

配置 vim 配置文件 : 

注 : 若 vim 配置文件不存在，则先创建一个就好啦～

- `/etc/vimrc` : 是系统级别的 Vim 配置文件，如果放在这里，只要配置一次，所有用户都可以使用
- `$HOME/.vimrc` : 是用户级别的 Vim 配置文件，只针对当前用户有效
- `~/.vim/vimrc` : 同样也属于当前用户的配置文件

这里展示一下我的 vim 配置文件（vim 真的超级好用啊阿啊爱了爱了）: 

```shell
hwte@sw demo % cat ~/.vimrc
""" 行号设置
set number						" 显示行号
set ruler							" 显示位置指示器
set cursorline				" 突出显示光标所在行

""" 缩进设置
set tabstop=4					" 设置tab键长度,这个长度对于编写代码刚刚好
set smartindent				" 使用智能缩进,例如代码换行时会自动参考上一行的缩进来进行缩进

""" 搜索设置
set ignorecase				" 搜索时忽略大小写
set hlsearch					" 搜索时高亮显示匹配项
set incsearch					" 增量搜索,即随着输入更多的字符,搜索结果会实时更新

""" 编程设置
syntax on							" 编程语言语法高亮显示

""" 编码设置
set encoding=utf-8		" 设置字符编码为UTF-8

""" 其它设置
set autoread					" 当文件发生变换时,自动读取新文件
```



### head

- `-c <字节数>` : 显示的字节数
- `-n <行数>` : 显示的行数

`head`命令用于显示文件的前几行内容，它的默认行为是显示前 10 行 .

```shell
head -n 24 file_name
```



### tail

- `-c <字节数>` : 显示的字节数
- `-n <行数>` : 显示的行数
- `-f` : 循环读取

`tail`命令与`head`命令相反，它用于显示文件的最后几行内容，它的默认行为是显示最后 10 行 .

```shell
tail -n 24 file_name
```

注 : 除了显示固定数量的行，`tail`命令还可以结合使用`-f`选项来跟踪日志文件或其他不断增长的文件，当文件被更新时，`tail -f`会自动更新显示，这样你就可以实时查看文件内容的变化 .



### echo

它是 shell 的内置命令，`echo`命令通常用于输出信息，如输出环境变量的值，当然也可用于将信息输入到文件 .

1. 打印环境变量的数值 : 

   ```shell
   # 查看当前用户名称
   hwte@sw ~ % echo $USER
   hwte
   # 查看当前系统语言
   hwte@sw~ % echo $LANG    
   zh_CN.UTF-8
   # 查看 PATH: 当用户在终端中输入一个命令时，shell 会在 PATH 环境变量指定的目录列表中查找对应的可执行文件
   hwte@sw ~ % echo $PATH
   /Library/Frameworks/Python.framework/Versions/3.7/bin:/Library/Frameworks/Python.framework/Versions/3.12/bin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/VMware Fusion.app/Contents/Public:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin
   ```

2. 将信息输入到文件 : 

   ```shell
   hwte@sw demo % ls -l
   total 0
   # 创建 file.txt 文件并将字符串 hello 2024 写入该文件
   # 注: `>` 符号表示覆盖写入
   hwte@sw demo % echo 'hello 2024' > file.txt
   hwte@sw demo % cat file.txt 
   hello 2024
   # 将字符串 hello python 追加写入文件 file.txt
   # 注: `>>` 符号表示追加写入
   hwte@sw demo % echo 'hello python\nhello hackorg.com' >> file.txt 
   hwte@sw demo % cat file.txt                   
   hello 2024
   hello python
   hello hackorg.com
   ```



### In

用于创建链接，这是一种特殊的文件，它指向另一个文件或目录. ln 命令中软链接与硬链接的区别如下 : 

* 软链接（`symbolic link`）
  * 应用场景 : 当你想要为一个文件创建一个**快捷方式**时
  * 当源文件被移动或删除时，提醒用户文件已经不存在
  * 它包含一个**指向另一个文件或目录的指针，即它不直接关联到文件的内容**
* 硬链接（`hard link`）
  * 应用场景 : 当你想要创建一个文件的多份副本，但不想浪费空间存储重复的内容
  * 应用场景 : 当你想要确保无论源文件被移动到哪里，都能通过硬链接访问到它
  * 当源文件被删除时，硬链接仍然存在
  * 它们**指向同一个文件内容的实例，即对一个硬链接的修改也会反映在源文件中**

1. 为指定文件创建一个硬链接（`hard link`）:

   ```shell
   # 查看源文件 script.py 的内容
   hwte@sw folder % cat script.py 
   print('hello world')
   # 为源文件 script.py 创建一个硬链接
   hwte@sw folder % ln script.py ~/Desktop/code-workbech   
   # 更新硬链接文件中的内容
   hwte@sw folder % echo "updated" > ~/Desktop/code-workbech/script.py 
   # 查看源文件 script.py 的内容
   hwte@sw folder % cat script.py
   updated
   # 移动并更新源文件 script.py
   hwte@sw folder % mv script.py inner_folder
   hwte@sw folder % echo 'updated again' > inner_folder/script.py
   # 查看硬链接文件中的内容（无论源文件被移动到哪里，都能通过硬链接访问到它）
   hwte@sw folder % cat ~/Desktop/code-workbech/script.py 
   update again
   # 删除源文件 script.py
   hwte@sw folder % rm inner_folder/script.py
   # 查看硬链接文件中的内容（当源文件被删除时，硬链接仍然存在）
   hwte@sw folder % cat ~/Desktop/code-workbech/script.py 
   update again
   ```

2. 为指定文件创建一个软链接（`symbolic link`）: 

   ```shell
   # 查看源文件 script.py 的内容
   hwte@sw demo % cat script.py 
   print('hello world')
   # 为源文件 script.py 创建一个软链接
   hwte@sw demo % ln -s ~/demo/script.py ~/Desktop/googtech-workbench 
   # 更新软链接文件中的内容
   hwte@sw demo % echo 'updated' > ~/Desktop/googtech-workbench/script.py 
   # 查看源文件 script.py 的内容
   hwte@sw demo % cat script.py 
   updated
   # 移动并更新源文件 script.py
   hwte@sw demo % mv script.py inner_folder 
   hwte@sw demo % echo 'updated again' > inner_folder/script.py
   # 查看硬链接文件中的内容（当源文件被移动或删除时，提醒用户文件已经不存在）
   hwte@sw demo % cat ~/Desktop/googtech-workbench/script.py
   cat: /Users/hwte/Desktop/googtech-workbench/script.py: No such file or directory
   ```



### diff

用于比较两个文件或两个目录的内容差异 .

* `-c` : 以一种`版本控制系统`的格式输出差异

* `-b --ignore-space-change` : 忽略空格的变化

* `-w --ignore-all-blanks` : 忽略所有空格的变化，其中包括行首、行尾、及字符之间的空格

* `-i --ignore-case` : 忽略字母大小写

* `-r --recursive` : 递归地比较公共子目录

*  `--color=[when]` : 

  Color the additions green, and removals red, or the value in the

  DIFFCOLORS environment variable. The possible values of when are

  "**never**", "**always**" and "**auto**". **auto** will use color if the output

  is a tty and the COLORTERM environment variable is set to a non-

  empty string.

* `-x pattern -- exclude pattern` : 

  Exclude files and subdirectories from comparison whose basenames

  match pattern. Patterns are matched using shell-style globbing

  via fnmatch(3). Multiple **-x** options may be specified.

示例 : 

1. demo_folder_1/folder : 

   ```shell
   ./demo_folder_1/folder:
   total 24
   -rw-r--r--  1 hwte  staff  55  7 14 08:41 README.md
   -rw-r--r--  1 hwte  staff  40  7 14 08:42 image.jpg
   -rw-r--r--  1 hwte  staff  49  7 14 07:56 script.py
   ```

   ```shell
   hwte@sw demo % cat demo_folder_1/folder/script.py 
   if(a == b):
   	print('a is equal with b')
   		# pass
   		
   hwte@sw demo % cat demo_folder_1/folder/README.md 
   # Intro
   This is README.md file in demo_folder_1/folder
   
   hwte@sw demo % cat demo_folder_1/folder/image.jpg 
   This is a image in demo_folder_1/folder
   ```

2. demo_folder_2/folder : 

   ```shell
   ./demo_folder_2/folder:
   total 24
   -rw-r--r--  1 hwte  staff  55  7 14 08:42 README.md
   -rw-r--r--  1 hwte  staff  40  7 14 08:42 image.jpg
   -rw-r--r--  1 hwte  staff  93  7 14 07:58 script.py
   ```

   ```shell
   hwte@sw demo % cat demo_folder_2/folder/script.py
   if(A==B):
   	print('A is equal with B')
   	# pass
   
   	# it's new line compare with first_script.py
   hwte@sw demo % cat demo_folder_2/folder/README.md
   # Intro
   This is README.md file in demo_folder_2/folder
   hwte@gsw demo % cat demo_folder_2/folder/image.jpg
   This is a image in demo_folder_2/folder
   ```

3. 比较目录 demo_folder_1/folder 与 demo_folder_2/folder : 

   ```shell
   hwte@sw demo % diff -r -c -i -w --color=always --exclude='*.jpg' demo_folder_1/folder demo_folder_2/folder
   diff -r -c -i -w --color=always --exclude=*.jpg demo_folder_1/folder/README.md demo_folder_2/folder/README.md
   *** demo_folder_1/folder/README.md	Sun Jul 14 08:41:48 2024
   --- demo_folder_2/folder/README.md	Sun Jul 14 08:42:07 2024
   ***************
   *** 1,2 ****
     # Intro
   ! This is README.md file in demo_folder_1/folder
   --- 1,2 ----
     # Intro
   ! This is README.md file in demo_folder_2/folder
   diff -r -c -i -w --color=always --exclude=*.jpg demo_folder_1/folder/script.py demo_folder_2/folder/script.py
   *** demo_folder_1/folder/script.py	Sun Jul 14 07:56:18 2024
   --- demo_folder_2/folder/script.py	Sun Jul 14 07:58:20 2024
   ***************
   *** 1,3 ****
   --- 1,5 ----
     if(A==B):
     	print('A is equal with B')
     	# pass
   + 
   + 	# it's new line compare with first_script.py
   ```



## 文件查找

### which

which 指令会在 PATH 变量指定的路径中，搜索某个**系统命令**的位置，并且返回第一个搜索结果 .

* `-a` : 显示所有符合条件的命令的路径

```shell
hwte@sw ~ % which python3
/Library/Frameworks/Python.framework/Versions/3.12/bin/python3
hwte@sw ~ % which -a python3
/Library/Frameworks/Python.framework/Versions/3.12/bin/python3
/usr/bin/python3
```



### whereis

用于查找指定程序的二进制文件、手册页（man page）的位置 .

- `-a` : 定位所有符合条件的可执行文件、源代码文件、帮助文件
- `-b` : 定位符合条件的可执行文件
- `-m` : 定位符合条件的帮助文件

```shell
hwte@sw ~ % whereis python3
python3: /usr/bin/python3 /Library/Frameworks/Python.framework/Versions/3.12/share/man/man1/python3.1
# 定位所有符合条件的可执行文件、源代码文件、帮助文件
hwte@sw ~ % whereis -a python3
python3: /usr/bin/python3 /Library/Frameworks/Python.framework/Versions/3.12/bin/python3 /Library/Frameworks/Python.framework/Versions/3.12/share/man/man1/python3.1
# 定位`所有`符合条件的可执行文件
hwte@sw ~ % whereis -ba python3
python3: /usr/bin/python3 /Library/Frameworks/Python.framework/Versions/3.12/bin/python3
# 定位符合条件的帮助文件
hwte@sw ~ % whereis -m python3
python3: /Library/Frameworks/Python.framework/Versions/3.12/share/man/man1/python3.1
```



### locate

用于快速地的搜寻指定的文件 .

: . . . 感觉不好用，还是学习使用 find 命令吧～



### ⭐️find

用于沿着文件层次结构向下遍历，匹配符合条件的文件 .

- `-name pattern` : 按照 pattern 匹配文件

- `-iname pattern` : 按照 pattern 匹配文件，忽略大小写

- `-type` : 查找某一类型的文件
  
  - `-type f`：查找普通文件，这是默认的行为，如果不使用`-type`选项，`find`命令只会列出普通文件
  - `-type d`：查找目录，这会列出所有的目录，包括那些不包含任何文件的目录
  - `-type l`：查找符号链接，这会列出所有指向其他文件或目录的符号链接
  - `-type b` : block special
  - `-type c` : character special
  - `-type p` : FIFO
  - `-type s` : socket
  
- `-exec` : 对找到的每个文件执行一个命令，注 : 需要加上`{}`来引用找到的文件

- `-delete`：直接删除找到的文件**（谨慎使用，无法恢复）**

- `-size n[ckMGTP]`

  True if the file's size, rounded up, in 512-byte blocks is n. If

  n is followed by a **c**, then the primary is true if the file's size

  is n bytes (characters). Similarly if n is followed by a scale

  indicator then the file's size is compared to n scaled as :

  **k** : kilobytes (1024 bytes)

  **M** : megabytes (1024 kilobytes)

  **G** : gigabytes (1024 megabytes)

  **T** : terabytes (1024 gigabytes)

  **P** : petabytes (1024 terabytes)

一. 操作文件 : 

```shell
# 查找`当前目录下`的所有文件
hwte@sw folder % find .              
.
./file.txt
./.DS_Store
./file_2.txt
./file.md
./file.doc
# 查找`当前目录下`文件名后缀为`.txt`的文件
hwte@sw folder % find . -name '*.txt'
./file.txt
./file_2.txt
# 查找`当前目录下`文件名后缀为`.txt`的文件，并显示其详细信息
hwte@sw folder % find . -name '*.txt' -exec ls -l {} \;
-rw-r--r--  1 hwte  staff  56  7  5 15:39 ./file.txt
-rw-r--r--  1 hwte  staff  0  7  6 15:25 ./file_2.txt
# 查找`当前目录下`文件名后缀为`.txt`的文件，并显示其行数
hwte@sw folder % find . -name '*.txt' | xargs wc -l
       3 ./file.txt
       0 ./file_2.txt
       3 total
# 查找`指定目录下`文件名后缀为`.md`的文件，并显示其详细信息
hwte@sw backup % find nothing/note -name '*.md' -exec ls -l {} \;
-rw-rw-r--@ 1 hwte  staff  151156  7  5 21:37 nothing/note/python/python-learning-note-newest.md
-rw-r--r--@ 1 hwte  staff  13843  7  5 22:32 nothing/note/others/sqlite3-learning-note(uploaded).md
-rw-r--r--@ 1 hwte  staff  6142  6 26 11:12 nothing/note/others/userful-git-command-in-real-dev.md
-rw-r--r--@ 1 hwte  staff  2084  7  5 22:29 nothing/note/others/Diff_Request_Session_In_Python.md
-rw-r--r--@ 1 hwte  staff  21346  7  6 16:17 nothing/note/others/useful-command-in-linux.md
-rw-r--r--@ 1 hwte  staff  3519  5 24 16:21 nothing/note/report/firstMonthReport.md
# 查找`指定目录下`文件名后缀为`.md`的文件，并显示其行数
hwte@sw backup % find nothing/note -name '*.md' | xargs wc -l
    4760 nothing/note/python/python-learning-note-newest.md
     474 nothing/note/others/sqlite3-learning-note(uploaded).md
     194 nothing/note/others/userful-git-command-in-real-dev.md
      47 nothing/note/others/Diff_Request_Session_In_Python.md
     750 nothing/note/others/useful-command-in-linux.md
      14 nothing/note/report/firstMonthReport.md
    6239 total
# 查找`指定目录下`文件名后缀为`.md` & 文件大小大于`10 KB`的文件，并显示其详细信息
hwte@sw backup % find nothing/note -name '*.md' -size +10k -exec ls -l {} \;
-rw-rw-r--@ 1 hwte  staff  151156  7  5 21:37 nothing/note/python/python-learning-note-newest.md
-rw-r--r--@ 1 hwte  staff  13843  7  5 22:32 nothing/note/others/sqlite3-learning-note(uploaded).md
-rw-r--r--@ 1 hwte  staff  22727  7  6 16:37 nothing/note/others/useful-command-in-linux.md
# 查找`指定目录下`文件名后缀为`.md` & 文件大小`2KB < file_size < 4KB`的文件，并显示其详细信息
hwte@sw backup % find nothing/note -name '*.md' -size +2k -size -4k -exec ls -l {} \;
-rw-r--r--@ 1 hwte  staff  2084  7  5 22:29 nothing/note/others/Diff_Request_Session_In_Python.md
-rw-r--r--@ 1 hwte  staff  3519  5 24 16:21 nothing/note/report/firstMonthReport.md
# 删除`指定目录下`文件名后缀为`.md` & 文件大小`2KB < file_size < 4KB`的文件，并验证是否删除成功
hwte@sw backup % find nothing/note -name '*.md' -size +2k -size -4k -delete          
hwte@sw backup % find nothing/note -name '*.md' -size +2k -size -4k -exec ls -l {} \;
```

二. 操作目录 : 

```shell
# 查找`当前目录下`的所有子目录
hwte@sw note % find . -type d                              
.
./pytest
./python
./others
./report
# 查找`当前目录下`目录名前缀为`py`的子目录
hwte@sw note % find . -type d -name 'py*'                  
./pytest
./python
# 查找`当前目录下`目录名前缀为`py`的子目录，并显示其详细信息
hwte@sw note % find . -type d -name 'py*' -exec ls -la {} \;  
total 0
drwxr-xr-x  3 hwte  staff   96  7  6 22:21 .
drwxr-xr-x  7 hwte  staff  224  7  6 22:21 ..
-rw-r--r--  1 hwte  staff    0  7  6 22:21 pytest.py
total 296
drwxr-xr-x  3 hwte  staff      96  7  5 21:37 .
drwxr-xr-x  7 hwte  staff     224  7  6 22:21 ..
-rw-rw-r--@ 1 hwte  staff  151156  7  5 21:37 python-learning-note-newest.md
```



## 文件解压缩

### ⭐️tar

`tar`命令是一个非常强大的工具，用于创建和处理档案文件，它可以将一个或多个文件或目录打包成一个档案文件，也可以解包档案文件，`tar`命令通常与`gzip`（`gz`）或`bzip2`（`bz2`）等解压缩工具结合使用 .

* `-c` : **表示创建一个新档案文件**
* `-v` : **表示显示创建过程中的详细信息**
* `-f` : **指定档案文件名**
* `-t` : 表示列出档案文件的内容
* `-r` : 表示向档案文件中添加文件
* `-x` **表示解压，即提取档案文件**
* `-z` : 表示使用`gzip`进行压缩（与`cvf`结合） / 解压缩（与`xvf`结合）
* `-j` : 表示使用`gzip`进行压缩（与`cvf`结合） / 解压缩（与`xvf`结合）
* `-C` : 后面跟的是你想要将文件解压到的目录

#### 详细使用文档

```shell
# 查看简约的使用文档
tar -help
```

```shell
# 查看详细的使用文档
tar --help 
```

#### 操作归档文件

1. 创建一个未压缩的档案文件 : 

   * `-c` : 表示创建一个新档案文件
   * `-v` : 表示显示创建过程中的详细信息
   * `-f` : 指定档案文件名

   ```shell
   hwte@sw % tar -cvf file.tar file.txt 
   a file.txt
   
   hwte@sw folder % ls -la
   total 32
   -rw-r--r--   1 hwte  staff  2048  7  7 15:42 file.tar
   -rw-r--r--   1 hwte  staff    12  7  7 15:42 file.txt
   ```

2. 列出档案文件的内容**（不解压）** : 

   * `-t` : 表示列出档案文件的内容

   ```shell
   hwte@sw folder % tar -tvf file.tar
   -rw-r--r--  0 hwte   staff      12  7  7 15:42 file.txt
   ```

3. 在档案文件中添加 / 替换指定文件或目录 :

   * `-r` : 表示向档案文件中添加文件

   ```shell
   hwte@sw folder % tar -rvf file.tar file_2.txt 
   a file_2.txt
   
   hwte@sw folder % tar -tvf file.tar           
   -rw-r--r--  0 hwte   staff      12  7  7 15:42 file.txt
   -rw-r--r--  0 hwte   staff       0  7  7 15:55 file_2.txt
   ```

4. 提取档案文件中的指定文件**（不全部解压）** :

   * `-x` 表示解压，即提取档案文件

   ```shell
   hwte@sw folder % ls -l
   total 8
   -rw-r--r--@ 1 hwte  staff  2560  7  7 15:56 file.tar
   
   hwte@sw folder % tar -xvf file.tar file_2.txt
   x file_2.txt
   
   hwte@sw folder % ls -l                       
   total 8
   -rw-r--r--@ 1 hwte  staff  2560  7  7 15:56 file.tar
   -rw-r--r--  1 hwte  staff     0  7  7 15:55 file_2.txt
   ```

#### 对文件解压缩

1. 创建一个使用`gz`压缩的归档文件 : 

   - `-z` : 表示使用`gzip`进行压缩 / 解压缩

   ```shell
   hwte@sw folder % ls -l
   total 0
   drwxr-xr-x  4 hwte  staff  128  7  7 17:10 inner_folder
   hwte@sw folder % ls -l inner_folder 
   total 8
   -rw-r--r--  1 hwte  staff     0  7  7 16:19 README.md
   -rw-r--r--@ 1 hwte  staff  2560  7  7 15:56 file.tar
   
   hwte@sw folder % tar -cvzf file.tar.gz inner_folder 
   a inner_folder
   a inner_folder/README.md
   a inner_folder/file.tar
   
   hwte@sw folder % ls -l                             
   total 8
   -rw-r--r--  1 hwte  staff  483  7  7 17:12 file.tar.gz
   drwxr-xr-x  4 hwte  staff  128  7  7 17:10 inner_folder
   ```
   
2. 列出压缩后的归档文件中的内容**（不解压）** :

   ```shell
   hwte@sw folder % tar -tvf file.tar.gz 
   drwxr-xr-x  0 hwte   staff       0  7  7 17:10 inner_folder/
   -rw-r--r--  0 hwte   staff       0  7  7 16:19 inner_folder/README.md
   -rw-r--r--  0 hwte   staff    2560  7  7 15:56 inner_folder/file.tar
   ```

3. 对压缩后的档案文件进行解压，**若未指定解压路径，则默认解压到当前目录** : 

   * `-z` : 表示使用`gzip`进行压缩 / 解压缩

   ```shell
   hwte@sw folder % ls -l
   total 8
   -rw-r--r--  1 hwte  staff  534  7  7 19:58 file.tar.gz
   
   hwte@sw folder % tar -xvzf file.tar.gz 
   x inner_folder/
   x inner_folder/README.md
   x inner_folder/file.tar
   
   hwte@sw folder % ls -l
   total 8
   -rw-r--r--  1 hwte  staff  534  7  7 19:58 file.tar.gz
   drwxr-xr-x  4 hwte  staff  128  7  7 19:53 inner_folder
   
   hwte@sw folder % ls -l inner_folder 
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 19:53 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   ```
   
4. 对压缩后的档案文件进行解压，**并指定解压路径** : 

   * `-C` : 后面跟的是你想要将文件解压到的目录

   ```shell
   hwte@sw folder % ls -l other_folder 
   total 0
   
   hwte@sw folder % tar -xvzf file.tar.gz -C other_folder 
   x inner_folder/
   x inner_folder/README.md
   x inner_folder/file.tar
   
   hwte@sw folder % ls -l other_folder/inner_folder 
   total 8
   -rw-r--r--  1 hwte  staff     0  7  7 16:19 README.md
   -rw-r--r--@ 1 hwte  staff  2560  7  7 15:56 file.tar
   ```



### ⭐️gzip

使用广泛的解压缩程序，文件经它压缩后，其名称后面会多出`.gz`的扩展名 .

* `-c` 或 `--stdout`：将压缩后的文件输出到标准输出，而不是创建一个新文件

* `-d` 或 `--decompress`：解压缩指定的压缩文件

* `-f` 或 `--force`：强制压缩或解压缩文件，即使目标文件已经存在

* `-r` 或 `--recursive`：递归地压缩或解压缩目录中的所有文件

* `-l` 或 `--list`：列出压缩文件的信息（包括原始文件大小、压缩后的大小、压缩比等）

* `-v` 或 `--verbose`：在压缩或解压缩时显示详细信息

* `-h` 或 `--help`：显示帮助文档

*  `-1 --fast` : fastest (worst) compression

   `-2 .. -8` : set compression level

   `-9 --best` : best (slowest) compression

1. 压缩当前目录下的指定文件 : 

   ```shell
   hwte@sw folder % ls -l
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 17:54 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   
   # 压缩当前目录下的指定文件
   # 注: 也可使用命令 gzip *，即压缩当前目录下的所有文件
   hwte@sw folder % gzip README.md file.tar 
   hwte@sw folder % ls -l                  
   total 16
   -rw-r--r--  1 hwte  staff   30  7  7 17:54 README.md.gz
   -rw-r--r--  1 hwte  staff  492  7  7 17:12 file.tar.gz
   ```

2. 压缩并重命名当前目录的指定文件 : 

   ```shell
   hwte@sw folder % ls -l
   total 16
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   
   hwte@sw folder % gzip -c file.tar > compressed_file.tar.gz
   
   hwte@sw folder % ls -l                                    
   total 24
   -rw-r--r--  1 hwte  staff   492  7  7 19:40 compressed_file.tar.gz
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   ```

3. 解压缩当前目录下被 gzip 压缩的文件 : 

   ```shell
   # 解压缩当前目录下被 gzip 压缩的文件
   hwte@sw folder % gzip -d README.md.gz file.tar.gz
   
   hwte@sw folder % ls -l
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 17:54 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   ```

4. 递归地压缩指定目录中的所有文件 & 在压缩时显示详细信息 : 

   ```shell
   # 详细查看当前目录中的子目录及其文件
   hwte@sw folder % ls -lR               
   total 0
   drwxr-xr-x  5 hwte  staff  160  7  7 20:29 inner_folder
   
   ./inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 19:53 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   drwxr-xr-x  4 hwte  staff   128  7  7 20:29 inner_inner_folder
   
   ./inner_folder/inner_inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 20:09 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 20:09 file.tar
   
   # 递归地压缩当前目录中的所有文件，并输出压缩信息
   hwte@sw folder % gzip -rv inner_folder 
   inner_folder/inner_inner_folder/README.md:	  -99.9% -- replaced with inner_folder/inner_inner_folder/README.md.gz
   inner_folder/inner_inner_folder/file.tar:	   93.1% -- replaced with inner_folder/inner_inner_folder/file.tar.gz
   inner_folder/README.md:	  -99.9% -- replaced with inner_folder/README.md.gz
   inner_folder/file.tar:	   93.1% -- replaced with inner_folder/file.tar.gz
   
   # 详细查看当前目录中的子目录及其文件
   hwte@sw folder % ls -lR               
   total 0
   drwxr-xr-x  5 hwte  staff  160  7  7 20:29 inner_folder
   
   ./inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff   30  7  7 19:53 README.md.gz
   -rw-r--r--  1 hwte  staff  492  7  7 17:12 file.tar.gz
   drwxr-xr-x  4 hwte  staff  128  7  7 20:29 inner_inner_folder
   
   ./inner_folder/inner_inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff   30  7  7 20:09 README.md.gz
   -rw-r--r--  1 hwte  staff  492  7  7 20:09 file.tar.gz
   ```

5. 递归地解压缩指定目录中的所有文件 : 

   ```shell
   # 详细查看当前目录中的子目录及其文件
   hwte@sw folder % ls -lR
   total 0
   drwxr-xr-x  5 hwte  staff  160  7  7 20:29 inner_folder
   
   ./inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff   30  7  7 19:53 README.md.gz
   -rw-r--r--  1 hwte  staff  492  7  7 17:12 file.tar.gz
   drwxr-xr-x  4 hwte  staff  128  7  7 20:29 inner_inner_folder
   
   ./inner_folder/inner_inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff   30  7  7 20:09 README.md.gz
   -rw-r--r--  1 hwte  staff  492  7  7 20:09 file.tar.gz
   
   # 递归地解压缩当前目录中的所有文件，并输出解压缩信息
   hwte@sw folder % gzip -rdv inner_folder 
   inner_folder/README.md.gz:	  -99.9% -- replaced with inner_folder/README.md
   inner_folder/inner_inner_folder/README.md.gz:	  -99.9% -- replaced with inner_folder/inner_inner_folder/README.md
   inner_folder/inner_inner_folder/file.tar.gz:	   93.1% -- replaced with inner_folder/inner_inner_folder/file.tar
   inner_folder/file.tar.gz:	   93.1% -- replaced with inner_folder/file.tar
   
   # 详细查看当前目录中的子目录及其文件
   hwte@sw folder % ls -lR                
   total 0
   drwxr-xr-x  5 hwte  staff  160  7  7 20:31 inner_folder
   
   ./inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 19:53 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   drwxr-xr-x  4 hwte  staff   128  7  7 20:31 inner_inner_folder
   
   ./inner_folder/inner_inner_folder:
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 20:09 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 20:09 file.tar
   ```

6. 列出压缩文件的信息（包括原始文件大小、压缩后的大小、压缩比等）: 

   ```shell
   hwte@sw folder % gzip -rl inner_folder
     compressed uncompressed  ratio uncompressed_name
             30            0 -99.9% inner_folder/README.md
             30            0 -99.9% inner_folder/inner_inner_folder/README.md
            492         7168  93.1% inner_folder/inner_inner_folder/file.tar
            492         7168  93.1% inner_folder/file.tar
   ```

7. 调整压缩等级 : 

   ```shell
   # `-1 --fast` : fastest (worst) compression
   hwte@sw inner_folder % gzip file.tar 
   hwte@sw inner_folder % gzip -l file.tar.gz 
     compressed uncompressed  ratio uncompressed_name
            492         7168  93.1% file.tar
   
   # `-2 .. -8` : set compression level
   hwte@sw inner_folder % gzip -1 file.tar 
   hwte@sw inner_folder % gzip -l file.tar.gz 
     compressed uncompressed  ratio uncompressed_name
            547         7168  92.3% file.tar
   
   # `-9 --best` : best (slowest) compression
   hwte@sw inner_folder % gzip -9 file.tar 
   hwte@sw inner_folder % gzip -l file.tar.gz 
     compressed uncompressed  ratio uncompressed_name
            472         7168  93.4% file.tar
   ```



### zip

`zip`命令是一个用来创建和操作 ZIP 格式压缩文件的实用工具 .

* `-r` : 向已有的 ZIP 文件中添加文件
* `-u` : 更新 ZIP 文件中已存在的文件
* `-d` : 删除 ZIP 文件中指定的文件
* `-e` : 对 ZIP 文件进行加密
* `-h` : 查看帮助文档

1. 创建一个新的 ZIP 文件 : 

   ```shell
   hwte@sw folder % zip zip_file.zip file.txt inner_folder 
     adding: file.txt (stored 0%)
     adding: inner_folder/ (stored 0%
   ```

2. 查看 ZIP 文件的内容 : 

   ```shell
   hwte@sw folder % zipinfo zip_file.zip 
   Archive:  zip_file.zip
   Zip file size: 335 bytes, number of entries: 2
   -rw-r--r--  3.0 unx       15 tx stor 24-Jul-09 11:00 file.txt
   drwxr-xr-x  3.0 unx        0 bx stor 24-Jul-09 10:59 inner_folder/
   2 files, 15 bytes uncompressed, 15 bytes compressed:  0.0%
   ```

3. 向已有的 ZIP 文件中添加文件 : 

   ```shell
   hwte@sw folder % zip -r zip_file.zip file_3.txt 
     adding: file_3.txt (stored 0%)
   ```

   ```shell
   hwte@sw folder % zipinfo zip_file.zip          
   Archive:  zip_file.zip
   Zip file size: 483 bytes, number of entries: 3
   -rw-r--r--  3.0 unx       15 tx stor 24-Jul-09 11:00 file.txt
   drwxr-xr-x  3.0 unx        0 bx stor 24-Jul-09 10:59 inner_folder/
   -rw-r--r--  3.0 unx        0 bx stor 24-Jul-09 11:06 file_3.txt
   3 files, 15 bytes uncompressed, 15 bytes compressed:  0.0%
   ```

4. 更新 ZIP 文件中已存在的文件 :

   ```shell
   hwte@sw folder % zip -u zip_file.zip file_3.txt 
   updating: file_3.txt (stored 0%)
   ```

   ```shell
   hwte@sw folder % zipinfo zip_file.zip                
   Archive:  zip_file.zip
   Zip file size: 500 bytes, number of entries: 3
   -rw-r--r--  3.0 unx       15 tx stor 24-Jul-09 11:00 file.txt
   drwxr-xr-x  3.0 unx        0 bx stor 24-Jul-09 10:59 inner_folder/
   -rw-r--r--  3.0 unx       17 tx stor 24-Jul-09 11:07 file_3.txt
   3 files, 32 bytes uncompressed, 32 bytes compressed:  0.0%
   ```

5. 删除 ZIP 文件中指定的文件 : 

   ```shell
   hwte@sw folder % zip -d zip_file.zip file_3.txt 
   deleting: file_3.txt
   ```

   ```shell
   hwte@sw folder % zipinfo zip_file.zip          
   Archive:  zip_file.zip
   Zip file size: 335 bytes, number of entries: 2
   -rw-r--r--  3.0 unx       15 tx stor 24-Jul-09 11:00 file.txt
   drwxr-xr-x  3.0 unx        0 bx stor 24-Jul-09 10:59 inner_folder/
   2 files, 15 bytes uncompressed, 15 bytes compressed:  0.0%
   ```

6. 创建一个新的 ZIP 文件 & 并对其进行加密 : 

   ```shell
   hwte@sw folder % zip -e zip_file.zip file.txt inner_folder/file_2.txt 
   Enter password: 
   Verify password: 
     adding: file.txt (stored 0%)
     adding: inner_folder/file_2.txt (stored 0%)
   ```

7. 解压加密过的 ZIP 文件，**若未指定解压路径，则默认解压到当前路径** : 

   ```shell
   hwte@sw folder % unzip -P goog.tech zip_file.zip
   Archive:  zip_file.zip
    extracting: file.txt                
    extracting: inner_folder/file_2.txt  
   ```

   解压加密过的 ZIP 文件，**并指定解压路径** : 

   ```shell
   hwte@sw folder % unzip -P goog.tech -d folder_2 zip_file.zip 
   Archive:  zip_file.zip
    extracting: folder_2/file.txt       
    extracting: folder_2/inner_folder/file_2.txt
   ```

   

### zipinfo

`zipinfo`命令是一个用于查看 ZIP 文件内容和属性的实用工具 .

* `-l` : 仅输出 ZIP 文件中所有的文件名，每一个文件名占一行
* `-v` : 详细地查看 ZIP 文件中各个文件的信息
* `-h` : 查看帮助文档

1. 查看 ZIP 文件的内容和属性 : 

   ```shell
   hwte@sw folder % zipinfo zip_file.zip   
   Archive:  zip_file.zip
   Zip file size: 428 bytes, number of entries: 2
   -rw-r--r--  3.0 unx       15 TX stor 24-Jul-09 13:49 file.txt
   -rw-r--r--  3.0 unx       17 TX stor 24-Jul-09 13:49 inner_folder/file_2.txt
   2 files, 32 bytes uncompressed, 32 bytes compressed:  0.0%
   ```

2. 仅输出 ZIP 文件中所有的文件名，每一个文件名占一行 : 

   ```shell
   hwte@sw folder % zipinfo -1 zip_file.zip 
   file.txt
   inner_folder/file_2.txt
   ```

3. 详细地查看 ZIP 文件中各个文件的信息，注 : 因信息过多，故可配合 less 使用哟 :  

   ```shell
   hwte@sw folder % zipinfo -v zip_file.zip | less
   ```

   

### unzip

`tar`命令可以配合`gzip`处理`.tar`和`.gz`格式的文件，但无法解压缩`.zip`格式的文件，要解压`.zip`文件，你可以使用`unzip`命令 .

* `-d` : 将文件解压缩到指定的目录
* `-l` : 列出 ZIP 文件中的内容，而不实际解压
* `-t` : 测试 ZIP 文件的结构和完整性，但不实际解压
* `-P` : 使用密码解压加密的 ZIP 文件
* `-h` : 查看使用文档

1. 将文件解压缩到指定的目录，若不指定这个参数，`unzip`会将文件解压缩到与 ZIP 文件同级的目录中 : 

   ```shell
   hwte@sw % unzip -d folder_2 zip_file.zip 
   Archive:  zip_file.zip
    extracting: folder_2/file.txt       
    extracting: folder_2/inner_folder/file_2.txt 
   ```

2. 列出 ZIP 文件中的内容，而不实际解压 : 

   ```shell
   hwte@sw folder % unzip -l zip_file.zip 
   Archive:  zip_file.zip
     Length      Date    Time    Name
   ---------  ---------- -----   ----
          15  07-09-2024 13:49   file.txt
          17  07-09-2024 13:49   inner_folder/file_2.txt
   ---------                     -------
          32                     2 files
   ```

3. 测试 ZIP 文件的结构和完整性，但不实际解压 : 

   ```shell
   hwte@sw folder % unzip -t zip_file.zip
   Archive:  zip_file.zip
       testing: file.txt                 OK
       testing: inner_folder/file_2.txt   OK
   No errors detected in compressed data of zip_file.zip.
   ```

4. 使用密码解压加密的 ZIP 文件 : 

   ```shell
   hwte@sw folder % unzip -P goog.tech zip_file.zip
   Archive:  zip_file.zip
    extracting: file.txt                
    extracting: inner_folder/file_2.txt  
   ```

   使用密码解压加密的 ZIP 文件 & 指定解压路径 : 

   ```shell
   hwte@sw folder % unzip -P goog.tech -d folder_2 zip_file.zip 
   Archive:  zip_file.zip
    extracting: folder_2/file.txt       
    extracting: folder_2/inner_folder/file_2.txt
   ```

   

## 文件权限设置

### ⭐️chmod

用于改变 linux 系统文件或目录的访问权限 .

```shell
chmod [option] [mode] [file/directory]
```

option 参数 : 

- `-R` : 处理指定目录以及其子目录下的所有文件

- `-v` : 运行时显示详细处理信息

#### mode为字母形式

在字母形式中，你使用符号来设定权限，这些符号是 : 

  `<权限范围> + <权限代号>` : 使权限范围内的目录或文件具有指定的权限

  `<权限范围> - <权限代号>` : 删除权限范围的目录或文件的指定权限

  `<权限范围> = <权限代号>` : 设置权限范围内的目录或文件具有指定的权限，同时移除其他所有权限

权限范围 : 

- `u` : 目录或者文件的当前的用户
- `g` : 目录或者文件的当前的群组
- `o` : 除了目录或者文件的当前用户(a)或群组(g)**之外的用户或者群组**（即其他用户）
- `a` : 所有的用户及群组

权限代号 : 

- `r` : 读权限，用数字 4 表示
- `w` : 写权限，用数字 2 表示
- `x` : 执行权限，用数字 1 表示
- `-` : 删除权限，用数字 0 表示

1. 给文件的所有者和组分别添加读、写权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod u+r,g+w file.txt 
   
   hwte@sw folder % ls -l file.txt        
   -r---w----  1 hwte  staff  0  7  9 21:32 file.txt
   ```

2. 从文件的所有者和组中分别移除读、写权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt                  
   -r---w----  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod u-r,g-w file.txt 
   
   hwte@sw folder % ls -l file.txt        
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   ```

3. 给所有用户（包括所有者、组和其他用户）赋予读权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod a+r file.txt 
   
   hwte@sw folder % ls -l file.txt    
   -r--r--r--  1 hwte  staff  0  7  9 21:32 file.txt
   ```

4. 给文件所有者添加读权限、组添加写权限、其他用户添加执行权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod u=r,g=w,o=x file.txt
   
   hwte@sw folder % ls -l file.txt            
   -r---w---x  1 hwte  staff  0  7  9 21:32 file.txt
   ```

#### mode为数字形式

在数字形式中，每个权限以三位数字表示，其中每位置代表一个用户组 : 文件所有者、组、其他用户，每个位置的数字范围是 0 到 7，分别对应没有权限到所有权限 .

- `0` - 没有权限
- `1` - 执行权限
- `2` - 写入权限
- `3` - 执行和写入权限
- `4` - 读取权限
- `5` - 读取和执行权限
- `6` - 读取和写入权限
- `7` - 所有权限（读、写、执行）

1. 给所有用户赋予所有权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod 777 file.txt
   
   hwte@sw folder % ls -l file.txt    
   -rwxrwxrwx  1 hwte  staff  0  7  9 21:32 file.txt
   ```

2. 给所有用户赋予执行和读权限，但只给文件所有者赋予写权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod 755 file.txt
   
   hwte@sw folder % ls -l file.txt    
   -rwxr-xr-x  1 hwte  staff  0  7  9 21:32 file.txt
   ```

3. 给所有用户赋予读权限，但只给文件所有者赋予写权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   
   hwte@sw folder % chmod 644 file.txt
   
   hwte@sw folder % ls -l file.txt    
   -rw-r--r--  1 hwte  staff  0  7  9 21:32 file.txt
   ```


#### 常用操作

1. 给目录的所有用户（所有者、组、其他用户）添加执行权限 : 

   ```shell
   hwte@sw folder % ls -l inner_folder 
   total 0
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   ----------  1 hwte  staff  0  7  9 22:15 file_2.txt
   
   hwte@sw folder % chmod -Rv ugo+x inner_folder
   inner_folder/file.txt
   inner_folder/file_2.txt
   
   hwte@sw folder % ls -l inner_folder          
   total 0
   ---x--x--x  1 hwte  staff  0  7  9 21:32 file.txt
   ---x--x--x  1 hwte  staff  0  7  9 22:15 file_2.txt
   ```

2. 给文件所有者设定所有权限，给组和其他用户设定读权限 : 

   ```shell
   hwte@sw folder % ls -l file.txt 
   ----------  1 hwte  staff  0  7  9 22:20 file.txt
   
   hwte@sw folder % chmod u=rwx,g=r,o=r file.txt
   
   hwte@sw folder % ls -l file.txt              
   -rwxr--r--  1 hwte  staff  0  7  9 22:20 file.txt
   ```

3. 递归地改变目录及其子目录的所有权限为755 : 

   ```shell
   hwte@sw folder % ls -l inner_folder                                             
   total 0
   ----------  1 hwte  staff  0  7  9 21:32 file.txt
   ----------  1 hwte  staff  0  7  9 22:15 file_2.txt
   
   hwte@sw folder % chmod -Rv 755 inner_folder                                   
   inner_folder/file.txt
   inner_folder/file_2.txt
   
   hwte@sw folder % ls -l inner_folder                                             
   total 0
   -rwxr-xr-x  1 hwte  staff  0  7  9 21:32 file.txt
   -rwxr-xr-x  1 hwte  staff  0  7  9 22:15 file_2.txt
   ```

4. 给`script.sh`脚本添加执行权限 : 

   ```shell
   hwte@sw folder % ls -l script.sh 
   ----------  1 hwte  staff  23  7  9 22:26 script.sh
   
   hwte@sw folder % chmod +x script.sh
   
   hwte@sw folder % ls -l script.sh   
   ---x--x--x  1 hwte  staff  23  7  9 22:26 script.sh
   ```




### chgrp

用于改变文件的`组` .



### chown

`chown` : 用于更改文件的`所有者`和`组` .



## 磁盘存储

### df

显示剩余的磁盘空间 .

* `-h` : 以方便阅读的方式显示

```shell
hwte@sw ~ % df -h    
Filesystem       Size   Used  Avail Capacity iused      ifree %iused  Mounted on
/dev/disk3s1s1  460Gi  8.5Gi  283Gi     3%  356048 2968353760    0%   /
devfs           209Ki  209Ki    0Bi   100%     723          0  100%   /dev
/dev/disk3s6    460Gi   20Ki  283Gi     1%       0 2968353760    0%   /System/Volumes/VM
/dev/disk3s2    460Gi  4.3Gi  283Gi     2%     174 2968353760    0%   /System/Volumes/Preboot
/dev/disk3s4    460Gi  3.6Mi  283Gi     1%      17 2968353760    0%   /System/Volumes/Update
/dev/disk2s2    500Mi  6.0Mi  482Mi     2%       1    4938200    0%   /System/Volumes/xarts
/dev/disk2s1    500Mi  6.0Mi  482Mi     2%      21    4938200    0%   /System/Volumes/iSCPreboot
/dev/disk2s3    500Mi  976Ki  482Mi     1%      51    4938200    0%   /System/Volumes/Hardware
/dev/disk3s5    460Gi  164Gi  283Gi    37% 1623372 2968353760    0%   /System/Volumes/Data
map auto_home     0Bi    0Bi    0Bi   100%       0          0  100%   /System/Volumes/Data/home
/dev/disk4s1    702Mi  690Mi   12Mi    99%    3679 4294963600    0%   /Volumes/PyCharm CE
/dev/disk5s1    200Mi  176Mi   24Mi    88%     606 4294966673    0%   /Volumes/网易有道翻译
/dev/disk6s1    663Mi  601Mi   62Mi    91%    4456 4294962823    0%   /Volumes/Xmind
```



### du

显示磁盘使用情况的统计信息 .

* `-a` : 计算指定目录中所有文件的大小，包括子目录
* `-s` : 只显示指定目录的**总大小**，不显示每个文件的大小
* `-h` : 以K、M、G为单位，提高信息的可读性

1. 查看当前目录中所有文件和子目录的**总大小** : 

   ```shell
   hwte@sw folder % du -sh inner_folder 
    12K	inner_folder
   ```

2. 查看当前目录中每个文件和子目录的大小，并以人类可读的方式输出 : 

   ```shell
   hwte@sw folder % du -ah inner_folder 
   4.0K	inner_folder/file.txt
   4.0K	inner_folder/file_2.txt
   4.0K	inner_folder/file_3.md
    12K	inner_folder
   ```

3. 查看当前目录中每个文件和子目录的大小 & 以人类可读的方式输出 & 按照大小进行排序 : 

   ```shell
   hwte@sw folder % du -ah inner_folder | sort   
    12K	inner_folder
   4.0K	inner_folder/file.txt
   4.0K	inner_folder/file_2.txt
   4.0K	inner_folder/file_3.md
   ```




## 系统监控和优化

### ⭐️top

显示当前系统正在执行的进程的相关信息 : 

* `-n` : 指定显示的进程数量
* `-pid` : 只显示指定的进程 ID 的进程信息
* `-s` : 指定更新间隔，单位为秒
* `-h` : 查看帮助文档

1. 显示当前系统正在执行的进程的相关信息 : 

   ```shell
   hwte@sw ~ % top
   ```

   ```shell
   Processes: 561 total, 2 running, 559 sleeping, 2534 threads                         20:45:22
   Load Avg: 1.29, 1.22, 1.18  CPU usage: 1.25% user, 2.16% sys, 96.58% idle
   ......
   
   PID    COMMAND      %CPU TIME     #TH   #WQ  #PORT MEM    PURG   CMPR PGRP  PPID  STATE
   78863  top          8.7  00:01.61 1/1   0    27    7793K  0B     0B   78863 51779 running
   45107  AtlasCore2   2.9  06:58.97 14    1    63    7754K  0B     0B   45107 1     sleeping
   858    USB Block    2.6  13:26.18 10    8    287   33M    144K   0B   858   1     sleeping
   ......
   ```

2. 显示当前系统正在执行的前 5 个进程的相关信息 : 

   ```shell
   hwte@sw ~ % top -n 5
   ```

   ```shell
   Processes: 560 total, 2 running, 558 sleeping, 2513 threads                         20:45:55
   Load Avg: 1.12, 1.19, 1.17  CPU usage: 5.8% user, 3.57% sys, 91.33% idle
   ......
   
   PID    COMMAND      %CPU TIME     #TH   #WQ  #PORT MEM    PURG   CMPR PGRP  PPID  STATE
   148    WindowServer 21.9 30:45.37 19    6    2631+ 436M-  36M    0B   148   1     sleeping
   26946  Terminal     18.7 01:08.62 9     3    366+  44M+   480K-  0B   26946 1     sleeping
   78945  top          7.4  00:01.04 1/1   0    27    5569K  0B     0B   78945 51779 running
   0      kernel_task  5.9  13:52.60 466/8 0    0     112K   0B     0B   0     0     running
   45107  AtlasCore2   3.2  06:59.96 14    1    63    7754K  0B     0B   45107 1     sleeping
   ```

3. 查看指定 pid 的进程信息 : 

   ```shell
   hwte@sw ~ % top -pid 455
   ```

   ```shell
   Processes: 532 total, 2 running, 530 sleeping, 2381 threads                   17:22:18
   Load Avg: 1.50, 1.34, 1.25  CPU usage: 4.12% user, 3.44% sys, 92.43% idle
   ......
   
   PID  COMMAND      %CPU TIME     #TH  #WQ  #POR MEM  PURG CMPR PGRP PPID STATE
   656  Google Chrom 0.3  01:22.97 18   1    284  114M 0B   0B   455  455  sleeping
   ```

4. 指定更新间隔，单位为秒 : 

   ```shell
   hwte@sw ~ % top -s 5
   ```

   ```shell
   Processes: 558 total, 2 running, 556 sleeping, 2517 threads                         20:56:37
   Load Avg: 1.32, 1.14, 1.14  CPU usage: 4.51% user, 11.61% sys, 83.87% idle
   ......
   
   PID    COMMAND      %CPU TIME     #TH   #WQ  #PORT MEM   PURG  CMPR PGRP  PPID  STATE
   80277  top          0.0  00:00.39 1/1   0    16    5025K 0B    0B   80277 51779 running
   80139  mdworker_sha 0.0  00:00.37 4     1    59    2961K 0B    0B   80139 1     sleeping
   78729  Google Chrom 0.0  00:00.06 11    1    91    16M   0B    0B   455   455   sleeping
   ......
   ```



### free

显示系统使用和空闲的内存情况，包括物理内存、交互区内存(swap)、内核缓冲区内存 .

**注 : MacOS Terminal (M2) 没有这条命令 .**



### vmstat

用来显示虚拟内存的信息 .

**注 : MacOS Terminal (M2) 没有这条命令 .**



### ⭐️lsof

`lsof`命令是 list open files 的缩写，它用于列出当前正在被进程打开的文件 .

* `-p` : 列出指定 pid 进程打开的文件
* `-h` : 查看帮助文档
* `-i` : 列出所有打开的TCP和UDP套接字
  * `-i TCP` : 列出所有打开的TCP套接字
  * `-i UDP` : 列出所有打开的UDP套接字
  * `-i:port_number` : 列出特定端口号被哪个进程使用的信息（**该命令可在 Linux 中使用**）

1. 列出指定 pid 进程打开的文件 : 

   ```shell
   hwte@sw ~ % lsof -p 45114 
   COMMAND   PID USER   FD     TYPE             DEVICE  SIZE/OFF                NODE NAME
   AtlasUI 45114 hwte  cwd      DIR               1,16       640                   2 /
   AtlasUI 45114 hwte  txt      REG               1,16    240336             8111353 /System/Volumes/Data/AppleInternal/Applications/AtlasUI.app/Contents/MacOS/AtlasUI
   
   ......
   ```

2. 列出所有打开的 TCP 套接字 :

   ```shell 
   hwte@sw ~ % lsof -i TCP
   COMMAND     PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
   ARDAgent    471 hwte    9u  IPv6 0x476647301cec9a7b      0t0  TCP *:net-assistant (LISTEN)
   Google      579 hwte   26u  IPv4 0x4766473e82029b03      0t0  TCP 10.171.39.246:57260->10.191.131.94:ndl-aas (CLOSE_WAIT)
   Google      579 hwte   27u  IPv4 0x4766473e82b85b03      0t0  TCP 10.171.39.246:57133->10.191.131.94:ndl-aas (CLOSED)
   VMware      809 hwte   54u  IPv4 0x4766473e82094ff3      0t0  TCP localhost:49795->localhost:8698 (ESTABLISHED)
   
   ......
   ```

3. 列出所有打开的 UDP 套接字 :

   ```shell
   hwte@sw ~ % lsof -i UDP
   COMMAND     PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
   loginwind   151 hwte    6u  IPv4 0x4766473e827a0f3b      0t0  UDP *:*
   rapportd    454 hwte    3u  IPv4 0x4766473e8260373b      0t0  UDP *:*
   
   ......
   ```



### ⭐️ps

用来显示当前进程的状态 .

* `-u` : 查看特定用户的进程信息
* `-a` : 显示其他用户以及你自己的进程信息，**这将跳过任何没有控制终端的进程，除非也指定了-x选项**
* `-A` : 显示其他用户的进程信息，包括没有控制终端的进程
* `-c` : 将 "command" 列的输出更改为只包含命令名，而不是完整的命令行
* `-f` : 显示uid、pid、父进程的pid、最近的CPU使用情况、进程启动时间、控制tty、已使用的CPU时间以及关联的command
* `-x` : 在显示由其他选项所匹配到的进程时，**+显示包括没有控制终端的进程**
* `-v` : 显示与关键词 pid、state、time、sl、re、pagein、vsz、rss、lim、tsiz、%cpu、%mem、commmand 关联的信息

1. 查看其他用户以及你自己的进程信息（详细的进程信息）:

   ```shell 
   hwte@sw demo % ps -a -v
     PID STAT      TIME  SL  RE PAGEIN      VSZ    RSS   LIM     TSIZ  %CPU %MEM COMMAND
   14512 Ss     0:00.01   0   0      0 408647504   4528     -        0   0.0  0.0 login -pf hwte
     ......
   ```

2. 查看其他用户以及你自己的进程信息（详细的进程信息）& 只显示包含指定 pattern 的信息 : 

   ```shell
   hwte@sw demo % ps -a -v | grep Python 
   14722 R+    10:07.50   0   0      0 408727760   5280     -        0  64.3  0.0 /Library/Frameworks/Python.framework/Versions/3.12/Resources/Python.app/Contents/MacOS/Python py_script.py
   ......
   ```




## 网络命令

### ipconfig

用来查看网络接口信息，以及为网络接口分配地址 & 配置网络接口参数 .

`-h` : 查看帮助文档

1. 显示所有网络接口的状态，若因信息量过多，可配合 `less` 命令哈 :  

   ```shell
   hwte@sw ~ % ifconfig | less
   ```

2. 显示指定网络接口的状态 : 

   ```shell
   hwte@sw ~ % ifconfig en0
   en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
   	options=50b<RXCSUM,TXCSUM,VLAN_HWTAGGING,AV,CHANNEL_IO>
   	ether 18:4a:53:0d:fc:c7 
   	inet6 fe80::1c19:56b9:bcce:624%en0 prefixlen 64 secured scopeid 0x9 
   	inet 10.171.39.246 netmask 0xfffffc00 broadcast 10.171.39.255
   	nd6 options=201<PERFORMNUD,DAD>
   	media: autoselect (1000baseT <full-duplex,energy-efficient-ethernet>)
   	status: active
   ```
   
3. 获取指定网络接口中的特定信息 : 

   ```shell
   hwte@sw ~ % ifconfig en0 | grep inet
   	inet6 fe80::1c19:56b9:bcce:624%en0 prefixlen 64 secured scopeid 0x9 
   	inet 10.171.39.246 netmask 0xfffffc00 broadcast 10.171.39.255
   ```



### route

用来查看和修改网络路由表 .

**注 : MacOS Terminal (M2) 中这条命令的用法与 Linux 中的用法大不同 .**



### ping

`ping`命令是一个网络诊断工具，它允许你检查与远程或本地计算机的网络连接 .

* `c` : 指定发送的 ping 包数量
* `s` : 设置 ping 包的大小
* `i` : 指定 ping 的频率（秒）
* `t` : 设置超时时间（秒），即若超出此时间则停止 ping
* `h` : 查看帮助文档

1. 检查与特定主机的连接 :

   ```shell
   ping 10.171.38.244
   ```

2. 指定发送的 ping 包数量 :

   ```shell
   hwte@sw ~ % ping -c 1 10.171.38.244
   PING 10.171.38.244 (10.171.38.244): 56 data bytes
   64 bytes from 10.171.38.244: icmp_seq=0 ttl=255 time=0.464 ms
   
   --- 10.171.38.244 ping statistics ---
   1 packets transmitted, 1 packets received, 0.0% packet loss
   round-trip min/avg/max/stddev = 0.464/0.464/0.464/nan ms
   ```

3. 设置 ping 包的大小为 1024 B :  

   ```shell
   hwte@sw ~ % ping -s 2024 10.171.38.244 
   PING 10.171.38.244 (10.171.38.244): 2024 data bytes
   2032 bytes from 10.171.38.244: icmp_seq=0 ttl=64 time=0.896 ms
   ......
   ```

4. 指定 ping 的频率为 5，即间隔 5 秒 ping 一次 : 

   ```shell
   hwte@sw ~ % ping -i 5 10.171.38.244
   PING 10.171.38.244 (10.171.38.244): 56 data bytes
   64 bytes from 10.171.38.244: icmp_seq=0 ttl=64 time=0.706 ms
   ......
   ```

5. 设置超时时间为 10，即 10 秒后停止 ping : 

   ```shell 
   hwte@sw ~ % ping -t 10 10.171.38.244
   PING 10.171.38.244 (10.171.38.244): 56 data bytes
   64 bytes from 10.171.38.244: icmp_seq=0 ttl=255 time=4.452 ms
   ......
   ```




### ⭐️traceroute

用于跟踪从一个主机到另一个主机之间的数据包路径 .

* `-n` : 只显示数字形式的 IP 地址，不进行域名解析
* `-w` : 设置等待每个响应的时间（以秒为单位）
* `-m` : 设置最大跳数
* `-v` : 详细显示指令的执行过程
* `-h` : 查看帮助文档

1. 只显示数字形式的IP地址，不进行域名解析 : 

   ```shell
   hwte@sw ~ % traceroute -n 10.191.130.130  
   traceroute to 10.191.130.130 (10.191.130.130), 64 hops max, 52 byte packets
    1  10.171.36.2  1.435 ms  0.559 ms  0.403 ms
    2  10.175.126.210  0.924 ms  0.862 ms  0.772 ms
    ......
   ```

2. 设置等待每个响应的时间（以秒为单位）:

   ```shell
   hwte@sw ~ % traceroute -w 10 10.191.130.130
   traceroute to 10.191.130.130 (10.191.130.130), 64 hops max, 52 byte packets
    1  10.171.36.2 (10.171.36.2)  1.268 ms  0.599 ms  0.465 ms
    2  10.175.126.210 (10.175.126.210)  2.946 ms  3.312 ms  0.897 ms
    ......
   ```

3. 设置最大跳数 & 详细显示指令的执行过程 : 

   ```shell
   hwte@sw ~ % traceroute -m 2 -v 10.191.130.130
   traceroute to 10.191.130.130 (10.191.130.130), 2 hops max, 52 byte packets
    1  10.171.36.2 (10.171.36.2) 36 bytes to 10.171.39.246  1.173 ms  0.498 ms  0.448 ms
    2  10.175.126.210 (10.175.126.210) 36 bytes to 10.171.39.246  0.839 ms  0.771 ms  0.747 ms
   ```



### netstat

用于显示与IP、TCP、UDP和ICMP协议相关的统计数据，一般用于检验本机各端口的网络连接情况 .

* `-p tcp` : 显示 TCP 的连接信息
* `-p udp` : 显示 UDP 的连接信息
* `-h` : 查看使用文档

1. 显示 TCP 的连接信息 : 

   ```shell
   hwte@sw ~ % netstat -p tcp
   Active Internet connections
   Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)    
   tcp4       0      0  10.171.39.246.58753    10.191.131.94.ndl-aas  FIN_WAIT_2 
   tcp4       0      0  localhost.4907         localhost.56078        ESTABLISHED
   tcp4       0      0  10.171.39.246.51743    10.191.131.94.3128     TIME_WAIT 
   ......
   ```

2. 显示 UDP 的连接信息 : 

   ```shell
   hwte@sw ~ % netstat -p udp
   Active Internet connections
   Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)    
   udp4       0      0  10.171.39.246.63083    42.194.136.76.interwis            
   udp4       0      0  10.171.39.246.59075    42.194.136.76.interwis    
   ......
   ```

3. 筛选指定的 TCP 连接信息 :

   ```shell 
   # 筛选包含端口号为 4906 的信息
   hwte@sw ~ % netstat -p tcp | grep 4906       
   tcp4       0      0  localhost.4906         localhost.56074        ESTABLISHED
   tcp4       0      0  localhost.56074        localhost.4906         ESTABLISHED
   tcp4       0      0  localhost.4906         localhost.56073        ESTABLISHED
   ......
   # 筛选连接状态为 ESTABLISHED 的信息
   hwte@sw ~ % netstat -p tcp | grep ESTABLISHED
   tcp4       0      0  localhost.4907         localhost.56078        ESTABLISHED
   tcp4       0      0  localhost.4907         localhost.56077        ESTABLISHED
   tcp4       0      0  localhost.56078        localhost.4907         ESTABLISHED
   ......
   ```



### telnet

允许你通过Telnet协议连接到远程计算机或设备 .

⚠️注意 : `telnet`命令是一种不安全的通信方式，因为它不加密数据，故对于敏感操作或需要安全连接的情况，应使用更安全的协议，如`SSH（Secure Shell）`. 



### ⭐️ssh

SSH（Secure Shell）是一种用于安全登录远程计算机的网络协议，通过 SSH，可以在不受干扰的情况下，传输服务器操作系统和网络管理中的各种命令，**它可以通过加密来保护传输的数据，使其难以被截取和窃听 .**

* `-i` : 指定身份验证文件（公钥），用于身份验证
* `-p` : 指定远程 SSH 服务器监听的端口号，默认为 22
* `-l` : 指定登录用户名，如果不指定将使用本地登录用户名
* `-h` : 查看帮助文档

1. 使用 SSH 连接远程主机 : 

   ```shell
   ssh user_name@ip_address
   ```

2. SSH 默认使用 22 号端口与远程主机通信，如果需要使用其他端口，可以使用 `-p` 参数指定 : 

   ```shell
   ssh -p port_number user_name@ip_address
   ```

3. 生成密钥对，按提示输入要保存密钥对的文件名、密码等信息 : 

   注 : `ssh-keygen`命令是用来生成 SSH 密钥的 .

   * `-t` : 选项用于指定密钥类型
   * `-h` : 查看帮助文档

   ```shell
   hwte@sw demo % ssh-keygen -t rsa   
   Generating public/private rsa key pair.
   Enter file in which to save the key (/Users/hwte/.ssh/id_rsa): id_rsa_demo
   Enter passphrase (empty for no passphrase): 
   Enter same passphrase again: 
   Your identification has been saved in id_rsa_demo
   Your public key has been saved in id_rsa_demo.pub
   The key fingerprint is:
   SHA256:T9qJMce1Ju1Bn3p7vSkRk+PIoq+ZbNtZBRYaFjTDAb8 hwte@sw.local
   The key's randomart image is:
   +---[RSA 3072]----+
   |       .+Oo.     |
   |        o.= .    |
   |         o oo .  |
   |         .o+.B . |
   |        SE* B.*  |
   |         @ B.=   |
   |        + =.o o .|
   |      .o+ o  o .+|
   |      .*++    o+.|
   +----[SHA256]-----+
   hwte@sw demo % ls -l
   total 16
   -rw-------  1 hwte  staff  2675  7 12 09:05 id_rsa_demo
   -rw-r--r--  1 hwte  staff   580  7 12 09:05 id_rsa_demo.pub
   ```

4. 将公钥上传到远程主机的 `authorized_keys` 文件中，之后可以免密登录 : 

   注 : `ssh-copy-id` 命令允许你快速而简单地将你的公钥添加到远程服务器上的 authorized_keys 文件中 .

   * `-i` : 指定要使用的私钥文件，若未指定将尝试使用默认的私钥文件
   * `-p` : 指定远程服务器的 SSH 端口，若未指定将使用默认的 SSH 端口（22）
   * `-h` : 查看帮助文档

   ```shell
   ssh-copy-id user_name@ip_addresss
   ```

5. 在 SSH 登录成功后，可以在远程主机上执行命令 : 

   ```shell 
   ssh user_name@ip_address "shell_command"
   ```



### scp

`scp`（secure copy）命令是一个用于在本地或远程主机之间安全地复制文件的工具，它基于`SSH`（Secure Shell）协议，这意味着在传输过程中，文件数据是加密的 .

* `-r` : 递归复制指定目录中子目录及文件
* `-v` : 启用详细输出，以便跟踪复制过程
* `-P` : 指定连接时使用的SSH端口号
* `-i` :  指定身份验证文件（公钥），用于身份验证
* `-h` : 查看帮助文档

1. 上传文件到远程服务器 / 从远程服务器下载文件 : 

   ```shell
   scp local_file_path user_name@ip_address:path 
   ```

   ```shell
   scp user_name@ip_address:path local_file_path
   ```

2. 上传整个目录到远程服务器 / 从远程服务器下载整个目录 : 

   ```shell
   scp -r local_directory_path user_name@ip_address:path
   ```

   ```shell
   scp -r user_name@ip_addresss:path local_directory_path
   ```

3. 使用通配符上传多个文件 / 使用通配符下载多个文件 : 

   ```shell
   scp local_directory_path/*.txt user_name@ip_address:path
   ```

   ```shell
   scp user_name@ip_address:path/*.txt local_directory_path
   ```




### ⭐️curl

用于下载文件、发送HTTP请求、代理服务器、文件上传等，它支持多种协议，包括HTTP、HTTPS、FTP、SFTP等 .

* `-o` : 指定下载的文件输出到哪个文件

* `-O` : 但使用远程文件名作为本地文件名

* `-#` : 显示一个进度条来指示下载或上传的进度

* `-x` : 指定代理服务器

* `-T` : 上传文件到服务器

* `--head` : 获取服务器的响应头而不下载文件内容

* `--connect-timeout` : 设置连接超时时间（以秒为单位）

* `--help` : 查看简洁的帮助文档

  `--help all` : 查看完整的帮助文档

1. 简单地从网站下载一个文件 : 

   ```shell
   curl https://example.com/file.zip
   ```

2. 下载文件并保存到本地指定目录 : 

   ```shell
   curl -o /local_path/file.zip https://example.com/file.zip
   ```

3. 使用`-O`选项，将下载的文件保存为源文件的名字 : 

   ```shell
   curl -O https://example.com/file.zip
   ```

4. 查看下载进度 : 

   ```shell
   curl -# https://example.com/file.zip
   ```

5. 使用代理服务器进行下载 :

   ```shell
   curl -x http://ip_address:port_number https://example.com/file.zip
   ```

   ⚠️注 : 如果你使用需验证身份的代理，你需要在`curl`命令中指定用户名和密码 :

   ```shell 
   # 设置 http 的代理
   curl --proxy http://user:password@ip_address:port_number https://example.com
   # 或设置 https 代理
   curl --proxy https://user:password@ip_address:port_number https://example.com
   ```

6. 上传文件到服务器 : 

   ```shell
   curl -T /local_path/file.zip https://example.com/upload
   ```

7. 使用`--head`选项，获取服务器的响应头而不下载文件内容 : 

   ```shell
   curl --head https://example.com/file.zip
   ```

8. 设置超时时间（例如30秒）: 

   ```shell
   curl --connect-timeout 30 https://example.com/file.zip
   ```



## 定时任务
### ⭐️at

在一个指定的时间执行一个指定的任务，**且只能执行一次** .

* `-b` :  **`batch`**命令的别名
* `-c` : 查看指定 ID 的任务的详细内容
* `-f` : 从文件中读取作业，而不是标准输入
* `-l` : 在没有参数的情况下，列出当前用户的所有作业，如果给出一个或多个作业编号，则只列出给定编号的作业
* `-m` : 即使没有输出，当作业完成时，也要向用户发送邮件
* `-q queue` : 使用指定的队列。队列标识由单个字母组成，有效的队列标识从 a 到 z 和 A 到 Z
* `-r` : 删除指定的作业
* `-t` : 使用 POSIX 时间格式指定作业时间，参数的格式为 : `[[CC]YY]MMDDhhmm[.SS]`
* `-v` : 对于**`atq`**命令，显示队列中已完成但尚未删除的作业，否则显示作业将执行的时间

在Unix系统中，`at`、`atq`、`atrm` 和 `batch` 是几个相关的命令，它们用于管理作业调度 : 

* `at` : 用于安排在将来某个时间点执行的作业，当你使用 `at` 命令时，会进入一个**交互式会话**，你可以在其中输入要执行的命令，提交作业后，它将根据指定的时间表执行 :

  ```shell
  hwte@sw ~ % at 18:57
  echo 'hello world at 18:57'
  job 3 at Sun Jul 14 18:57:00 2024 # 按下 Ctrl + D 键来提交作业
  ```

* `atq` : 用于列出所有作业的 ID 和执行时间

  ```shell
  hwte@sw ~ % atq
  4	Sun Jul 14 18:50:00 2024
  3	Sun Jul 14 18:57:00 2024
  ```

* `atrm` : 用于删除已经安排的作业，使用 `atq` 命令获取作业ID，然后使用 `atrm` 命令删除指定 ID 的作业

  ```shell
  hwte@sw ~ % atrm 3 
  hwte@sw ~ % atq   
  4	Sun Jul 14 18:50:00 2024
  ```

* `batch` : 与 `at` 命令类似，但它用于在非交互模式下运行作业，通常`batch`命令用于在后台执行脚本或程序 .

`at`命令的时间格式 : 

* `HH:MM` : 例如 06:00，在今天的 6 点执行一次该任务，若 6 点已过则明天 6 点再次执行
* `HH:MM YYY-MM-DD` : 例如 `17:30 2024-07-14`
* `HH:MM[am|pm] [Month] [Date]` : 例如 `05:30pm March 17`，即在 3 月 17 号下午 5 点 30 分执行一次该任务
* `HH:MM[am|pm] + number [minutes|hours|days|weeks]` : 例如 `now + 10 minutes`，即在 10 分钟后执行一次该任务，又例如 `05:30pm + 3 weeks`，即在 3 周后的下午 5 点 30 分执行一次该任务



### ⭐️crontab

在固定的间隔时间执行指定的系统指令或脚本 .

#### 与`at`命令的区别

`at` 适合于需要在未来某个特定时间**执行一次**的任务，而 `crontab` 则适合于需要**定期执行**的任务，**并且它提供了更加复杂的调度选项** .

#### 与`cron`命令的区别

简而言之，**cron 是实际执行任务的`进程`，而 crontab 是告诉 cron 何时何地执行这些任务的`配置文件`**，用户通过编辑自己的 crontab 来设置任务，这些任务会被 cron 守护进程周期性检查和执行 .

#### 常用参数

* `-u user` : 指定要操作的用户，默认为当前用户
* `-l` : 列出 crontab 文件内容，若不指定用户，则显示当前用户的 crontab 文件内容
* `-r` : 移除 crontab 文件内容，若不指定用户，则删除当前用户的 crontab 文件
* `-e` : 编辑 crontab 文件内容，若不指定用户，则编辑当前用户的 crontab 文件

#### 权限文件

* ` /usr/lib/cron/cron.deny` : 该文件中所列用户**不允许**使用 crontab 命令
* `/usr/lib/cron/cron.allow` : 该文件中所列用户**允许**使用 crontab 命令
* 注 : 如果 cron.allow 文件存在，使用 crontab 命令的前提是你的用户名**在** cron.allow 文件中，如果 cron.allow 文件不存在，但 cron.deny 文件存在，使用 crontab 命令的前提是你的用户名**不在** cron.deny 文件中，如果这两个文件都不存在，然后根据站点特定的配置参数，只有超级用户才能使用 crontab 命令，或者所有用户都将能使用 crontab 命令 .

#### crontab 文件

用户所建立的`crontab`文件中，每一行都代表一项任务，每行的每个字段代表一项设置，它的格式共分为六个字段，前五段是时间设定段，第六段是要执行的命令段，格式如下 : 

```shell
*    *    *    *    *    *
-    -    -    -    -    -
|    |    |    |    |    |+----- 命令: 可以是系统命令,也可以是自己编写的脚本文件
|    |    |    |    +----- 星期几 (0 - 7) (星期天为 0 或 7 ) 或 sun,mon,tue,wed,thu,fri,sat 
|    |    |    +---------- 月份 (1 - 12) 或 jan,feb,mar,apr... 
|    |    +--------------- 号数 (1 - 31) 即一个月中的第几天
|    +-------------------- 小时 (0 - 23)
+------------------------- 分钟 (0 - 59)
```

在以上各个字段中，还可以使用以下特殊字符 : 

* 星号(`*`) : 表示所有可能的值，例如 month 字段如果是星号，则表示在满足其它字段的制约条件后**每月都执行**该命令操作 .

  注 : crontab 每次检查的时间间隔为 1 分钟，所以如果 5 个都是`*`，表示每分钟都执行一次

* 逗号(`,`) : 表示一个列表范围，例如 "1,2,5,7,8,9" 若用在 `号数` 字段，则表示每月的 1,2,5,7,8,9 号

* 中杠(`-`) : 表示一个整数范围，例如 "2-6" 表示 "2,3,4,5,6"，其若用在 `星期几` 字段，则表示每周的周 2,3,4,5,6

* 正斜线(`/`) : 表示时间的间隔频率，例如 "0-23/2" 表示每两小时执行一次，正斜线可以和星号一起使用，例如 "*/10" 若用在 `分钟` 字段，则表示每 10 分钟执行一次

使用特殊字符示例的如下，该行代码的含义为 : 在`1月和2月`的`1-5号以及10号`，在`6-13点之间每隔2小时，以及17点`，以及`第 15/30/45 分`执行脚本 `/home/usr/script.sh` .

```shell
15,30,45 6-13/2,17 1-5,10 jan,feb * /home/usr/script.sh
-------- --------- ------ ------- - -------------------
|            |        |      |    |         |+----- (5).执行脚本/home/usr/script.sh
|            |        |      |    +----- (2).周一到周日
|            |        |      +---------- (1).1月和2月
|            |        +--------------- (2).1-5号及10号
|            +-------------------- (3).6-13点之间每隔2小时,以及17点
+------------------------- (4).第15,30,45分钟
```

#### crontab 的增删改查

1. 创建一个名为`<user>cron`的文件，其中`<user>`是指用户名，例如 hwtecron : 

   ```shell
   # echo the date to the file.txt file every minute
   * * * * * /bin/echo $(date) >> ~/file.txt
   ```

2. 为了提交你刚刚创建的 crontab 文件，可以把这个新创建的文件作为 crontab 命令的参数 : 

   ```shell
   # 提交 crontab 文件，即使其生效，命令格式为: crontab <crontab_file_name>
   hwte@sw ~ % crontab hwtecron
   ```

3. 查看当前用户的 crontab 文件内容 : 

   ```shell
   hwte@sw ~ % crontab -l      
   # echo the date to the file.txt file every minute
   * * * * * /bin/echo $(date) >> ~/file.txt
   ```

   注 : 可以使用下述方法在指定目录中对 crontab 文件做一份备份，以防平时不小心误删了 crontab 文件 : 

   ```shell
   # 对 crontab 文件做一份备份，备份文件名为 backup_hwtecron
   hwte@sw ~ % crontab -l > backup_folder/backup_hwtecron
   
   # 查看备份文件的内容
   hwte@sw ~ % cat backup_folder/backup_hwtecron 
   # echo the date to the file.txt file every minute
   * * * * * /bin/echo $(date) >> ~/file.txt
   ```

4. 编辑 crontab 文件，即更新其内容，可以使用 `$crontab -e` 命令来编辑当前用户的 crontab 文件内容，例如更新后的内容为 : 

   ```shell
   # echo the date to the file.txt file                                        
   * * * * * /bin/echo 'The Current Time is:' $(date) >> ~/file.txt
   ```

5. 删除 crontab 文件 : 

   ```shell
   # 查看当前用户的 crontab 文件内容
   hwte@sw ~ % crontab -l
   # echo the date to the file.txt file every minute
   * * * * * /bin/echo 'The Current Time is:' $(date) >> ~/file.txt
   
   # 删除当前用户的 crontab 文件
   hwte@sw ~ % crontab 文件 -r
   
   # 再次查看当前用户的 crontab 文件内容
   hwte@sw ~ % crontab -l
   crontab: no crontab for hwte
   ```

   注 : 若不小心误删了 crontab 文件，假设你还有一个备份文件，如 3 中名为 `backup_hwtecron` 的备份文件，你可以通过命令 `crontab <crontab_file_name>` 来快速恢复误删的 crontab 文件 : 

   ```shell
   hwte@sw ~ % crontab backup_folder/backup_hwtecron 
   hwte@sw ~ % crontab -l
   # echo the date to the file.txt file every minute
   * * * * * /bin/echo $(date) >> ~/file.txt
   ```

#### 使用技巧

1. 一次执行多个命令的方法 : 

   ```shell
   # 方法一: 在脚本文件里写多个命令
   # 方法二: 命令在 crontab 里面用括号括起来，中间用分号隔开，例如:
   * * * * * (command_1;command_2;...)
   # 方法三: 使用 `run-parts` 执行指定文件夹内的所有脚本，例如:
   * * * * * root run-parts /path/script_folder
   ```

2. 启动就执行的命令如何设置 : 

   ```shell
   # 用 @reboot 起头，最好加上延迟，以防网络未就绪导致某些脚本无法顺利执行，例如:
   @reboot (sleep 60 && /path/script.sh)
   ```

3. 修改`crontab`默认编辑器的方法 : 

   ```shell
   # 在配置文件中（如`.bash_profile`或`.zshrc`）里面添加一行设置 `EDITOR` 的环境变量并使其生效即可，
   # 例如指定 crontab 的默认编辑器为 vim:
   echo 'EDITOR="/usr/bin/vim"' >> ~/.zshrc
   # 然后立即应用配置文件中的设置:
   source ~/.zshrc
   ```
   
   或者简单粗暴直接**临时**切换编辑器，并开始编辑 : 

   ```shell
   export EDITOR='/usr/bin/vim';crontab -e
   ```

#### 使用示例

1. 示例一 : 每 1 分钟执行一次 command 命令 :  

   ```shell
   * * * * * command
   ```

2. 示例二 : 每 1 小时执行一次 command 命令 : 

   ```shell
   * */1 * * * command
   ```

3. 示例三 : 每小时的第 3 和 15 分钟执行一次 command 命令 : 

   ```shell 
   3,15 * * * * command
   ```

4. 示例四 : 每天上午 8 到 11 点，其中每小时的第 3 和 15 分钟执行一次 command 命令 : 

   ```shell
   3,15, 8-11 * * * command
   ```

5. 示例五 : 每隔 2 天的上午 8 到 11 点，其中每小时的第 3 和 15 分钟执行一次 command 命令 : 

   ```shell
   3,15 8-11 */2 * * command
   ```

6. 示例六 : 每个星期一的上午 8 到 11 点，其中每小时的第 3 和 15 分钟执行一次 command 命令 : 

   ```shell
   3,15 8-11 * * 1 command
   ```

7. 示例七 : 每月的 1，10，22 号的上午 8:00 执行一次 command 命令 : 

   ```shell 
   0 8 1,10,22 * * command
   ```

8. 示例八 : 1，3，5月的 1，10，22 号的下午 17:30 执行一次 command 命令 : 

   ```shell
   30 17 1,10,22 1,3,5 * command
   ```

#### 注意事项

* Shell 脚本第一行记得声明 `#!/bin/bash`

* 记得检查脚本文件是否具有执行权限，添加执行权行的命令为 `chmod +x <script_file>`

* 脚本中的路径最好用**绝对路径**，可以避免很多错误

* **脚本执行要用到环境变量时，必须引入环境变量**，

  例如当手动执行脚本OK，但是`crontab`不执行时。这时必须大胆怀疑是环境变量惹的祸～

* 谨慎使用命令 `crontab -r`，它会删除用户所有的 crontab 文件

* 在 crontab 中`%`是有特殊含义的，表示换行的意思，如果要用的话必须转义为`\%`



## 其它命令
### pwd

用于查看"当前工作目录"的完整路径 .




### ⭐️grep

它允许你使用正则表达式来匹配指定字符串，**也可用于匹配文件内容中包含指定字符串的行**

* `-w --word-regexp` : 匹配指定单词

* `-x, --line-regexp` :  只匹配整个行，而不是行的部分

* `-c --count` : 只打印匹配到的次数

* `-i --ignore-case` : 匹配时不区分大小写

* `-n, --line-number` : 在匹配的行前面加上行号

* `-l --files-without-match` : 只打印包含指定匹配模式的文件名

* `-H` : 打印包含匹配模式的行，及其文件名

* `-R, -r, --recursive` : 在指定子目录中进行递归搜索

* `--include pattern` : 仅对包含指定 pattern 的文件进行匹配

* `--include-dir pattern` : 仅对包含指定 pattern 的文件夹进行匹配

* `--colour=[when], --color=[when]` : 

  ​       Mark up the matching text with the expression stored in the

  ​       GREP_COLOR environment variable. The possible values of when are

  ​       “**never**”, “**always**” and “**auto**”.

常用参数示例（注 : `.`表示当前目录）: （❌下述命令待重测）

```shell
hwte@sw demo % cat folder_1/first.txt folder_2/second.txt folder_3/third.md  
hello world
hello 2024
HELLO WORLD
HELLO 2024
hello world
HELLO 2024
helloHELLO world and 2024
hwte@sw demo % grep -H -R -w -i -n --colour='always' --include='*.md' hello .
./folder_3/third.md:1:hello world
./folder_3/third.md:2:HELLO 2024
```



### wc

用于计算单词、行数、字节数 .

- `-c` : 显示字节数
- `-l` : 显示行数
- `-m` : 显示字符数
- `-w` : 显示单词数

注 : 若不指定参数，`-l`，`-w`，`-c` 为默认参数参数，示例如下 : 

```shell
hwte@wc demo % cat file_1.txt 
hello 2024 
hwte@wc demo % wc file_1.txt 
       1       2      11 file_1.txt
```

结合其它命令的常用用法 : 

1. 查看当前目录下后缀为 .txt 的文件的行数，单词数，字符数 : 

   ```shell
   hwte@sw demo % cat file_1.txt            
   hello 2024
   hwte@sw demo % cat file_2.txt 
   hello 2024
   hwte@sw demo % cat file_3.md 
   hello 2024
   hwte@sw demo % cat *.txt | wc  
          2       4      22
   ```

2. 查看当前目录下所有文件的行数，单词数，字符数 : 

   ```shell
   hwte@sw demo % find . -type f -exec wc {} \; 
          1       2      11 ./file_1.txt
          1       2      11 ./file_2.txt
          1       2      11 ./file_3.md
   ```



### watch

允许你周期性地运行一个命令，并将结果输出在屏幕上 .

**注 : MacOS Terminal (M2) 没有这条命令 .**




### ⭐️make

用于自动化编译、链接和安装等步骤，其是基于一个名为`Makefile`的文件来工作的，此文件包含了构建软件所需的指令和规则 .

* `make all` 或 `make`：编译所有目标文件和可执行文件，这是最常见的用法
* `make clean`：删除所有编译生成的目标文件和可执行文件，以便于从源代码开始重新编译
* `make install`：将编译好的可执行文件和相关文件安装到系统的指定位置

一个 `Makefile` 可能包含以下内容 : 

```shell
all:
    # 编译源代码
    gcc -o myprogram src/*.c

test: all
    # 运行测试套件
    ./myprogram test/testcases.txt

install: all
    # 将可执行文件安装到指定位置
    install -D myprogram /usr/bin
    chmod +x /usr/bin/myprogram

clean:
    # 删除编译生成的文件
    rm -f myprogram
```



### sort

排序或合并文本，及二进制文件中的记录（行）.

* `-f` : 忽略大小写
* `-r` : 反向排序
* `-n` : 按数字大小排序

1. 对文件内容进行排序 : 

   ```shell
   # 查看文件内容
   hwte@sw demo % cat file.txt 
   BBB222
   ...
   222BBB
   ---
   
   aaa111
   ///
   111aaa
   """
   # 对文件内容进行正向排序（忽略大小写）
   hwte@sw demo % sort -f file.txt 
   
   """
   ---
   ...
   ///
   111aaa
   222BBB
   aaa111
   BBB222
   # 对文件内容进行逆向排序（忽略大小写）
   hwte@sw demo % sort -fr file.txt 
   BBB222
   aaa111
   222BBB
   111aaa
   ///
   ...
   ---
   """
   
   # 对文件内容进行逆向排序（忽略大小写）（加`-n`使得数字在前）
   hwte@sw demo % sort -frn file.txt
   222BBB
   111aaa
   aaa111
   BBB222
   ///
   ...
   ---
   """
   ```

2. 结合`ls`命令对当前目录下的文件进行排序 : 

   ```shell
   # 按照文件大小正向排序
   hwte@sw app % ls -l | sort   
   -rw-r--r--  1 hwte  staff     363329  4 24 14:29 lua-5.4.6.tar.gz
   -rw-r--r--@ 1 hwte  staff      87533  6  5 18:48 jquery-3.7.1.min.js
   -rw-r--r--@ 1 hwte  staff   14322439  4 12 11:34 Typora.dmg
   -rw-r--r--@ 1 hwte  staff   45672323  4 12 11:51 python-3.12.3-macos11.pkg
   -rw-r--r--@ 1 hwte  staff   74189227  4 24 08:34 node-v20.12.2.pkg
   -rw-r--r--@ 1 hwte  staff  222312294  4 12 11:19 VSCode-darwin-universal.zip
   -rw-r--r--@ 1 hwte  staff  262707263  6 12 07:54 Xmind-for-macOS-24.04.dmg
   total 1210288
   # 按照文件大小逆向排序
   hwte@sw app % ls -l | sort -r
   total 1210288
   -rw-r--r--@ 1 hwte  staff  262707263  6 12 07:54 Xmind-for-macOS-24.04.dmg
   -rw-r--r--@ 1 hwte  staff  222312294  4 12 11:19 VSCode-darwin-universal.zip
   -rw-r--r--@ 1 hwte  staff   74189227  4 24 08:34 node-v20.12.2.pkg
   -rw-r--r--@ 1 hwte  staff   45672323  4 12 11:51 python-3.12.3-macos11.pkg
   -rw-r--r--@ 1 hwte  staff   14322439  4 12 11:34 Typora.dmg
   -rw-r--r--@ 1 hwte  staff      87533  6  5 18:48 jquery-3.7.1.min.js
   -rw-r--r--  1 hwte  staff     363329  4 24 14:29 lua-5.4.6.tar.gz
   ```

3. 结合`find`命令对匹配到的文件进行排序 : 

   ```shell 
   # 查找当前目录下的 Markdown 文件，并按照文件大小正向排序
   hwte@sw note % find . -name '*.md' -exec ls -l {} \; | sort   
   -rw-r--r--@ 1 hwte  staff  13843  7  5 22:32 ./others/sqlite3-learning-note(uploaded).md
   -rw-r--r--@ 1 hwte  staff  6142  6 26 11:12 ./others/userful-git-command-in-real-dev.md
   -rw-r--r--@ 1 hwte  staff  91713  7 15 10:43 ./others/useful-command-in-linux.md
   -rw-rw-r--@ 1 hwte  staff  151156  7  5 21:37 ./python/python-learning-note-newest.md
   # 查找当前目录下的 Markdown 文件，并按照文件大小逆向排序
   hwte@sw note % find . -name '*.md' -exec ls -l {} \; | sort -r
   -rw-rw-r--@ 1 hwte  staff  151156  7  5 21:37 ./python/python-learning-note-newest.md
   -rw-r--r--@ 1 hwte  staff  91713  7 15 10:43 ./others/useful-command-in-linux.md
   -rw-r--r--@ 1 hwte  staff  6142  6 26 11:12 ./others/userful-git-command-in-real-dev.md
   -rw-r--r--@ 1 hwte  staff  13843  7  5 22:32 ./others/sqlite3-learning-note(uploaded).md
   ```



### ⭐️export

用于设置或导出环境变量，环境变量是可以在 shell 会话期间访问的值，它可以影响 shell 和在其上运行的程序的行为 .

1. 在终端中，设置需要身份验证的代理 : 

   ⚠️**注 : 使用`export`命令设置的环境变量只对当前终端会话有效，即关闭该终端后环境变量将失效，除非你将它们导出到配置文件中 ！**

   ```shell
   # 设置 http 与 https 代理
   export http_proxy="http://<user>:<password>@<proxy_server>:<proxy_port>"
   export https_proxy="https://<user>:<password>@<proxy_server>:<proxy_port>"
   # 查看是否设置成功, 若成功则输出 key 对应的 value 值
   echo $http_proxy $https_proxy
   ```

2. 将环境变量的设置导出到配置文件中（如`.bash_profile`或`.zshrc`），以便在每次启动 shell 时都应用这些设置 : 

   ⚠️注 : 该配置文件存放在用户的 home 目录下，如果没有则新建一个 .

   ⚠️注 : `source`命令用于在当前 bash 会话中立即应用配置文件中的设置，而无需关闭并重新打开终端 .

   ⚠️注 : `.bash_profile`和 `.zshrc`都是`用户级别`的配置文件，它们用于设置 shell 的个性化环境变量和配置，但是，它们适用于不同的shell，如果你不确定使用哪个配置文件，你可以检查你的 shell 类型，即在终端中输入`echo $SHELL`，这将输出你当前使用的 shell 的路径，若输出`/bin/bash`，那么使用`.bash_profile`，若输出是其他路径，比如`/bin/zsh`，那么使用`.zshrc` .

   ⚠️注 : 区分`/bin/bash`与`/bin/zsh` : `/bin/bash`是`Bourne-Again Shell`，是大多数 Linux 发行版的默认 shell，而 `/bin/zsh`是 Z Shell，它是一个功能更强大的 shell，即相比前者 zsh 提供了更多的特性和自定义选项，通常用于高级用户和系统管理员 .

   ```shell
   # 查看 shell 类型
   hwte@sw ~ % echo $SHELL 
   /bin/zsh
   # 将环境变量的设置导出到配置文件 .zshrc 中
   hwte@sw ~ % cat ~/.zshrc 
   hwte@sw ~ % echo 'export demo_key="demo_value"' >> ~/.zshrc                            
   # 让刚刚修改的配置立刻生效
   hwte@sw ~ % source ~/.zshrc
   # 查看环境变量是否设置成功
   hwte@sw ~ % echo $demo_key   
   demo_value
   ```



### source

用于在终端中运行配置文件或脚本，以便在当前会话中立即应用其设置 .

1. **运行脚本** : 如果你有一个脚本文件，其中包含了一组命令或程序，你可以使用`source`命令来在当前会话中运行它，而不是将它作为独立程序来执行 .

   ```shell
   source script.sh
   ```

2. **环境变量** : 如果你在配置文件中设置或修改某个环境变量，可以使用`source`命令来立即应用配置文件中的设置 .

   ```shell
   echo 'export demo_key="demo_value"' >> ~/.zshrc
   source ~/.zshrc
   ```



### history

列出用户之前在终端中输入过的命令 .

1. 查看最近的历史记录，默认为 15 条 : 

   ```shell
   hwte@sw ~ % history 
    1024  ls
    ......
    1039  vim ~/.zshrc
   ```

2. 查看所有历史记录，若信息过多，可使用`less`命令 :  

   ```shell
   $ history +1 | less
   ```

   ```shell
       1  ls
   		......
      27  cat script.py
   :
   ```

3. 在所有历史记录中匹配搜索指定的命令 :

   ```shell
   hwte@sw ~ % history +1 | grep python
      11  ps -u hwte | grep python
    	 ......
     640  rm -rf python3\ packages vscode\ extensions
   ```

4. 查看从第 n 条开始的所有历史记录 : 

   ```shell
   hwte@sw ~ % history +5
       5  ls
       ......
    1044  history +1 | grep python
   ```

5. 查看所有历史记录的最后 n 条记录 :  

   ```shell
   # 例如查看所有历史记录的最后 3 条记录:
   hwte@gl-f1227452macd ~ % history -3
    1043  history +1 | less
    1044  history +1 | grep python
    1045  history +5
   ```

注 : 因当前使用的 Shell 为 `zsh`，故可以在文件夹`~/.zsh_sessions/`中找到**所有的**历史记录 : 

```shell
hwte@sw ~ % echo $SHELL
/bin/zsh
hwte@sw ~ % ls -lt ~/.zsh_sessions/ | grep history
-rw-------  1 hwte  staff  16834  7 17 21:55 FF6ED487-B8BF-419C-B888-4A11DE96569D.history
-rw-------  1 hwte  staff      0  7 17 21:53 B16946C4-11B5-4708-B8C6-1686B499872D.historynew
......
```

那么有趣的点来了！！！让我们康康我用过哪些包含`python3`字符串的命令吧 : 

```shell
hwte@sw ~ % cat ~/.zsh_sessions/*.history | grep -i python3 | less -N
```

```shell
      1 python3 --version
			......
     27 which python3
:
```



### chsh

切换到其它可用的 `Shell` .

1. 查看当前系统的默认 Shell : 

   ```shell
   hwte@sw ~ % echo $SHELL       
   /bin/zsh
   ```

2. 查看当前操作系统中已安装的所有 Shell : 

   ```shell
   hwte@sw ~ % cat /etc/shells 
   # List of acceptable shells for chpass(1).
   # Ftpd will not allow users to connect who are not using one of these shells.
   
   /bin/bash
   /bin/csh
   /bin/dash
   /bin/ksh
   /bin/sh
   /bin/tcsh
   /bin/zsh
   ```

3. 使用`chsh`命令可以改变当前系统的默认 Shell，例如我们将默认的 Shell 从`zsh`改为`bash` : 

   ```shell
   # 首先我们通过`which`命令找出`bash`可执行文件的位置
   hwte@sw ~ % which bash
   /bin/bash
   # 然后通过`chsh -s <shell_path>`命令来切换默认 Shell
   hwte@sw ~ % chsh -s /bin/bash
   Changing shell for hwte.
   Password for hwte: 
   ```

   最后打开一个新的终端，检验是否切换成功 : 

   ```shell
   Last login: Thu Jul 18 08:11:38 on ttys004
   
   The default interactive shell is now zsh.
   To update your account to use zsh, please run `chsh -s /bin/zsh`.
   For more details, please visit https://support.apple.com/kb/HT208050.
   sw:~ hwte$ echo $SHELL
   /bin/bash
   ```

   

# linux常用命令

## 一.操作文件或目录

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

1. demo

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

2. demo

   ```shell
   hwte@gl-f1227452macd note % ls -ltr 
   total 0
   drwxr-xr-x  3 hwte  staff   96  6 26 11:07 report
   drwxr-xr-x  7 hwte  staff  224  6 26 11:12 others
   drwxr-xr-x  3 hwte  staff   96  6 26 15:05 python
   ```

3. demo

   ```shell
   hwte@gl-f1227452macd note % ls -lS 
   total 0
   drwxr-xr-x  7 hwte  staff  224  6 26 11:12 others
   drwxr-xr-x  3 hwte  staff   96  6 26 15:05 python
   drwxr-xr-x  3 hwte  staff   96  6 26 11:07 report
   ```

4. demo

   ```shell
   hwte@gl-f1227452macd note % ls -lSRr 
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

### pwd

用于查看"当前工作目录"的完整路径 .

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

用于更改文件或目录的访问时间和修改时间 .

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

用于查看、连接和输出文件内容 .

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

### more 与 less 的区别

* less可以按键盘上下方向键显示上下内容，而 more 不能通过上下方向键控制显示
* less不必读整个文件，加载速度会比 more 更快
* less退出后 shell 不会留下刚显示的内容，而 more 退出后会在shell上留下刚显示的内容
* 阅读到文件结束时，less不会退出，而more会
* less可用行号或百分比作为书签浏览文件，而 more 不行
* 相比more，less提供更加友好的检索、高亮显示等操作



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



## 二.文件查找

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

whereis 命令是定位**可执行文件、源代码文件、帮助文件**在文件系统中的位置 .

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



### ❌locate

可以很快速的搜寻档案系统内是否有指定的档案 .

```shell
# 
hwte@sw Desktop % locate *.txt

WARNING: The locate database (/var/db/locate.database) does not exist.
To create the database, run the following command:

  sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist

Please be aware that the database can take some time to generate; once
the database has been created, this message will no longer appear.

hwte@sw Desktop % sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist 
Password:

# 
hwte@gl-f1227452macd Desktop % locate *.txt                                                               

WARNING: The locate database (/var/db/locate.database) does not exist.
To create the database, run the following command:

  sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist

Please be aware that the database can take some time to generate; once
the database has been created, this message will no longer appear.

# 
hwte@sw Desktop % sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
/System/Library/LaunchDaemons/com.apple.locate.plist: service already loaded
Load failed: 37: Operation already in progress
```

. . . 感觉不好用，还是学习使用 find 命令吧～



### ⭐️find

主要作用是沿着文件层次结构向下遍历，匹配符合条件的文件，并执行相应的操作 .

- `-name` : 按照文件名查找文件
- `-type` : 查找某一类型的文件
  - `-type f`：查找普通文件，这是默认的行为，如果不使用`-type`选项，`find`命令只会列出普通文件
  - `-type d`：查找目录，这会列出所有的目录，包括那些不包含任何文件的目录
  - `-type l`：查找符号链接，这会列出所有指向其他文件或目录的符号链接
  - . . .
- `-exec` : 对找到的每个文件执行一个命令，注 : 需要加上`{}`来引用找到的文件
- `-delete`：直接删除找到的文件**（谨慎使用，无法恢复）**
- `-size`：根据文件大小进行搜索，单位可以是字节b、字符c、字w、千字节k、兆字节M、吉字节G
  - `b` (bytes)
  - `c` (bytes, for counting blocks)
  - `w` (2-byte words)
  - `k` (kilobytes, 1024 bytes)
  - `M` (megabytes, 1024 kilobytes)
  - `G` (gigabytes, 1024 megabytes)

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
hwte@gl-f1227452macd backup % find nothing/note -name '*.md' -size +2k -size -4k -exec ls -l {} \;
-rw-r--r--@ 1 hwte  staff  2084  7  5 22:29 nothing/note/others/Diff_Request_Session_In_Python.md
-rw-r--r--@ 1 hwte  staff  3519  5 24 16:21 nothing/note/report/firstMonthReport.md
# 删除`指定目录下`文件名后缀为`.md` & 文件大小`2KB < file_size < 4KB`的文件，并验证是否删除成功
hwte@gl-f1227452macd backup % find nothing/note -name '*.md' -size +2k -size -4k -delete          
hwte@gl-f1227452macd backup % find nothing/note -name '*.md' -size +2k -size -4k -exec ls -l {} \;
```

二. 操作目录 : 

```shell
# 查找`当前目录下`的所有子目录
hwte@gl-f1227452macd note % find . -type d                              
.
./pytest
./python
./others
./report
# 查找`当前目录下`目录名前缀为`py`的子目录
hwte@gl-f1227452macd note % find . -type d -name 'py*'                  
./pytest
./python
# 查找`当前目录下`目录名前缀为`py`的子目录，并显示其详细信息
hwte@gl-f1227452macd note % find . -type d -name 'py*' -exec ls -la {} \;  
total 0
drwxr-xr-x  3 hwte  staff   96  7  6 22:21 .
drwxr-xr-x  7 hwte  staff  224  7  6 22:21 ..
-rw-r--r--  1 hwte  staff    0  7  6 22:21 pytest.py
total 296
drwxr-xr-x  3 hwte  staff      96  7  5 21:37 .
drwxr-xr-x  7 hwte  staff     224  7  6 22:21 ..
-rw-rw-r--@ 1 hwte  staff  151156  7  5 21:37 python-learning-note-newest.md
```



## 三.文件解压缩

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
# 简约的使用文档
hwte@sw ~ % tar -help
Usage:
  List:    tar -tf <archive-filename>
  Extract: tar -xf <archive-filename>
  Create:  tar -cf <archive-filename> [filenames...]
  Help:    tar --help
```

```shell
# 详细的使用文档
hwte@sw ~ % tar --help
tar(bsdtar): manipulate archive files
First option must be a mode specifier:
  -c Create  -r Add/Replace  -t List  -u Update  -x Extract
Common Options:
  -b #  Use # 512-byte records per I/O block
  -f <filename>  Location of archive
  -v    Verbose
  -w    Interactive
Create: tar -c [options] [<file> | <dir> | @<archive> | -C <dir> ]
  <file>, <dir>  add these items to archive
  -z, -j, -J, --lzma  Compress archive with gzip/bzip2/xz/lzma
  --format {ustar|pax|cpio|shar}  Select archive format
  --exclude <pattern>  Skip files that match pattern
  -C <dir>  Change to <dir> before processing remaining files
  @<archive>  Add entries from <archive> to output
List: tar -t [options] [<patterns>]
  <patterns>  If specified, list only entries that match
Extract: tar -x [options] [<patterns>]
  <patterns>  If specified, extract only entries that match
  -k    Keep (don't overwrite) existing files
  -m    Don't restore modification times
  -O    Write entries to stdout, don't restore to disk
  -p    Restore permissions (including ACLs, owner, file flags)
bsdtar 3.5.3 - libarchive 3.5.3 zlib/1.2.11 liblzma/5.0.5 bz2lib/1.0.8 
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
   
   hwte@gl-f1227452macd folder % ls -l                       
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
   
   hwte@gl-f1227452macd folder % ls -l
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
   hwte@sw folder % ls -l
   total 8
   -rw-r--r--  1 hwte  staff  483  7  7 17:12 file.tar.gz
   drwxr-xr-x  2 hwte  staff   64  7  7 17:17 other_folder
   
   hwte@sw folder % ls -l other_folder 
   total 0
   
   hwte@sw folder % tar -xvzf file.tar.gz -C other_folder 
   x inner_folder/
   x inner_folder/README.md
   x inner_folder/file.tar
   hwte@sw folder % ls -l
   total 8
   -rw-r--r--  1 hwte  staff  483  7  7 17:12 file.tar.gz
   drwxr-xr-x  3 hwte  staff   96  7  7 17:17 other_folder
   
   hwte@sw folder % ls -l other_folder 
   total 0
   drwxr-xr-x  4 hwte  staff  128  7  7 17:10 inner_folder
   
   hwte@sw folder % ls -l other_folder/inner_folder 
   total 8
   -rw-r--r--  1 hwte  staff     0  7  7 16:19 README.md
   -rw-r--r--@ 1 hwte  staff  2560  7  7 15:56 file.tar
   ```



### ⭐️gzip

使用广泛的压缩程序，文件经它压缩过后，其名称后面会多出 `.gz` 的扩展名 .

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
   hwte@gl-f1227452macd folder % ls -l
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 17:54 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   # 压缩当前目录下的指定文件
   # 注: 也可使用命令 gzip *，即压缩当前目录下的所有文件
   hwte@gl-f1227452macd folder % gzip README.md file.tar 
   hwte@gl-f1227452macd folder % ls -l                  
   total 16
   -rw-r--r--  1 hwte  staff   30  7  7 17:54 README.md.gz
   -rw-r--r--  1 hwte  staff  492  7  7 17:12 file.tar.gz
   ```

2. 压缩并重命名当前目录的指定文件 : 

   ```shell
   hwte@gl-f1227452macd folder % ls -l
   total 16
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   hwte@gl-f1227452macd folder % gzip -c file.tar > compressed_file.tar.gz
   hwte@gl-f1227452macd folder % ls -l                                    
   total 24
   -rw-r--r--  1 hwte  staff   492  7  7 19:40 compressed_file.tar.gz
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   ```

3. 解压缩当前目录下被 gzip 压缩的文件 : 

   ```shell
   # 解压缩当前目录下被 gzip 压缩的文件
   hwte@gl-f1227452macd folder % gzip -d README.md.gz file.tar.gz 
   hwte@gl-f1227452macd folder % ls -l
   total 16
   -rw-r--r--  1 hwte  staff     0  7  7 17:54 README.md
   -rw-r--r--  1 hwte  staff  7168  7  7 17:12 file.tar
   ```

4. 递归地压缩指定目录中的所有文件 & 在压缩时显示详细信息 : 

   ```shell
   #
   hwte@gl-f1227452macd folder % ls -lR               
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
   #
   hwte@gl-f1227452macd folder % gzip -rv inner_folder 
   inner_folder/inner_inner_folder/README.md:	  -99.9% -- replaced with inner_folder/inner_inner_folder/README.md.gz
   inner_folder/inner_inner_folder/file.tar:	   93.1% -- replaced with inner_folder/inner_inner_folder/file.tar.gz
   inner_folder/README.md:	  -99.9% -- replaced with inner_folder/README.md.gz
   inner_folder/file.tar:	   93.1% -- replaced with inner_folder/file.tar.gz
   # 
   hwte@gl-f1227452macd folder % ls -lR               
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
   #
   hwte@gl-f1227452macd folder % ls -lR
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
   # 
   hwte@gl-f1227452macd folder % gzip -rdv inner_folder 
   inner_folder/README.md.gz:	  -99.9% -- replaced with inner_folder/README.md
   inner_folder/inner_inner_folder/README.md.gz:	  -99.9% -- replaced with inner_folder/inner_inner_folder/README.md
   inner_folder/inner_inner_folder/file.tar.gz:	   93.1% -- replaced with inner_folder/inner_inner_folder/file.tar
   inner_folder/file.tar.gz:	   93.1% -- replaced with inner_folder/file.tar
   # 
   hwte@gl-f1227452macd folder % ls -lR                
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

6. 列出压缩文件的信息（包括原始文件大小、压缩后的大小、压缩比等）

   ```shell
   hwte@gl-f1227452macd folder % gzip -rl inner_folder
     compressed uncompressed  ratio uncompressed_name
             30            0 -99.9% inner_folder/README.md
             30            0 -99.9% inner_folder/inner_inner_folder/README.md
            492         7168  93.1% inner_folder/inner_inner_folder/file.tar
            492         7168  93.1% inner_folder/file.tar
   ```

7. 列出压缩文件的信息（包括原始文件大小、压缩后的大小、压缩比等）: 

   ```shell
   #
   hwte@gl-f1227452macd inner_folder % gzip file.tar 
   hwte@gl-f1227452macd inner_folder % gzip -l file.tar.gz 
     compressed uncompressed  ratio uncompressed_name
            492         7168  93.1% file.tar
   
   #
   hwte@gl-f1227452macd inner_folder % gzip -1 file.tar 
   hwte@gl-f1227452macd inner_folder % gzip -l file.tar.gz 
     compressed uncompressed  ratio uncompressed_name
            547         7168  92.3% file.tar
   
   # 
   hwte@gl-f1227452macd inner_folder % gzip -9 file.tar 
   hwte@gl-f1227452macd inner_folder % gzip -l file.tar.gz 
     compressed uncompressed  ratio uncompressed_name
            472         7168  93.4% file.tar
   ```



Have rest you need on weekday. 20:57



### unzip

`tar`命令可以配合`gzip`处理`.tar`和`.gz`格式的文件，但无法解压缩`.zip`格式的文件，要解压`.zip`文件，你可以使用`unzip`命令 .

```shell
```





## 四.文件权限设置

### chmod



### chgrp



### chown



## 五.磁盘存储

### df



### du



## 六.性能监控和优化

### top

### free

### vmstat

### lostat

### lsof



## 七.网络命令

### ipconfig

### route

### ping

### traceroute

### netstat

### telnet



## 八.其它命令

### In

### diff

### grep

### wc

### ps

### watch

### at

### crontab

### make


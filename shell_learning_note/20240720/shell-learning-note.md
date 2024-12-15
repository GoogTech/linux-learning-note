# Shell 学习笔记

## 参考教程

* https://wangdoc.com/bash/
* https://www.runoob.com/linux/linux-shell.html



## 预备知识

### Shell 简介

Shell 这个单词的原意是“外壳”，跟 kernel（内核）相对应，比喻内核外面的一层，即用户跟内核交互的对话界面。

具体来说，Shell 这个词有多种含义。

首先，Shell 是一个程序，提供一个与用户对话的环境。这个环境只有一个命令提示符，让用户从键盘输入命令，所以又称为命令行环境（command line interface，简写为 CLI）。Shell 接收到用户输入的命令，将命令送入操作系统执行，并将结果返回给用户。本书中，除非特别指明，Shell 指的就是命令行环境。

其次，Shell 是一个命令解释器，解释用户输入的命令。它支持变量、条件判断、循环操作等语法，所以用户可以用 Shell 命令写出各种小程序，又称为脚本（script）。这些脚本都通过 Shell 的解释执行，而不通过编译。



### Shell 种类

Shell 有很多种，只要能给用户提供命令行环境的程序，都可以看作是 Shell，其中 Bash 是目前最常用的 Shell .

历史上，主要的 Shell 有下面这些。

- Bourne Shell（sh）
- Bourne Again shell（bash）
- C Shell（csh）
- TENEX C Shell（tcsh）
- Korn shell（ksh）
- Z Shell（zsh）
- Friendly Interactive Shell（fish）

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



### Shell 和 Bash 的历史

Shell 伴随着 Unix 系统的诞生而诞生。

1969年，Ken Thompson 和 Dennis Ritchie 开发了第一版的 Unix。

1971年，Ken Thompson 编写了最初的 Shell，称为 Thompson shell，程序名是`sh`，方便用户使用 Unix。

1973年至1975年间，John R. Mashey 扩展了最初的 Thompson shell，添加了编程功能，使得 Shell 成为一种编程语言。这个版本的 Shell 称为 Mashey shell。

1976年，Stephen Bourne 结合 Mashey shell 的功能，重写一个新的 Shell，称为 Bourne shell。

1978年，加州大学伯克利分校的 Bill Joy 开发了 C shell，为 Shell 提供 C 语言的语法，程序名是`csh`。它是第一个真正替代`sh`的 UNIX shell，被合并到 Berkeley UNIX 的 2BSD 版本中。

1979年，UNIX 第七版发布，内置了 Bourne Shell，导致它成为 Unix 的默认 Shell。注意，Thompson shell、Mashey shell 和 Bourne shell 都是贝尔实验室的产品，程序名都是`sh`。对于用户来说，它们是同一个东西，只是底层代码不同而已。

1983年，David Korn 开发了Korn shell，程序名是`ksh`。

1985年，Richard Stallman 成立了自由软件基金会（FSF），由于 Shell 的版权属于贝尔公司，所以他决定写一个自由版权的、使用 GNU 许可证的 Shell 程序，避免 Unix 的版权争议。

1988年，自由软件基金会的第一个付薪程序员 Brian Fox 写了一个 Shell，功能基本上是 Bourne shell 的克隆，叫做 Bourne-Again SHell，简称 Bash，程序名为`bash`，任何人都可以免费使用。后来，它逐渐成为 Linux 系统的标准 Shell。

1989年，Bash 发布1.0版。

1996年，Bash 发布2.0版。

2004年，Bash 发布3.0版。

2009年，Bash 发布4.0版。

2019年，Bash 发布5.0版。

用户可以通过`bash`命令的`--version`参数或者环境变量`$BASH_VERSION`，查看本机的 Bash 版本。

```shell
sw:~ hwte$ bash --version
GNU bash, version 3.2.57(1)-release (arm64-apple-darwin22)
Copyright (C) 2007 Free Software Foundation, Inc.
sw:~ hwte$ echo $BASH_VERSION
3.2.57(1)-release
```



## Bash 简介

Bash 是 Unix 系统和 Linux 系统的一种 Shell（命令行环境），是目前绝大多数 Linux 发行版的默认 Shell .

⚠️注 : 当前系统的默认 Shell 已设置成 `bash`（原来为`zsh`，因为使用的是 MacOS），**即本笔记的实验环境 & 学习对象为 `bash`** : 

```shell
# 查看当前系统的默认 Shell
sw:~ hwte$ echo $SHELL
/bin/bash
# 查看当前系统的 bash 版本
sw:~ hwte$ bash --version
GNU bash, version 5.2.21(1)-release (aarch64-apple-darwin22.6.0)
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```



## Bash 下载 & 安装

下载链接（清华大学开源软件镜像站） : https://mirrors.tuna.tsinghua.edu.cn/gnu/bash/ 

在 MacOS 中的安装过程如下所示 : 

```shell
# 1.解压 .tar.gz 文件
tar -xzf bash-5.2.21.tar.gz

# 2.进入解压后的文件夹
cd bash-5.2.21

# 3.指定软件安装的根目录，即将软件安装在 /usr/local/ 目录下
# 注: 默认情况下，很多软件的安装路径为 /usr/local/
./configure --prefix=/usr/local

# 4.编译源代码
make

# 5.安装编译后的二进制文件
sudo make install
```

```shell
# 6.打开一个新的终端，查看当前系统中 bash 的版本
# 注: 因前面 bash-5.2.21 安装在了 /usr/local/ 目录下，即当前用户的目录下，
# 故 bash --version 优先会显示 /usr/local/bin/bash 的版本，而非 /bin/bash 的版本
sw:~ hwte$ bash --version
GNU bash, version 5.2.21(1)-release (aarch64-apple-darwin22.6.0)
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

# 7.进入 bash 专属的命令界面
# 注: 因前面 bash-5.2.21 安装在了 /usr/local/ 目录下，即当前用户的目录下，
# 故键入的 bash 命令优先会使用 /usr/local/bin/bash，而非 /bin/bash
sw:~ hwte$ bash
bash-5.2$ 
```

```shell
# 以下为扩展内容:

# 查看当前系统中已安装的 bash 命令的路径
sw:~ hwte$ which -a bash
/usr/local/bin/bash
/bin/bash

# 查看这两个 bash 命令各自的版本: 
# /usr/local/bin/bash --version
sw:~ hwte$ /usr/local/bin/bash --version
GNU bash, version 5.2.21(1)-release (aarch64-apple-darwin22.6.0)
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

# /bin/bash --version
sw:~ hwte$ /bin/bash --version
GNU bash, version 3.2.57(1)-release (arm64-apple-darwin22)
Copyright (C) 2007 Free Software Foundation, Inc.

# bash --version
# 注: 因前面 bash-5.2.21 安装在了 /usr/local/ 目录下，即当前用户的目录下，
# 故键入的 "bash --version" 命令优先会显示 /usr/local/bin/bash 的版本信息，而非 /bin/bash
sw:~ hwte$ bash --version
GNU bash, version 5.2.21(1)-release (aarch64-apple-darwin22.6.0)
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```



## 进入 & 退出 Bash

打开终端后，如果当前系统默认的 Shell 不是你想使用的类型，可以通过输入`<shell_name>`命令启用指定类型的 Shell .

```shell
# 查看当前系统默认的 Shell
hwte@sw ~ % echo $SHELL
/bin/zsh

# 启用 bash
# 注: 因前面 bash-5.2.21 安装在了 /usr/local/ 目录下，即当前用户的目录下，
# 故键入的 "chsh -s /bin/bash" 命令优先会使用 /usr/local/bin/bash，而非 /bin/bash
hwte@sw ~ %  
Changing shell for hwte.
Password for hwte: 
```

```shell
# 打开一个新的终端，然后再次查看当前系统默认的 Shell
sw:~ hwte$ echo $SHELL
/bin/bash

# 进入 bash 专属的命令界面（尽管现在当前系统默认的 Shell 就是 bash）
# 注: 在此界面学习 bash 编程更舒服一些哈～
sw:~ hwte$ bash
bash-5.2$ 

# 退出 bash 专属的命令界面（也可使用 Ctrl+d）
bash-5.2$ exit
exit
sw:~ hwte$ 
```



## 第一个 Bash 脚本

vim hello_shell.sh :  

注 : `#!`是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell，**若不加则使用当前系统默认的 Shell** .

```shell
#!/bin/bash
echo 'Hello Shell'
```



## 运行 Shell 脚本的方法

1. 作为可执行程序 :

   ⚠️注 : 一定要写成`./hello_shell.sh`，而不是`hello_shell.sh`，运行其它`二进制的程序`也一样，直接写`hello_shell.sh`，linux 系统会去 `PATH` 里寻找有没有叫 `hello_shell.sh` 的文件，而只有 `/bin`, `/sbin`,` /usr/bin`，`/usr/sbin` 等在 `PATH` 里，你的当前目录通常不在 `PATH` 里，所以写成 `hello_shell.sh` 是会找不到该文件的，要用 `./hello_shell.sh` 告诉系统说，就在当前目录找 .

   ```shell
   # 查看当前用户是否有执行 hello_shell.sh 的权限，发现无
   sw:~ hwte$ ls -l hello_shell.sh 
   -rw-r--r--  1 hwte  staff  31  7 18 10:35 hello_shell.sh
   # 使脚本具有执行权限
   sw:~ hwte$ chmod +x hello_shell.sh 
   # 执行脚本
   sw:~ hwte$ ./hello_shell.sh 
   Hello Shell
   ```

2. 作为解释器参数 : 

   注 : 这种运行方式是，直接运行解释器，其参数就是 Shell 脚本的文件名，**这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用** .

   ```shell
   sw:~ hwte$ cat hello_shell.sh 
   echo 'Hello Shell'
   sw:~ hwte$ /bin/bash hello_shell.sh 
   Hello Shell
   sw:~ hwte$ /bin/zsh hello_shell.sh 
   Hello Shell
   ```



## Bash 注释

1. 单行注释 : 

   ```shell
   # echo function be used to print something to console
   echo 'Hello Shell'
   ```

2. 多行注释 :  

   ```shell
   # 注释内容...
   # 注释内容...
   # 注释内容...
   echo 'Hello Shell'
   ```
   
   ```shell
   : '
   注: 冒号`:`是一个空命令，这些内容不会被执行
   注释内容...
   注释内容...
   '
   echo 'Hello Shell'
   ```
   
   

## Bash 变量

### 命名规范

* 只包含字母、数字和下划线
* 为变量赋值的**等号两侧**避免使用空格
* . . . 更多详情请参考 Python3 的命令规范哈，类似的～



### 使用 & 删除变量

1. **变量的使用** : 使用一个定义过的变量，只要在变量名前面加美元符号`$`即可，变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的**边界**，**推荐给所有变量加上花括号，这是个好的编程习惯～**

   ```shell
   bash-3.2$ name='googtech'
   bash-3.2$ echo ${name}
   googtech
   ```

2. **只读变量** : 使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变，**类似于 Python 中的常量** : 

   ```shell
   bash-3.2$ join_us='https://hackorg.com'
   bash-3.2$ readonly join_us
   bash-3.2$ join_us='...'
   bash: join_us: readonly variable
   ```

3. **删除变量** : 变量被删除后不能再次使用，unset 命令不能删除只读变量

   ```shell
   # 尝试删除只读变量
   bash-3.2$ join_us='https://hackorg.com'
   bash-3.2$ unset join_us
   bash: unset: join_us: cannot unset: readonly variabl
   
   # 尝试删除普通变量，变量被删除后，`echo ${name}`将打印空值
   bash-3.2$ name='hack'
   bash-3.2$ unset name
   bash-3.2$ echo ${name}
   
   ```



### 变量类型

在 Shell 脚本中，变量通常没有类型声明，即它们是**动态类型**，这意味着你不需要明确指定变量是整数、字符串还是其他类型 .

#### 整数变量

可以使用`declare -i`命令来声明将变量作为一个整数处理，需要注意的是，**此命令在赋值时会自动将非整数转换为整数** .

```shell
# 尝试赋值一个`整数`
bash-3.2$ declare -i year=2024
bash-3.2$ echo ${year}
2024

# 尝试赋值一个`浮点数`
bash-3.2$ declare -i price=6.66
bash: declare: 6.66: syntax error: invalid arithmetic operator (error token is ".66")

# 尝试赋值一个`字符串`
bash-3.2$ declare -i var='hello'
bash-3.2$ echo ${var}
0

# 尝试赋值一个`整数类型的数组`
bash-3.2$ declare -i var=(3 2 1)
bash-3.2$ echo ${var}
3

# 尝试赋值一个`浮点类型的数组`
bash-3.2$ declare -i var=(1.01 2.01 3.01)
bash: 1.01: syntax error: invalid arithmetic operator (error token is ".01")

# 尝试赋值一个`字符串类型的数组`
bash-3.2$ declare -i var=('abc' 'bac' 'cab')
bash-3.2$ echo ${var}
0
```



#### 字符串变量

在 Shell中，变量通常被视为字符串，可以使用单引号`'`或双引号`"`来定义字符串 : 

```shell
bash-3.2$ programming_language='Shell'
bash-3.2$ str="Hello '${programming_language}'"
bash-3.2$ echo ${str}
Hello 'Shell'
```

注 : 使用单引号`'`时容易错的点，即**单引号中不可以出现转义字符** : 

```shell
bash-3.2$ programming_language='Shell'
bash-3.2$ str='Hello ${programming_language} \n'
bash-3.2$ echo ${str}
Hello ${programming_language} \n
```

##### 操作字符串的常用函数

1. 获取字符串长度，注 : 变量为字符串时，`${#string}`等价于`${#string[0]}` : 

   ```shell
   bash-3.2$ str='hello shell & 2024'
   bash-3.2$ echo ${#str}
   18
   bash-3.2$ echo ${#str[0]}
   18
   ```

2. 提取字符串，注 : 第一个字符的索引值为 `0` : 

   ```shell
   bash-3.2$ str='hello shell & 2024'
   bash-3.2$ echo ${str:14:17}
   2024
   ```

   

#### 数组变量

bash支持一维数组（不支持多维数组），并且没有限定数组的大小，数组元素的下标由 0 开始 .

##### 普通数组

1. 定义数组 : 在 Shell 中，用括号来表示数组，数组元素用 "空格" 符号分割开 .

   ```shell
   # 定义整数类型的数组
   bash-3.2$ arr=(2 0 2 4)
   bash-3.2$ echo ${arr}
   2
   # 定义浮点类型的数组
   bash-3.2$ arr=(6.66 8.88 9.99)
   bash-3.2$ echo ${arr}
   6.66
   # 定义字符串类型的数组（两种格式均可）
   bash-3.2$ arr=(python3 bash 2024)
   bash-3.2$ echo ${arr}
   python3
   bash-3.2$ arr=('python3' 'shell' '2024')
   bash-3.2$ echo ${arr}
   python3
   ```

2. 为指定数组下标赋值 : 

   ```shell
   # 示例一
   bash-3.2$ arr=()
   bash-3.2$ arr[0]='hello'
   bash-3.2$ arr[2]='shell'
   bash-3.2$ echo ${arr[0]} ${arr[2]}
   hello shell
   # 示例二
   bash-3.2$ arr=('python3' 'bash' '2024')
   bash-3.2$ arr[1]='shell'
   bash-3.2$ echo ${arr[1]}
   shell
   ```

3. 获取数组中的元素 : 

   ```shell
   # 获取数组中指定下标的元素
   bash-3.2$ arr=('python3' 'shell' '2024')
   bash-3.2$ echo ${arr[2]}
   2024
   # 获取数组中的所有元素
   bash-3.2$ echo ${arr[@]}
   python3 bash 2024
   ```

4. 获取数组的长度 : 

   ```shell
   # 获取数组中指定下标元素的长度
   bash-3.2$ echo ${#arr[0]}
   7
   # 获取数组的长度（两种方法均可）
   bash-3.2$ echo ${#arr[@]}
   3
   bash-3.2$ echo ${#arr[*]}
   3
   ```

5. 遍历数组 : 

   ```shell
   arr=('python3' 'shell' '2024')
   
   # emmm...其语法和 Lua 非常相似!!!
   for element in ${arr[@]}; do
   	echo ${element}
   done
   ```

   ```shell
   bash-3.2$ ./test.sh
   python3
   shell
   2024
   ```

##### 关联数组（字典）

Bash 支持关联数组，可以使用任意的字符串、或者整数作为下标来访问数组元素 .

注 : `-A`选项用于声明一个关联数组，关联数组的键是唯一的 .

1. 定义字典 : 

   ```shell
   bash-5.2$ declare -A site_dict
   # 当然，我们也可以在创建字典的同时，为其赋予不同的键值对，例如:
   # declare -A site_dict=(["about_me"]="goog.tech" ["join_us"]="hackorg.com")
   ```

2. 向字典中添加键值对（key-value） : 

   ```shell
   bash-5.2$ site_dict['about_me']='goog.tech'
   bash-5.2$ site_dict['join_us']='hackorg.com'
   ```

3. 获取字典中的值（value） : 

   ```shell
   # 获取指定键的值
   bash-5.2$ echo ${site_dict['about_me']}
   goog.tech
   bash-5.2$ echo ${site_dict['join_us']}
   hackorg.com
   # 获取全部值的两种方法
   bash-5.2$ echo ${site_dict[*]}
   goog.tech hackorg.com
   bash-5.2$ echo ${site_dict[@]}
   goog.tech hackorg.com
   ```

4. 更新字典中的值（value）: 

   ```shell
   bash-5.2$ site_dict['join_us']='HackOrg.com'
   bash-5.2$ echo ${site_dict['join_us']}
   HackOrg.com
   ```

5. 获取字典中的键 : 

   ```shell
   # 获取全部键的两种方法
   bash-5.2$ echo ${!site_dict[*]}
   about_me join_us
   bash-5.2$ echo ${!site_dict[@]}
   about_me join_us
   ```

6. 删除字典中指定键的值 : 

   ```shell
   bash-5.2$ unset site_dict['join_us']
   bash-5.2$ echo ${site_dict[*]}
   goog.tech
   ```

7. 获取字典的长度 : 

   ```shell
   # 获取字典长度的两种方法
   bash-5.2$ echo ${#site_dict[*]}
   1
   bash-5.2$ echo ${#site_dict[@]}
   1
   ```

8. 遍历字典 : 

   ```shell
   declare -A site_dict=(['about_me']='goog.tech' ['join_us']='hackorg.com')
   
   for key in ${!site_dict[*]}; do
   	echo "${key} : ${site_dict[${key}]}"
   done
   ```

   ```shell
   bash-5.2$ ./test.sh 
   about_me : goog.tech
   join_us : hackorg.com
   ```

   

#### 环境变量

这些是由操作系统或用户设置的特殊变量，用于配置 Shell 的行为和影响其执行环境，例如 : 

* `PATH` 环境变量 : 存储着操作系统搜索可执行文件的路径
* `LANG`环境变量 : 存储着当前操作系统的语言类型
* `USER`环境变量 : 存储着当前用户的用户名

```shell
bash-3.2$ echo ${PATH}
/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/VMware Fusion.app/Contents/Public:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin

bash-3.2$ echo ${LANG}
zh_CN.UTF-8

bash-3.2$ echo ${USER}
hwte
```



#### 特殊变量

常用于向 Shell 脚本传递参数 .

* `$0`：表示脚本的名称
* `$1`, `$2`, ...：表示传递给脚本的参数，`$1`是第一个参数，`$2`是第二个参数，以此类推
* `$#`：表示传递给脚本的参数个数
* `$*`：表示所有参数的字符串，每个参数之间用空格分隔
* `$@`：表示所有参数的列表，每个参数可作为单独的字符串
* `$?`：表示上一个命令的退出状态，0表示没有错误，其他任何值表明有错误
* `$!`：表示上一个后台命令的进程ID
* `$$`：表示当前 Shell 进程的进程ID

用法示例 : 

```shell
# test.sh

echo "this file name: $0"
echo "arg_1: $1"
echo "arg_2: $2"
echo "args count: $#"
echo "all args in string: $*"
echo "all args in array:"
for arg in $@; do
	echo ${arg}
done
echo "previous shell's exit status: $?"
echo "previous shell's process ID: $!"
echo "current shell's process ID: $$"
```

程序运行结果 : 

```shell
bash-3.2$ ./test.sh arg1 arg2
this file name: ./test.sh
arg_1: arg1
arg_2: arg2
args count: 2
all args in string: arg1 arg2
all args in array:
arg1
arg2
previous shell's exit status: 0
previous shell's process ID: 
current shell's process ID: 62458
```



## Bash 基本运算符

### expr

`expr` 是一款表达式计算工具，使用它能完成表达式的求值操作，但有两点要特别注意 : 

* ⚠️表达式和运算符之间要有**空格**，例如 2+2 是不对的，必须写成 2 + 2
* ⚠️完整的表达式要被 **``** 包含，注意这个字符不是常用的单引号，而是反引号
* ⭐️在 MacOS 中 Shell 的 expr 语法是 : `$((表达式))`，此处表达式中的 `*` 不需要转义符号 `\`

```shell
# 表达式和运算符之间要有**空格**，例如 2+2 是不对的，必须写成 2 + 2
bash-5.2$ result=`expr 1+2`
bash-5.2$ echo ${result}
1+2
# 完整的表达式要被 **``** 包含，注意这个字符不是常用的单引号，而是反引号
bash-5.2$ result='expr 1 + 2'
bash-5.2$ echo ${result}
expr 1 + 2
# 在 MacOS 中 Shell 的 expr 语法是 : `$((表达式))`，此处表达式中的 `*` 不需要转义符号 `\`
bash-5.2$ result=$((1+2))
bash-5.2$ echo ${result}
3
# 标准正确写法
bash-5.2$ result=`expr 1 + 2`
bash-5.2$ echo ${result}
3
```

### 算术运算符

假定变量 a 为 10，变量 b 为 20 : 

| 运算符 | 说明                                              | 举例                        |
| :----- | :------------------------------------------------ | :-------------------------- |
| `+`    | 加法                                              | `expr $a + $b` 结果为 30    |
| `-`    | 减法                                              | `expr $a - $b` 结果为 -10   |
| `*`    | 乘法                                              | `expr $a \* $b` 结果为  200 |
| `/`    | 除法                                              | `expr $b / $a` 结果为 2     |
| `%`    | 取余                                              | `expr $b % $a` 结果为 0     |
| `=`    | 赋值                                              | a=$b 把变量 b 的值赋给 a    |
| `==`   | 相等，用于比较两个**数字**，相同则返回 true。     | [ $a == $b ] 返回 false     |
| `!=`   | 不相等，用于比较两个**数字**，不相同则返回 true。 | [ $a != $b ] 返回 true      |

⚠️注1 : 条件表达式要放在方括号之间，**并且要有空格**，例如 : `[$a==$b]` 是错误的，必须写成 `[ $a == $b ]` .

⚠️注2 : 在 Bash 中，`[]` 的使用场景如下 : 

* 用于`字符集匹配`，例如`[a-z]`匹配任何小写字母
* 用于`数组定义`，例如使用`[]`来定义和访问数组
* 用于`条件测试`，例如下面代码中的 if 判断

```shell
# test.sh
a=10
b=20

val=`expr $a + $b`
echo "$a + $b : $val"

val=`expr $a - $b`
echo "$a - $b : $val"

val=`expr $a \* $b`
echo "$a * $b : $val"

val=`expr $b / $a`
echo "$b / $a : $val"

val=`expr $b % $a`
echo "$b % $a : $val"

temp_var=$val
echo "temp_var($b % $a) : $temp_var"

if [ $a == $b ]
then
   echo "$a == $b"
fi

if [ $a != $b ]
then
   echo "$a != $b"
fi
```

```shell
bash-5.2$ ./test.sh 
10 + 20 : 30
10 - 20 : -10
10 * 20 : 200
20 / 10 : 2
20 % 10 : 0
temp_var(20 % 10) : 0
10 != 20
```

⚠️**如你所见，使用 `expr` 进行算数运算的代码看起来很蠢，推荐使用 `$(())` : 用于执行算术运算，它允许在 Bash 脚本中进行数学计算，下面利用 `$(())` 来重写上述蠢代码** : 

```shell
a=10
b=20

val=$(($a + $b))
echo "$a + $b : $val"

val=$(($a - $b))
echo "$a - $b : $val"

val=$(($a * $b))
echo "$a * $b : $val"

val=$(($b / $a))
echo "$b / $a : $val"

val=$(($b % $a))
echo "$b % $a : $val"

temp_var=$val
echo "temp_var($b % $a) : $temp_var"

if [ $a == $b ]
then
   echo "$a == $b"
fi

if [ $a != $b ]
then
   echo "$a != $b"
fi
```

```shell
bash-5.2$ ./test.sh 
10 + 20 : 30
10 - 20 : -10
10 * 20 : 200
20 / 10 : 2
20 % 10 : 0
temp_var(20 % 10) : 0
10 != 20
```



### 关系运算符

关系运算符只支持数字，不支持字符串，除非字符串的值是数字 .

⚠️注 : 如果使用 `((...))` 作为判断语句，大于、小于、大于等于、小于等于可以直接使用 `>`、`<`、`>=`、`<=` .

假定变量 a 为 10，变量 b 为 20 : 

| 运算符 | 说明                           | 举例                     |
| :----- | :----------------------------- | :----------------------- |
| `-eq`  | 检测两个数是否相等             | [ $a -eq $b ] 返回 false |
| `-ne`  | 检测两个数是否不相等           | [ $a -ne $b ] 返回 true  |
| `-gt`  | 检测左边的数是否大于右边的     | [ $a -gt $b ] 返回 false |
| `-lt`  | 检测左边的数是否小于右边的     | [ $a -lt $b ] 返回 true  |
| `-ge`  | 检测左边的数是否大于等于右边的 | [ $a -ge $b ] 返回 false |
| `-le`  | 检测左边的数是否小于等于右边的 | [ $a -le $b ] 返回 true  |

```shell
# test.sh
a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : true"
else
   echo "$a -eq $b : false"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b : true"
else
   echo "$a -ne $b : false"
fi
if [ $a -gt $b ]
then
   echo "$a -gt $b : true"
else
   echo "$a -gt $b : false"
fi
if [ $a -lt $b ]
then
   echo "$a -lt $b : true"
else
   echo "$a -lt $b : false"
fi
if [ $a -ge $b ]
then
   echo "$a -ge $b : true"
else
   echo "$a -ge $b : false"
fi
if [ $a -le $b ]
then
   echo "$a -le $b : true"
else
   echo "$a -le $b : false"
fi
```

```shell
bash-5.2$ ./test.sh 
10 -eq 20 : false
10 -ne 20 : true
10 -gt 20 : false
10 -lt 20 : true
10 -ge 20 : false
10 -le 20 : true
```

⚠️ 如果使用 `((...))` 作为判断语句，大于、小于、大于等于、小于等于可以直接使用 `>`、`<`、`<=`、`>=` :  

```shell
# test.sh
a=10
b=20

if (($a == $b))
then
   echo "$a == $b : true"
else
   echo "$a == $b : false"
fi
if (($a != $b))
then
   echo "$a != $b : true"
else
   echo "$a != $b : false"
fi
if (($a > $b))
then
   echo "$a > $b : true"
else
   echo "$a > $b : false"
fi
if (($a < $b))
then
   echo "$a < $b : true"
else
   echo "$a < $b : false"
fi
if (($a >= $b))
then
   echo "$a >= $b : true"
else
   echo "$a >= $b : false"
fi
if (($a <= $b))
then
   echo "$a <= $b : true"
else
   echo "$a <= $b : false"
fi
```

```shell
bash-5.2$ ./test.sh 
10 == 20 : false
10 != 20 : true
10 > 20 : false
10 < 20 : true
10 >= 20 : false
10 <= 20 : true
```



### 逻辑运算符

假定变量 a 为 10，变量 b 为 20 : 

| 运算符 | 说明       | 举例                                       |
| :----- | :--------- | :----------------------------------------- |
| `&&`   | 逻辑的 AND | [[ $a -lt 100 && $b -gt 100 ]] 返回 false  |
| `||`   | 逻辑的 OR  | [[ $a -lt 100 \|\| $b -gt 100 ]] 返回 true |

```shell
# test.sh

a=10
b=20

if [[ $a -lt 100 && $b -gt 100 ]] then
	echo "true"
else
	echo "false"
fi

if [[ $a -lt 100 || $b -gt 100 ]] then
	echo "true"
else
	echo "false"
fi
```

```shell
bash-5.2$ ./test.sh 
false
true
```

### 字符串运算符

假定变量 `about_me` 为 "goog.tech"，变量 `join_us` 为 "hackorg.com" : 

| 运算符 | 说明                     | 举例                   |
| :----- | :----------------------- | :--------------------- |
| `=`    | 检测两个字符串是否相等   | [ $a = $b ] 返回 false |
| `!=`   | 检测两个字符串是否不相等 | [ $a != $b ] 返回 true |
| `-z`   | 检测字符串长度是否为 0   | [ -z $a ] 返回 false   |
| `-n`   | 检测字符串长度是否不为 0 | [ -n "$a" ] 返回 true  |
| `$`    | 检测字符串是否不为空     | [ $a ] 返回 true       |

```shell
# test.sh

a="goog.tech"
b="hackorg.com"

if [ $a = $b ]
then
   echo "a == b"
else
   echo "a != b"
fi

if [ $a != $b ]
then
   echo "a != b"
else
   echo "a == b"
fi

if [ -z $a ]
then
   echo "the length of a is 0"
else
   echo "the length of a isn't 0"
fi

if [ -n "$a" ]
then
   echo "the length of a isn't 0"
else
   echo "the length of a is 0"
fi

if [ $a ]
then
   echo "the string of a isn't NULL"
else
   echo "the string of a is NULL"
fi
```

```shell
bash-5.2$ ./test.sh 
a != b
a != b
the length of a isn't 0
the length of a isn't 0
the string of a isn't NULL
```

### 文件测试运算符

文件测试运算符用于检测 Unix 文件的各种属性 .

* `-b file` : 检测文件是否是**块设备文件**
* `-c file` : 检测文件是否是**字符设备文件**
* `-d file` : 检测文件是否是**目录**
* `-f file` : 检测文件是否是**普通文件**（既不是目录，也不是设备文件）
* `-g file` : 检测文件是否设置了 **SGID 位**
* `-k file` : 检测文件是否设置了**粘着位（Sticky Bit）**
* `-p file` : 检测文件是否是有名**管道**
* `-u file` : 检测文件是否设置了 **SUID 位**
* `-r file` : 检测文件是否**可读**
* `-w file` : 检测文件是否**可写**
* `-x file` : 检测文件是否**可执行**
* `-s file` : 检测文件是否**不为空**（文件大小是否大于0）
* `-e file` : 检测文件（包括目录）是否**存在**
* `-S file` : 判断某文件是否是 **socket文件**
* `-L file` : 检测文件是否存在并且是一个**符号链接**

test.sh 文件内容 : 

```shell
# 检测文件名是否作为参数传递
if [ $# -eq 0 ]; then
    echo "请提供一个文件名作为参数"
    exit 1
fi

# 接收参数,即文件名
file="$1"

# 检测文件的各种属性
if [ -b "$file" ]; then echo "$file 是块设备文件"; fi
if [ -c "$file" ]; then echo "$file 是字符设备文件"; fi
if [ -d "$file" ]; then echo "$file 是目录"; fi
if [ -f "$file" ]; then echo "$file 是普通文件"; fi
if [ -g "$file" ]; then echo "$file 设置了SGID位"; fi
if [ -k "$file" ]; then echo "$file 设置了粘着位"; fi
if [ -p "$file" ]; then echo "$file 是有名管道"; fi
if [ -u "$file" ]; then echo "$file 设置了SUID位"; fi
if [ -r "$file" ]; then echo "$file 可读"; fi
if [ -w "$file" ]; then echo "$file 可写"; fi
if [ -x "$file" ]; then echo "$file 可执行"; fi
if [ -s "$file" ]; then echo "$file 不为空"; fi
if [ -e "$file" ]; then echo "$file 存在"; fi
if [ -S "$file" ]; then echo "$file 是Socket文件"; fi
if [ -L "$file" ]; then echo "$file 是符号链接"; fi
```

运行 test.sh 脚本 : 

```shell
bash-5.2$ ./test.sh test.file 
test.file 是普通文件
test.file 可读
test.file 可写
test.file 不为空
test.file 存在
```

### 自增和自减操作符

尽管 Shell 本身没有像 C++ 或 Java 那样的 `++` 和 `--` 操作符，但可以通过其他方式实现相同的功能 : 

1. 使用 `let` 命令 : 此命令允许对整数进行算术运算 .

   ```shell
   bash-5.2$ year=2024
   bash-5.2$ let year++
   bash-5.2$ echo ${year}
   2025
   ```

2. 使用 `$(())` 进行算术运算 : `$(( ))`语法也是进行算术运算的一种方式 .

   ```shell
   bash-5.2$ year=2024
   bash-5.2$ year=$((2024 + 1))
   bash-5.2$ echo ${year}
   2025
   ```

   

## Bash 常用命令

### echo 命令

`echo` 命令用于简单地输出文本和变量 .

#### 显示变量

```shell
bash-5.2$ about_me='goog.tech'
bash-5.2$ echo ${about_me}
goog.tech
bash-5.2$ echo $about_me
goog.tech
```

#### 区分单与双引号

- 双引号 : 允许`变量`替换和`命令`替换
- **单引号 : 所有内容原样输出，不进行`变量`替换或`命令`替换**

```shell
bash-5.2$ about_me='goog.tech'
# 双引号
bash-5.2$ echo "webiste: ${about_me}"
webiste: goog.tech
bash-5.2$ echo "date: `date`"
date: Fri Jul 19 11:39:10 CST 2024
bash-5.2$ echo "date: $(date)"
date: Fri Jul 19 11:39:17 CST 2024
# 单引号
bash-5.2$ echo 'webiste: ${about_me}'
webiste: ${about_me}
bash-5.2$ echo 'date: `date`'
date: `date`
bash-5.2$ echo 'date: $(date)'
date: $(date)
```

#### 显示普通 / 转义字符

```shell
# 显示普通字符串
bash-5.2$ echo "hello 2024"
hello 2024
bash-5.2$ echo hello 2024
hello 2024
# 显示转义字符
bash-5.2$ echo "\"hello 2024\""
"hello 2024"
bash-5.2$ echo \"hello 2024\"
"hello 2024"
```

#### 显示换行 / 不换行

换行 : 

```shell
bash-5.2$ echo -e "hello 2024\nhello bash"
hello 2024
hello bash
```

不换行 : 

```shell
# test.sh
echo -e "hello 2024 \c"
echo "hello bash"
```

```shell
bash-5.2$ ./test.sh 
hello 2024 hello bash
```

#### 显示命令执行结果

注 : 这里使用的是反引号 **`**，而不是单引号 **'** .

```shell
# 方式一 :  
bash-5.2$ echo `pwd`
/Users/hwt
bash-5.2$ echo `date`
Fri Jul 19 11:22:43 CST 2024
# 方式二 : 
bash-5.2$ echo $(pwd)
/Users/hwte
bash-5.2$ echo $(date)
Fri Jul 19 11:32:59 CST 2024
```

#### 将显示结果写入文件

直接写入文件（会覆盖原文件内容） : 

```shell 
bash-5.2$ cat test.file 
hello 2024
bash-5.2$ echo 'hello bash' > test.file 
bash-5.2$ cat test.file 
hello bash
```

追加写入文件（会写入到原文件内容尾部） : 

```shell
bash-5.2$ cat test.file 
hello bash
bash-5.2$ echo 'hello 2024' >> test.file 
bash-5.2$ cat test.file 
hello bash
hello 2024
```

### printf 命令

`printf` 命令提供了更强大的格式化输出能力，类似于 C 语言中的 `printf` 函数。它支持更多的转义序列，并且可以精确控制输出的格式，如对齐、宽度和精度 .

`printf` 命令的语法如下 :

```shell 
# format-string : 一个格式字符串，它包含普通文本和格式说明符
# arguments : 用于填充格式说明符的参数列表
printf  format-string  [arguments...]
```

#### 对比 echo

* **格式化** : `printf` 支持更复杂的格式化选项，如 `%s`、`%-10s` 等，而 `echo` 的格式化能力较弱
* **转义字符** : `printf` 更可靠地处理转义字符，而 `echo` 在某些 shell 中可能不完全支持所有转义序列
* **变量引用** : `printf` 需要使用额外的参数来引用变量，而 `echo` 可以直接在字符串中引用变量
* **安全性** : 在某些情况下，`printf` 可能更安全，因为它不自动展开变量，这可以防止某些类型的注入攻击

对于简单的文本输出，`echo` 可能就足够了，但是，如果你需要更复杂的格式化或更可靠的转义字符处理，`printf` 是更好的选择 .

#### 格式说明

- `%s`：输出字符串，注 : 若没有给 arguments，则输出空值
- `%d` 或 `%i`：输出整数，注 : 若没有给 arguments，则输出 0
- `%.nf`：输出浮点数，`n`表示小数点后保留的位数
- `%c`：输出单个字符
- `%b`：输出八进制数
- `%x` 或 `%X`：输出十六进制数，小写或大写
- `%%`：输出百分号`%`
- `%e`：输出科学计数法表示的浮点数

注 : `%-Ns`指一个宽度为 N 个字符（`-`表示左对齐，没有则表示右对齐）

```shell
# test.sh
printf "%-10s %-8s %-4s\n"   NAME SEX WEIGHT  
printf "%-10s %-8s %-4.2f\n" abc  f   50.123
printf "%-10s %-8s %-4.2f\n" bac  f   50.213
printf "%-10s %-8s %-4.2f\n" cab  f   50.312
```

```shell
bash-5.2$ ./test.sh 
NAME       SEX      WEIGHT
abc        f        50.12
bac        f        50.21
cab        f        50.31
```

#### 转义序列

- `\a`：发出警告声
- `\b`：退格
- `\f`：换页
- `\n`：换行
- `\r`：回车
- `\t`：水平制表符
- `\v`：垂直制表符
- `\\`：反斜杠
- `\0nnn`：八进制字符（其中`n`是数字）
- `\xHH`：十六进制字符（其中`H`是十六进制数字）

### test 命令

在 Bash 中，`test`命令是一个非常强大的工具，用于测试文件属性、比较数字、检查字符串等，它通常用于条件语句中，如`if`语句，以决定程序的流程控制，`test`命令的语法是`[ expression ]`或`[[ expression ]]`，其中`expression`可以是**文件测试**、**字符串测试**或**数值测试** .

区分`[ expression ]`与`[[ expression ]]` : 

* `[ expression ]` 和 `[[ expression ]]` 都需要在符号（ [ 与 ] ）与参数之间加**空格**，例如 `[ "$1" = "$2" ]`
* `[ expression ]`不支持逻辑运算符`&&`和`||`，而`[[ expression ]]`支持
* `[[ expression ]]` 支持更复杂的表达式，如正则表达式和更安全的字符串比较

**综上，可知`[[`提供了更强大和更安全的字符串处理能力，因此在大多数情况下，推荐使用`[[`进行条件判断** .

#### [ expression ]

```shell
# test.sh

# 数值测试
if [ "$1" -eq 10 ]; then
	echo "$1 == 10"
else
	echo "$1 != 10"
fi
# 文件测试
if [ -f "$2" ]; then
	echo "$2 is exists"
else
	echo "$2 isn't exists"
fi
```

```shell
bash-5.2$ ./test.sh 2024 test.file
2024 != 10
test.file is exists
```

#### [[ expression ]]

注 : 在 Bash 中，`=~` 操作符用于字符串模式匹配，它用于检查一个字符串是否匹配给定的正则表达式 .

```shell
# test.sh

# 数值测试（使用正则表达式）
if [[ "$1" =~ ^[0-9]+$ ]]; then
	echo "$1 is number"
else
	echo "$1 isn't number"
fi
# 数值测试 && 文件测试（使用逻辑运算符 &&）
if [[ "$1" -gt 100 && -f "$2" ]]; then
	echo "$1 > 100 and $2 is exists"
else
	echo "$1 <= 100 or $2 isn't exists"
fi
```

```shell
bash-5.2$ ./test.sh 2024 test.file
2024 is number
2024 > 100 and test.file is exists
```



## Bash 控制流程

### if

```shell
# test.sh
if [ "$1" -eq 2024 ]; then
	echo "$1 equal with 2024"
fi

# 当然，也可以写成一行
if [ "$1" -eq 2024 ]; then echo "$1 equal with 2024"; fi
```

```shell
bash-5.2$ ./test.sh 2024
2024 equal with 2024
2024 equal with 2024
```

### if else

```shell
# test.sh
if [ "$1" -eq 2024 ]; then
	echo "$1 is equal with 2024"
else
	echo "$1 isn't equal with 2024"
fi
```

```shell
bash-5.2$ ./test.sh 2025
2025 isn't equal with 2024
```

### if else-if else

```shell
# test.sh
if [ "$1" -eq 2024 ]; then
	echo "$1 is equal with 2024"
elif [ "$1" -eq 2025 ]; then
	echo "$1 is equal with 2025"
else
	echo "$1 isn't equal with 2024 or 2025"
fi
bash-5.2$ ./test.sh 2025
2025 is equal with 2025
```

```shell
bash-5.2$ ./test.sh 2025
2025 is equal with 2025
```

### for

```shell
# test.sh
# 遍历指定的数字/字符
for i in 1 2 3; do
	printf $i
done
printf '\n'
for i in 'a' 'b' 'c'; do
	printf $i
done
printf '\n\n'

# 遍历指定范围的数字/字符
for i in {1..3}; do
    printf $i
done
printf '\n'
for i in {a..c}; do
    printf $i
done
printf '\n\n'

# 遍历数组中的元素
arr=('python3' 'shell' '2024')
for element in ${arr[@]}; do
	printf "${element}\n"
done
printf '\n'

# 遍历字典中的元素
declare -A site_dict=(['about_me']='goog.tech' ['join_us']='hackorg.com')
for key in ${!site_dict[*]}; do
	printf "${key} : ${site_dict[${key}]}\n"
done
```

```shell
bash-5.2$ ./test.sh 
123
abc

123
abc

python3
shell
2024

about_me : goog.tech
join_us : hackorg.com
```

### while

```shell
# test.sh
i=1
while [ $i -le 3 ]; do
	echo $i
	let i++
done
```

```shell
bash-5.2$ ./test.sh
1
2
3
```

### until

until 循环执行一系列命令直至条件为 true 时停止，其处理方式刚好与 while 循环相反 .

```shell
# test.sh
i=1
# 注: 当条件为假时持续执行
until [ $i -gt 3 ]; do
	echo $i
	let i++
done
```

```shell
bash-5.2$ ./test.sh 
1
2
3
```

### case ... esac

`case ... esac`为多选择语句，与其它语言中的 `switch ... case` 语句类似，是一种多分支选择结构，每个 case 分支用右圆括号开始，用两个分号 `;;` 表示 break .

```shell
# test.sh
value=2
case $value in
	1)
		echo "value == 1"
		;;
	2)
		echo "value == 2"
		;;
	*)
		echo "value !=1 and !=2"
		;;
esac
```

```shell
bash-5.2$ ./test.sh
value == 2
```

### break

`break` 命令允许跳出所有循环（终止执行后面的所有循环）.

```shell
# test.sh
# 在循环中使用 break 语句提前退出循环
for i in {1..10}; do
    if [ $i -eq 4 ]; then
        break
    fi
    echo "number: $i"
done
```

```shell
bash-5.2$ ./test.sh 
number: 1
number: 2
number: 3
```

### continue

`continue` 命令与 `break` 命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环 .

```shell
# test.sh
# 在循环中使用 continue 语句跳过当前迭代
for i in {1..6}; do
    if [ $((i % 2)) -eq 0 ]; then
        continue
    fi
    echo "number: $i"
done
```

```shell
bash-5.2$ ./test.sh 
number: 1
number: 3
number: 5
```



## Bash 函数

### 函数定义

```shell
function_name() {
		# 接收参数: var_1=$1,var_2=$2,...var_3=$n
    # 函数内容: 可以写任何合法的 Bash 命令
    # 返回结果: echo 需返回的结果
}
```

### 函数调用 

通过函数名即可调用函数 : 

```shell
bash-5.2$ greet() { echo "Hello 2024"; }
bash-5.2$ greet
Hello 2024
```

### 局部变量 

在函数内部，可以使用`local`关键字来声明局部变量，这些变量只在函数内部有效 : 

```shell
bash-5.2$ greet() { local year=2024; echo "Hello ${year}"; }
bash-5.2$ greet
Hello 2024
bash-5.2$ echo ${year} # 输出空值

```

### 参数传递 

函数可以接受任意数量的参数，这些参数可以通过`$1`, `$2`, `$3`, ...来访问 : 

```shell
bash-5.2$ add() { local cal_result=$(($1+$2)); echo $cal_result;  }
bash-5.2$ add 1 2
3
```

### 返回值 

可以通过`echo`输出结果，然后在调用函数时使用命令替换`$(command)`来捕获这个输出 : 

```shell
bash-5.2$ add() { local cal_result=$(($1+$2)); echo $cal_result;  }
bash-5.2$ echo $(add 1 2)
3
```

### 示例程序

```shell 
# test.sh
# 定义一个用于输出问候语的函数
greet() {
	echo "Hello, $1"
}

# 定义一个用于计算两数之和的函数
add() {
	local cal_result=$(( $1 + $2 ))
	echo $cal_result
}

# 调用函数 greet() 并传入参数 "Bash"
greet "Bash"

# 调用函数 add() 并传入参数 1 与 2
add_res=$(add 1 2)

# 输出计算结果
echo "The sum is: $(add 1 2)"
echo "The sum is: $add_res"
```

```shell
bash-5.2$ ./test.sh 
Hello, Bash
The sum is: 3
The sum is: 3
```



## Bash I/O重定向

. . .



## Bash 文件包含

. . .



## 扩展 : 易混淆的点

### ⭐️区分`[]`,`[[]]`,`()`,`(())`,`$()`,`$(())`

* `[]` : 用于条件测试，**它是`test`命令的简化形式**，通常用于条件语句中，它实际上是一个命令，用于比较字符串或数值，以及检查文件属性 : 

  ```shell
  if [ "$1" -gt "2024" ]; then
  	echo "$1 > 2024"
  fi
  ```

  ```shell
  bash-5.2$ ./test.sh 2025
  2025 > 2024
  ```

* `[[]]` 是 `[]` 的扩展版本 : 支持更复杂的表达式，如正则表达式和更安全的字符串比较 :  

  ```shell
  if [[ $1 =~ ^[0-9]+$ ]]; then
  	echo "$1 is a number"
  fi
  ```

  ```shell
  bash-5.2$ ./test.sh 2024
  2024 is a number
  ```

* `()` : 用于`子shell`，可以在其中执行一组命令，这些命令在**新的**进程环境中运行，不会影响父环境 : 

  ```shell
  # 子shell
  (
  cd ~/folder # 进入用户目录下的 folder 目录
  pwd         # 查看当前目录的路径
  ls          # 查看当前目录下的文件及文件夹
  )
  # 父shell
  printf "\n$(pwd)\n" # 查看当前目录的路径
  ```

  ```shell
  bash-5.2$ ./test.sh 
  /Users/hwte/folder
  file.txt
  
  /Users/hwte
  ```

* `(())` : 用于算术表达式，**故可用于数值计算，同 `$(())`，但建议在进行数值计算时使用`$(())`，其更易读** .

  ⚠️注 : 如果使用 `(())` 作为判断语句，大于、小于、大于等于、小于等于可以直接使用 `>`、`<`、`>=`、`<=` .

  ```shell
  if [ "$1" -gt "2024" ]; then
  	echo "$1 > 2024"
  	res=`expr $1 \* 2` # 使用`expr`时`*`符号还需要转义，糟糕透了!
  	echo $res
  fi
  
  # 上述代码可利用`(())`写成更易读的形式
  if (($1 > 2024)) then
  	echo "$1 > 2024"
  	# 建议在进行数值计算时使用`$(())`，其更易读
  	# res=$(($1 * 2))
  	((res=$1 * 2))
  	echo $res
  fi
  ```

  ```shell
  bash-5.2$ ./test.sh 2025
  2025 > 2024
  4050
  2025 > 2024
  4050
  ```

* `$()` : 用于命令替换，例如获取当前目录的路径 : 

  ```shell
  bash-5.2$ path=$(pwd)
  bash-5.2$ echo $path
  /Users/hwte
  ```

* `$(())` : 用于执行算术运算，它允许在 Bash 脚本中进行数学计算 : 

  ```shell
  bash-5.2$ result=$((1012 * 2))
  bash-5.2$ echo $result
  2024
  ```


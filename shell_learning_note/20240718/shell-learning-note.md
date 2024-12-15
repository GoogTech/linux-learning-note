# Shell 学习笔记

## 参考教程

* https://wangdoc.com/bash/
* https://www.runoob.com/linux/linux-shell.html



## Shell 简介

Shell 这个单词的原意是“外壳”，跟 kernel（内核）相对应，比喻内核外面的一层，即用户跟内核交互的对话界面。

具体来说，Shell 这个词有多种含义。

首先，Shell 是一个程序，提供一个与用户对话的环境。这个环境只有一个命令提示符，让用户从键盘输入命令，所以又称为命令行环境（command line interface，简写为 CLI）。Shell 接收到用户输入的命令，将命令送入操作系统执行，并将结果返回给用户。本书中，除非特别指明，Shell 指的就是命令行环境。

其次，Shell 是一个命令解释器，解释用户输入的命令。它支持变量、条件判断、循环操作等语法，所以用户可以用 Shell 命令写出各种小程序，又称为脚本（script）。这些脚本都通过 Shell 的解释执行，而不通过编译。



## Shell 种类

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



## Shell 和 Bash 的历史

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



## ——————



## Bash 简介

Bash 是 Unix 系统和 Linux 系统的一种 Shell（命令行环境），是目前绝大多数 Linux 发行版的默认 Shell。

⚠️注 : 当前系统的默认 Shell 为 `bash`（原来为`zsh`），即本笔记的实验环境 & 学习对象为 `bash` : 

```shell
sw:~ hwte$ echo $SHELL
/bin/bash
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
# 以下为扩展内容 :
# 查看当前系统中已安装的 bash 命令的路径
sw:~ hwte$ which -a bash
/usr/local/bin/bash
/bin/bash
# 查看这两个 bash 命令各自的版本
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
```

23:01:goodnight.



## 进入 & 退出 Bash

打开终端后，如果当前系统默认的 Shell 不是你想使用的类型，可以通过输入`<shell_name>`命令启用指定类型的 Shell .

```shell
# 查看当前系统默认的 Shell
sw:~ hwte$ echo $SHELL
/bin/bash

# 启用`zsh`
gl-f1227452macd:~ hwte$ zsh
hwte@gl-f1227452macd ~ % pwd
/Users/hwte

# 退出`zsh`环境（也可使用 Ctrl+d）
hwte@gl-f1227452macd ~ % exit

# 进入`bash`专属的命令界面（尽管当前系统默认的 Shell 就是`bash`）
# 注: 在此界面学习`bash`编程更舒服一些哈～
hwte@gl-f1227452macd ~ % bash

The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
bash-3.2$
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

3. 读取数组中的元素 : 

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

1. 定义数组 : 

   ```shell
   ```

2. 向数组中添加元素 : 

   ```shell
   ```

3. 读取数组中的元素 : 

   ```shell
   ```

4. 删除数组中的元素 : 

   ```shell
   ```

5. 获取数组的长度 : 

   ```shell
   ```

6. 遍历数组 : 

   ```shell
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

# 目录结构

1. 采用级层式树状目录结构；最上层是根目录"/"； "/" —>"home"、"bin"、"root"、"etc"......
   已规定好目录结构，对应方面存放对应类型的文件
2. 会把计算机的硬件影射成文件来管理     <!--在linux世界里，一切皆为文件-->
3. `/bin` ->  存放最经常使用的一些命令
   `/sbin` -> 存放系统管理员常用的管理程序
   `/home` -> 普通用户的主目录
   `/root` -> 系统管理员的主目录
   `etc` -> 配置文件
   `/user` -> 应用程序和文件；类似于Win的program files
   `/boot` -> 启动`linux`的相关文件
   `/dev` -> 类似于Win的设备管理器
   `/media` -> 自动识别的一些设备（U盘、光驱等）会挂载到此目录
   `/mnt` -> 可挂载外部存储
   `/user/local` -> 安装的软件（一般是通过编译运行的程序）

# 远程登录linux

XSHELL / XFTP

通过ifconfig指令可获得另一台机器的IP

若有中文乱码，可能是编码方式选择不对

# 使用vim

| 移动光标的方法                                               |                                                              |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| h 或 向左箭头键(←)                                           | 光标向左移动一个字符                                         |
| j 或 向下箭头键(↓)                                           | 光标向下移动一个字符                                         |
| k 或 向上箭头键(↑)                                           | 光标向上移动一个字符                                         |
| l 或 向右箭头键(→)                                           | 光标向右移动一个字符                                         |
| 如果你将右手放在键盘上的话，你会发现 hjkl 是排列在一起的，因此可以使用这四个按钮来移动光标。 如果想要进行多次移动的话，例如向下移动 30 行，可以使用 "30j" 或 "30↓" 的组合按键， 亦即加上想要进行的次数(数字)后，按下动作即可！ |                                                              |
| [Ctrl] + [f]                                                 | 屏幕『向下』移动一页，相当于 [Page Down]按键 (常用)          |
| [Ctrl] + [b]                                                 | 屏幕『向上』移动一页，相当于 [Page Up] 按键 (常用)           |
| [Ctrl] + [d]                                                 | 屏幕『向下』移动半页                                         |
| [Ctrl] + [u]                                                 | 屏幕『向上』移动半页                                         |
| +                                                            | 光标移动到非空格符的下一行                                   |
| -                                                            | 光标移动到非空格符的上一行                                   |
| n<space>                                                     | 那个 n 表示『数字』，例如 20 。按下数字后再按空格键，光标会向右移动这一行的 n 个字符。例如 20<space> 则光标会向后面移动 20 个字符距离。 |
| 0 或功能键[Home]                                             | 这是数字『 0 』：移动到这一行的最前面字符处 (常用)           |
| $ 或功能键[End]                                              | 移动到这一行的最后面字符处(常用)                             |
| H                                                            | 光标移动到这个屏幕的最上方那一行的第一个字符                 |
| M                                                            | 光标移动到这个屏幕的中央那一行的第一个字符                   |
| L                                                            | 光标移动到这个屏幕的最下方那一行的第一个字符                 |
| G                                                            | 移动到这个档案的最后一行(常用)                               |
| nG                                                           | n 为数字。移动到这个档案的第 n 行。例如 20G 则会移动到这个档案的第 20 行(可配合 :set nu) |
| gg                                                           | 移动到这个档案的第一行，相当于 1G 啊！ (常用)                |
| n<Enter>                                                     | n 为数字。光标向下移动 n 行(常用)                            |
| 搜索替换                                                     |                                                              |
| /word                                                        | 向光标之下寻找一个名称为 word 的字符串。例如要在档案内搜寻 vbird 这个字符串，就输入 /vbird 即可！ (常用) |
| ?word                                                        | 向光标之上寻找一个字符串名称为 word 的字符串。               |
| n                                                            | 这个 n 是英文按键。代表重复前一个搜寻的动作。举例来说， 如果刚刚我们执行 /vbird 去向下搜寻 vbird 这个字符串，则按下 n 后，会向下继续搜寻下一个名称为 vbird 的字符串。如果是执行 ?vbird 的话，那么按下 n 则会向上继续搜寻名称为 vbird 的字符串！ |
| N                                                            | 这个 N 是英文按键。与 n 刚好相反，为『反向』进行前一个搜寻动作。 例如 /vbird 后，按下 N 则表示『向上』搜寻 vbird 。 |
| 使用 /word 配合 n 及 N 是非常有帮助的！可以让你重复的找到一些你搜寻的关键词！ |                                                              |
| :n1,n2s/word1/word2/g                                        | n1 与 n2 为数字。在第 n1 与 n2 行之间寻找 word1 这个字符串，并将该字符串取代为 word2 ！举例来说，在 100 到 200 行之间搜寻 vbird 并取代为 VBIRD 则： 『:100,200s/vbird/VBIRD/g』。(常用) |
| **:1,$s/word1/word2/g** 或 **:%s/word1/word2/g**             | 从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！(常用) |
| **:1,$s/word1/word2/gc** 或 **:%s/word1/word2/gc**           | 从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！且在取代前显示提示字符给用户确认 (confirm) 是否需要取代！(常用) |
| 删除、复制与贴上                                             |                                                              |
| x, X                                                         | 在一行字当中，x 为向后删除一个字符 (相当于 [del] 按键)， X 为向前删除一个字符(相当于 [backspace] 亦即是退格键) (常用) |
| nx                                                           | n 为数字，连续向后删除 n 个字符。举例来说，我要连续删除 10 个字符， 『10x』。 |
| dd                                                           | 剪切游标所在的那一整行(常用)，用 p/P 可以粘贴。              |
| ndd                                                          | n 为数字。剪切光标所在的向下 n 行，例如 20dd 则是剪切 20 行(常用)，用 p/P 可以粘贴。 |
| d1G                                                          | 删除光标所在到第一行的所有数据                               |
| dG                                                           | 删除光标所在到最后一行的所有数据                             |
| d$                                                           | 删除游标所在处，到该行的最后一个字符                         |
| d0                                                           | 那个是数字的 0 ，删除游标所在处，到该行的最前面一个字符      |
| yy                                                           | 复制游标所在的那一行(常用)                                   |
| nyy                                                          | n 为数字。复制光标所在的向下 n 行，例如 20yy 则是复制 20 行(常用) |
| y1G                                                          | 复制游标所在行到第一行的所有数据                             |
| yG                                                           | 复制游标所在行到最后一行的所有数据                           |
| y0                                                           | 复制光标所在的那个字符到该行行首的所有数据                   |
| y$                                                           | 复制光标所在的那个字符到该行行尾的所有数据                   |
| p, P                                                         | p 为将已复制的数据在光标下一行贴上，P 则为贴在游标上一行！ 举例来说，我目前光标在第 20 行，且已经复制了 10 行数据。则按下 p 后， 那 10 行数据会贴在原本的 20 行之后，亦即由 21 行开始贴。但如果是按下 P 呢？ 那么原本的第 20 行会被推到变成 30 行。 (常用) |
| J                                                            | 将光标所在行与下一行的数据结合成同一行                       |
| c                                                            | 重复删除多个数据，例如向下删除 10 行，[ 10cj ]               |
| u                                                            | 复原前一个动作。(常用)                                       |
| [Ctrl]+r                                                     | 重做上一个动作。(常用)                                       |
| 这个 u 与 [Ctrl]+r 是很常用的指令！一个是复原，另一个则是重做一次～ 利用这两个功能按键，你的编辑，嘿嘿！很快乐的啦！ |                                                              |
| .                                                            | 不要怀疑！这就是小数点！意思是重复前一个动作的意思。 如果你想要重复删除、重复贴上等等动作，按下小数点『.』就好了！ (常用) |

# 用户管理

## 添加账户   

`useradd 用户名`	<!--创建成功后，会自动创建同用户名的家目录在/home/用户名-->

-   `useradd -d 目录路径 用户名`指定家目录
-  `useradd -g 组名 用户名`指定用户所属的组
-  `useradd -G 组名 用户名`指定用户所属的附加用户组
- `groups 用户名` 显示用户所属的用户组

##  指定/修改密码

`passwd  用户名` 修改对应用户的密码

`pwd`显示当前处于哪个目录

## 删除用户

`userdel  用户名`   <!--只有管理员可删人-->

- 删除用户但保存家目录 	`userdel 用户名`
- 全部删除   `userdel -r 用户名`   ***谨慎！！***

## 查询用户信息指令

`id 用户名` 会显示`uid 、gid和组`

切换用户   `su - 用户名` ；返回原来用户时使用`exit/logout` 

查看当前用户   `who am i`  显示第一次登录的用户的信息（不显示切换的）

## 用户组

 系统可以对有共性/权限的多个用户进行统一管理

`groupadd  组名` 添加一个组 ——`groupdel 组名` 删除组

增加一个用户，直接指定到一个组 <!--若未指定，则默认归到同用户名的组里-->     `useradd -g  用户组  用户名` 

`usermod -g 用户组 用户名` 切换用户所属组

### 用户和组相关文件

-  `/etc/passwd `文件
   用户的配置文件（每行含义： 用户名、口令、用户标识号、组标识号、注释性描述、主目录、登录shell）
- `/etc/shadow `文件   口令的配置文件
- `/etc/group` 文件      组的配置文件

# 实用指令[Linux 命令大全 | 菜鸟教程 (runoob.com)](https://www.runoob.com/linux/linux-command-manual.html)

## 外部&内部指令


Linux的命令可以分为内部命令和外部命令：

```markdown
内置命令实际上是 shell 程序的一部分，其中包含的是一些比较简单的 Linux 系统命令,在系统启动时就调入内存，是常驻内存的，所以执行效率高。
 
而外部命令是系统的软件功能，在系统加载时并不随系统一起被加载到内存中，而是在需要时才从硬盘中读入内存.是bash shell之外的程序，它并不是shell 的一部分。外部命令一般位于/bin、/usr/bin、/sbin或/usr/sbin中。
```

## 指定运行级别

1. 关机
2. 单用户  [找回丢失密码]
3. 多用户状态无网络服务
4. 多用户状态有网络服务
5. 图形界面
6. 系统重启

<!--常用4和5，也可以指定默认运行级别-->

通过`init` 切换不同的运行级别

`systemctl get-default` 得到当前运行级别

`systemctl set-default TARGET.target` 设定一个运行级别  （TARGET是对应级别名）

## 找回root密码（不同版本略有差别）

从开机界面进入编辑界面，在有显示linux版本的行之后  输入`init=/bin/sh` 
ctrl+x进入单用户模式，输入`mount -o remount,rw/` 
在新的一行后输入`passwd` enter后输入新的密码*2
输入`touch /.autorelabel` 
输入 `exec /sbin/init` 

## 帮助指令

`man 命令或配置文件`  获得帮助信息

`help 命令` 获得shell**内置命令**的帮助信息  <-->`命令 --help`查询**外部命令**

 `ls 选项 文件名` 指令
		`-a` 选项：列出所有文件，包括"."k开头的隐藏文件
		`-l` 选项： 单列输出
        `-R` 连同子目录内容一同列出

​		<!--选项可以组合使用-->

## 常用指令

- `clear` 清除当前终端内容
- `CTRL+C` 强制终止命令
- `top` 监控`linux`的系统状况，实时显示系统中各个进程的资源占用情况
- `ping` 检测是否可建立网络连接	
- 可使用`tab键` 自动补全文件名或命令名及文件目录



## 文件目录类指令

- `pwd`指令  显示当前工作目录的**绝对**路径
- `cd [参数]` 切换到指定目录   参数区分绝对和相对路径
  		`cd ~ ` 或者`cd` 回到家目录
    		`cd ..` 回到当前目录的上一级目录  比如：从`/home/tom/ `到`/root`   用`cd ../../root`
- `mkdir /路径.../文件夹名`  创建一个文件夹 (默认只可创建一级目录)
  		`mkdir -p` **创建多级目录** : `mkdir -p /dir1/dir2` 分别创建两个目录
- `rmdir 目录名` 删除一个目录（其删除的是空目录，如果目录下有内容则无法删除）**`rm -rf`** 可**删除非空目录**
     `rmdir -p /目录名1/目录名2` **递归删除**。删除目录1下的目录2，若目录1为空目录，则也删除目录1.
- `touch 文件名称` 创建空文件
- `cp [选项] 要复制的文件  目的地`  拷贝指定文件到文件夹 
  	-r ： 递归复制整个文件夹  比如：将`/home/bbb`整个目录（包括目录本身）复制到指定文件夹
  	`\cp` 指令 ，强制覆盖
  引申：可以使用通配符来匹配`/etc`目录下所有文件名第2位至第4位是`ost`的文件，然后使用`cp`命令将它们复制到`/var/tmp`目录。具体命令如下：
       `sudo cp /etc/?ost* /var/tmp/` 
  这里的**通配符“*”表示匹配任意字符，所以`*ost*`可以匹配所有文件名中包含`ost`的文件**。需要**使用`sudo`命令获取管理员权限**，因为在Ubuntu系统中，`/etc`目录下的大部分文件都是只有管理员才有权限进行读写操作的。复制完成后，所有符合条件的文件都会被复制到`/var/tmp`目录下。
- `rm` 指令 ：**移除文件或目录**
  	-r  : 递归删除整个文件夹
  	-f  :  强制删除不提示
    `-i`：交互式删除，删除前询问用户是否确认删除。
- `mv` 移动文件或目录或重命名
   (若两个文件在同目录，则此时是**重命名**  `mv 文件名 新文件名`)
   (移动：`mv 文件名 文件夹`) 
   (移动并命名   `mv 旧文件名 /目标目录.../新文件名`)
   `-f` 强制覆盖同名的 

### 显示文本文件内容

- `cat [选项] 要查看的文件` 查看文件内容
     -n 显示行号
     <!--cat 只能浏览文件，无法修改文件。为了方便一般加上**管道命令** |more-->

- `more 要查看的文件`  指令；是基于VI编辑器的文本过滤器，以全屏幕的方式 按页显示文本文件内容（也可以和cat结合使用） 
  ![6EZ}{~{YHF5M`(V9LO@8HF0](C:\Users\Administrator\Desktop\编程笔记\linux\6EZ}{~{YHF5M`(V9LO@8HF0.png)

- `less 要查看的文件` 用来分屏查看文件,可用`PgDn`和`PgUp`翻页（动态加载）![QHEO@RQ3L68NME`AHZ]B{ZD](D:\资料\学科学习资料\编程笔记\linux\QHEO@RQ3L68NME`AHZ]B{ZD.png)

- `echo [选项] [输出内容] `  使出内容到控制台 

- `head 文件` 显示文件的开头部分 ，默认下显示前十行
      `head -n 行数` 显示自定行数

- `tail 文件` 

  用于输出文件尾部内容
  `tail -n 文件` 查看末尾n行内容
  `tail -f 文件` 实时追踪该文档的所有更新

- `> `重定向指令`>>`追加指令
  `ls -l > 文件` （把列表中的内容写入文件中（覆盖式））  <!--若当前文件不存在，则会创建-->
  **`ls -al >> 文件` (将列表中的内容追加到文件中)**
  **`cat 文件1 > 文件2 ` （用·文件1的内容覆盖掉文件2）**
  **`echo “内容” >> 文件` (追加)**

- `ln 原文件/目录 硬连接名` 给文件创建一个硬链接，但是在不同文件系统中不可建立硬链接。
  **`ln -s [原文件或目录] [软链接名] ` 给原文件创建一个软链接（软链接也称符号链接，类似于快捷方式）**
  `rm [软链接名]` 删除软链接  

- `history` 查看命令执行的历史记录 <!--使用符号`!` 执行指定序号的命令，没有history前缀-->
         `history -c `清空当前历史命令
         `history 10` 显示最近的10条记录
          使用`!n`（其中n表示命令的编号）可以执行指定的命令。例如，输入`!10`可以执行第10条命令。
     
- **`file [选项] 文件名`** file命令是一个Linux/Unix系统下的命令，用于识别文件类型。
     常用的选项包括：

     - -b：仅输出文件类型，不显示文件名；
     - -i：输出MIME类型；
     - -f filename：从文件中读取文件名列表，对每个文件执行file命令；
     - -h：显示帮助信息。

## 时间日期类

- date 指令 显示当前时期
  1.`date +%Y` 显示年份
  2.`date +%m` 显示月份
  3.`date +%d` 显示哪一天
  4.`date +"%Y-%m-%d %H:%M:%S"` 显示年月日时分秒
  `date -s  字符串时间` 设置时间；例：`date -s "2023-03-19  10:07:30"` 
- `cal 指令`
  `cal [选项] `（不加选项，显示当月日历）
  显示2020年日历 ：`cal 2020`

## 搜索查找类

- find指令  将从指定目录向下递归地遍历各个子目录，将满足条件的文件或目录显示在终端
  `find [搜索范围] [选项]` 
  选项：
         `-name 文件名` 按照指定的文件名查找模式查找文件
         `-user 用户名`查找属于指定用户的所有文件
         `-size` 按照制定文件大小查找文件
         `-print`显示整个文件的路径与名称 
  
  实例：
        1.在home目录下查找`hello.text` : `find /home -name hello.text`
        2.在/opt目录下，查找用户名为nobody的文件 :  `find /opt -user nobody `
        3.查找整个系统中大于200mb的文件（+n 大于 -n 小于 n 等于,单位有:k,M,G）: `find / -size +200M`
  
  ​      4.查找所有文件名中含有dev的文件`find ~ -name "dev" -print` 
  引申：
  
  - 使用find命令搜索` /etc `目录下文件名第2位至第4位是`ost`的所有内容
    `sudo find /etc -name '?ost*'`
  - 查找以**my开头**的所有普通文件
    `find /user -name my* -type f -print` 
  
- locate 指令，快速定位文件路径
  `locate 搜索文件` <!--locate基于数据库查询，所以第一次运行前，必须先执行updatedb指令-->

- which指令，可以查看某个指令在哪个目录下 `which 指令名` 

- grep指令和管道符号，grep 过滤查找，管道符'|' ；表示将前一个命令的处理结果输出传递给后面的命令执行
  `grep [选项] 查找内容 源文件` 
  选项：

  ​       -n 显示匹配行及行号； -i 忽略字母大小写
  实例：在hello.txt文件中查找"yes" 所在的行，并显示行号`cat /home/hello.txt | grep "yes"`  或者`grep -n "yes" /home/hello.txt`

## 压缩和解压类

- `gzip/gunzip` 指令
  `gzip 文件` (压缩文件，只能将文件压缩成.gz文件)
  `gunzip 文件.gz` (解压缩文件)
  实例：将/home下的hello.txt文件进行gzip压缩
            `gzip /home/hello.txt` 

- `zip/unzip`指令

  `zip [选项] XXX.zip  将要压缩的内容` (压缩文件和目录) 
  `unzip [选项] XXX.zip` （解压缩文件）
  zip常用选项： -r  递归压缩，即压缩目录
  unzip常用选项： -d <目录> 指定压缩文件后的存放目录
  案例：
       将/home下的所有文件/文件夹进行压缩成 myhome.zip `zip -r myhome.zip  /home` 
       将myhome.zip 解压到/opt/temp 目录下  `unzip -d /opt/temp  /home/myhome.zip`

- tar指令
  其是打包指令，最后打包的文件是 .tar.gz 格式
  `tar  [选项]  XXX.tar.gz  打包的内容` 
  选项说明：
      -c  产生.tar打包文件
      -v  显示详细过程
      -f   指定压缩后的文件名
      -z  打包的同时压缩
      -x  解包.tar文件
  应用实例：
       压缩多个文件，将/home/pig.txt 和 /home/cat.txt 压缩成pc.tar.gz  `tar -zcvf pc.tar.gz /home/pig.txt /home/cat.txt`

  ​    将/home 的文件夹 压缩成 myhome.tar.gz  `tar -zcvf myhome.tar.gz /home/`
  ​    将 pc.tar.gz 解压到当前目录
  ​    `tar -zxvf pc.tar.gz` 
  ​    将 myhome.tar.gz 解压到 /opt/temp目录下 `tar -axvf /home/myhome.tar.gz -C /opt/temp` 

## 组管理和权限管理

### 组的介绍

- linux中每个用户必须属于一个组，不可独立于组之外
- 每个文件有所有者、其他组、所属组

### 所有者

- 查看文件所有者
  ·ls -ahl`查看所有者——>前面的是所有者，后面是目录名
- 修改所有者
  `chown [用户名]:[用户组] 文件`
  `chown user1 myfile` 设置文件`myfile` 的所属用户为`user1` 
  `chown :grp1 myfile`设置文件`myfile` 的所属组为`grp1` 
  `chown user1:grp1 myfile` 设置文件`myfile` 的所属用户为`user1` ，所属组为`grp1` 

### 所在组

- `groupadd 组名` 创建一个组——`useradd -g 组名 用户名` 创建一个用户，并放入到一个组中
- 查看目录/文件所在组`ls -ahl` 
- `chgrp 组名 文件名` 修改文件所在组

其他组：除了文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组

- `usermod -g 新组名 用户名` 改变用户所在的主用户组
- `usermod -d 目录名 用户名 ` 改变该用户登录的初始目录。<!--用户要有进入新目录的权限-->

### 权限管理

#### ls -l显示的内容中；0到9位

实例：-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc

- 第零位确定文件类型（d ,- ,l ,c, b）
  - l 是链接，相当于windows的快捷方式
  - d 是目录，相当于Windows的文件夹
  - c 是字符设备文件，鼠标、键盘
  - b 是块设备，比如：键盘
  - `-` 是普通文件
  - p 命名管道文件
- 第一到三位确定所有者拥有该文件的权限  ——User
- 第四到六位：确定所属组（同用户组的）拥有该文件的权限 ——Group
- 第七到九位：其他用户拥有该文件的权限

也可用数字表示：**r = 4; w = 2; x = 1**;  因此rwx = 4+2+1=7

- 1 代表文件的硬连接数或者目录的子目录数
- root  用户
- root  组
- 1213  文件大小（字节），若是文件夹，显示4096字节
- Feb 2 09:39 代表修改日期
- abc   文件名

#### rwx权限详解

##### 作用到文件

- [ r ] 代表可读；可以读取、查看
- [ w ] 代表可写；可以修改，但不代表可以删除文件。删除权限需要有对该文件所在的目录有写权限
- [ x ] 代表可执行

##### 作用到目录

- [ r ] 代表可以ls查看目录内容
- [ w ] 代表可写；可以修改，对目录创建+删除+重命名
- [ x ] 代表可执行，可以进入该目录，如：cd

### 修改权限

`chmod` 指令

#### 第一种方式

u : 所有者； g : 所在组； o：其他人：a ：所有人

- `chmod u=rwx,g=rx,o=x 文件/目录名` 给予所有者rwx权限，给同组用户rx权限，给其他人执行的权限
- `chmod o+w 文件/目录名`   给其他用户 w 的权限
- `chmod a-x 文件/目录名` 

实例：给abc文件的所有者除去 执行权限，增加组写的权限`chmod u-x,g+w abc`

#### 第二种：通过数字

`chmod  u=rwx,g=rx,o=x 文件/目录名` ==`chmod 751 文件/目录名`  

### 修改文件所有者

`chown newowner 文件/目录` 改变所有者
`chown newowner:newgroup  文件/目录` 改变所有者和所在组
`-R ` 如果是目录，则其下所有子文件及目录递归生效

### 修改文件/目录所在组

`chgrp newgroup 文件/目录` 改变所在组

## 进程管理相关指令

1. `pstree` 显示系统中进程的继承关系
2. `ps [选项]` 显示系统中进程的状态和属性——记清对应字段名的含义

| -a   | 显示所有进程，包括其他用户的 |
| ---- | ---------------------------- |
| -r   | 只显示正在运行的进程         |
| -x   | 显示没有控制终端的进程       |
| -u   | 打印用户格式，显示用户名     |
| -l   | 长列表方式                   |
| -e   | 显示所有进程                 |
| -f   | 全格式                       |
| -j   | 按作业格式输出               |

`ps -ejf` 显示所有进程

`ps -a` 显示所有终端上运行的进程

1. `kill [-s 信号代码] 进程PID`

   `killall 进程名称` 

   `-9` 表示强制终止
   ``-l` 列出所有可用的信号名
   `-s` 指定发送的信号

- `kill -l`列出所有的信号
- `kill -9 323`发送信号9终止PID为323的进程
- `kill -9 -1223`杀死进程组号为1223的所有进程
- `kill -ITERM 0`发送信号ITERM给当前进程组中的所有进程
- `kill -9 -1`发送信号KILL给所有进程标识大于1的进程

1. `fg 作业号` 将指定作业号的作业从后台切到前台
2. `bg 作业号`让指定作业号的后台暂停进程继续运行
3. `jobs` 显示当前的后台程序状态

## 输入输出重定向和管道

### 输入重定向

`命令 <输入文件` 或`命令 0<输入文件` 从输入文件中获取数据，而不是从键盘中

`cat </etc/fstab` 显示文件`/etc/fstab` 的内容

### 输出重定向

`命令 n>输出文件`为覆盖 ——`命令 n>>输出文件` 为追加

**数字n：**

- 1  标准输出
- 2 标准错误输出
- & 标准输出和标准错误输出

- `ls /etc/fstab >>error` 将标准输出追加到重定向文件`error`
- `ls -l &>errfile` 将标准输出和标准错误输出重定向至文件`errfile`

### 管道

其将一个进程的标准输出作为另一个进程的标准输入

#### 无名管道

`命令1 | 命令2 |.....[命令n]` ：将命令1的标准输出作为命令2的标准输入，再将命令2的标准输出作为命令3的标准输入，以此类推

`cat file | grep 'pipe' | more` 分页显示文件file中包含“pipe”的所有行

#### 命名管道

`mkfifo [选项] 文件名` ：创建命名管道文件

选项`-m` 表示文件的权限 ，同`chmod`

- `mkfifo -m 664 myfifo` 建立权限为664的命名管道文件`myfifo`
- `mkfifo -m g-w,o-rw fifo` 建立命名管道文件`fifo`
- `mkfifo a=rw demofifo` 建立命名管道文件`demofifo`，权限为666
- `cat core.c >demofifo &`向命名管道文件中写入`core.c`
- `cat <demofifo` 从`myfifo`中读取内容

## 元字符与正则表达式

### 通配符

| 元字符 | 含义                                       |
| ------ | ------------------------------------------ |
| ？     | 匹配任意一个字符                           |
| *      | 匹配相当数量的字符                         |
| [abc]  | 匹配方括号中的任意一个字符                 |
| [a-z]  | 匹配方括号内中表示字符范围内的任意一个字符 |
| [!a-z] | 匹配除了方括号中表示范围的字符             |

-  `ls [a-z]*`  #查找以字母a到z开头的所有文件
-  `ls [!a-z]*`#查找不以字母a到z开头的所有文件
- `ls *.c` #查找后缀名为c的所有文件

#### 屏蔽元字符的特殊含义

有时，若需要在命令中使用元字符本身，不希望元字符表示其特殊的含义，下面介绍两方法。
在包含元字符的字符串两边加单引号或双引号
`ls “ab*cd"`  #查找文件名为“ab*cd”的文件
在元字符前使用反斜杠“\”。这样，紧接在反斜杠“\”后的元字符就失去了特殊的含义，仅表示元字符本身。
 `ls abc\*def` #查找文件“abcdef”

### 正则表达式

`grep [选项] 正则表达式 文本文件列表` 

![qq_pic_merged_1680785094012_看图王](D:\资料\学科学习资料\编程笔记\linux\qq_pic_merged_1680785094012_看图王.jpg)



　　实例分析
　　1.在文件textfile中搜索以字符“n”开头的所有行。
　　` grep '^n' textfile`
　　2.在文件textfile中索以“.00”结尾的所有行。
　　`grep '\.00$' textfile`
　　3.在文件`textfile`中搜索包含数字5，后面紧接字符“.”，再后面是任意一个字符的所有行。
　　` grep '5\..' textfile`
　　4.在文件textfile中搜索以字符“w”和“y”开始的所有行。
　　` grep '[^wy]' textfile`
　　5.在文件textfile中搜索以字符“.”后紧接两个非数字0结尾的所有行。
　　`grep '\.[^0][^0]$' textfile`
　　6.在文件textfile中搜索包含至少6个连续数字，后面紧接着字符“.”的所有行。
　　`grep '[0-9]\{6\}\.' textfile`
　　7.在文件textfile中搜索包含以单词“north”开始的所有行。
　　`grep '\<north' textfile`

# `crond`任务调度

## 入门

### `crontab`用法

`crontab`进行定时任务的设置

`crontab [选项]` 
选项：1. -e : 编辑`crontab` 的定时任务；2. -l ：查询`crontab`任务； 3. -r ：删除当前用户所有的`crontab`任务

例： `crontab -e`然后向文件中写入` */1 * * * * ls -l /etc/ > /tmp/to.txt`   意思是每隔一分钟执行一次`ls -l /etc/ > /tmp/to.txt`命令

### 时间规则

- 第一个‘*’代表一小时中的第几分钟
- 第二个‘*’代表一天中的第几小时
- 第三个‘*’代表一个月中的第几天
- 第四个‘*’代表一年中的第几个月
- 第五个‘*’代表一周中的星期几(范围是0-7；0/7都代表周日)

## 时间规则

### 特殊符号说明

- `*`代表任何时间。比如第一个“*” 就代表一小时中每分钟都执行一次的意思。
- `,`代表不连续的时间。比如`0 8,12,16 * * *`命令，就代表在每天的8点0分，12点0分，16点0分都执行一次命令
- `-`代表连续的时间范围。比如`0 5* * 1-6命令`代表在周一到周六的凌晨5点0分执行命令
- `*/n`代表每隔多久执行一次。比如`*/10 * * * *命令`代表每隔10分钟就执行一
- 一遍命令

### 特定时间执行案例

- `45 22 * * *`命令——在22点45分执行命令
- `0 17 * * 1`命令——每周1的17点0分执行命令
- `0 5 1,15**`命令——每月1号和15号的凌晨5点0分执行命令
- `40 4 * * 1-5 `命令——每周一到周五的凌晨4点40分执行命令
- `*/10 4 * * *`命令——每天的凌晨4点，每隔10分钟执行一次命令
- `0 0 1,15 * 1` 命令——每月1号和15号，每周1的0点0分都会执行命令。注意：星期几和几号最好不要同时出现，因为他们定义的都是天。非常容易让管理员混乱。

## 相关指令

- `crontab -r` 终止任务调度
- `crontab -l ` 列出当前有哪些任务调度
- `service crond restart `重启任务调度

### 案例：

每隔一分钟，将当前日期和日历都追加到 `/home/mycal` 文件中

1. 先创建脚本`vim /home/my.sh`, 写入内容 `date >> /home/mycal` 和 `cal >> /home/mycal` 
2. 给`my.sh` 增加执行权限， `chmod u+x /home/my.sh`
3. `crontab -e` 增加`*/1 * * * * /home/my.sh` 

# at任务调度

### 机制

- at是一次性定时计划任务，at的守护进程atd会以后台模式运行，检查作业队列来运行
- 默认下，atd守护进程每一分钟检查作业队列。有作业时，检查作业的运行时间，如果时间与当前时间匹配，则运行此作业
- at命令，执行完一次后就不再执行此任务
- 使用at命令时，一定保证atd进程的启动，可以用`ps -ef | grep atd` 来查看

### 命令格式

- `atd [选项] [时间]`   (如果不指定选项，则 `atd` 将使用默认选项执行任务。)
  - `-b`：指定一个可执行文件或 shell 脚本，用于作为执行任务的 shell 环境。
  - `-d`：将调试信息输出到系统日志中。
  - `-f`：指定一个文件名，用于作为任务的标准输入。
  - `-l`：禁用 `at` 命令中的 `MAILTO` 环境变量，防止任务执行完成后发送邮件通知。
  - `-s`：禁用 `at` 命令中的 `MAILTO` 环境变量，防止任务执行完成后发送邮件通知，并将标准输出和标准错误输出合并为一个文件。
  - `-x`：设置任务执行时的 umask 值，通常为 `022`。
- `at > 指令/shell脚本` 
- `Ctrl + D` 结束`at` 命令的输入（需要输入两次）

### 时间定义

案例

1. 2天后的下午5点运行  `/bin/ls /home`
   `at 5pm + 2 days` --> `at> /bin/ls /home`
2. 明天下午5点，输出时间到指定文件/root/date100
   `at 5pm tomorrow` -->`at> date> /root/date100`
3. 两分钟后，输出时间到指定文件内  /root/date200
   `at now + 2 minutes` --> `at> date> /root/date200`
4. 删除已经设定好的任务 `atrm 编号` 



`atq` 命令用于列出系统中所有待执行的 `at` 任务

# 磁盘

## 分区机制

`lsblk` 指令（或者`lsblk -f` ）——看硬盘和Linux文件系统的关系
硬盘分区与文件系统的关系是“挂载”

### Linux分区

Linux硬盘分为IDE和SCSI硬盘，目前基本是SCSI

SCSI硬盘标识为`sdx~`  ，用`sd`表示分区所在设备的类型，`x` 为盘号（a为基本盘，b为基本从盘，c是辅助主盘，d是辅助从属盘），`~`代表分区，

## 增加磁盘的应用实例

1. 虚拟机添加硬盘(非命令操作，用的话再查吧)
2. 分区——分区命令`fdisk /dev/sdb` 
   开始对/sdb分区：
     m 显示命令列表
     p显示磁盘分区 同`fdisk -l`
     n新增分区·
     d删除分区
     w写入并退出
   说明：开始分区后，输入n，新增分区；然后选择p，分区类型为基本，后面输入的数就是几个分区；两次回车默认剩余全部空间；输入w写入分区并退出，若不保存退出则输入q
3.   格式化——分区命令`mkfs -t ext4 /dev/sdb1` (`ext4` 是分区类型)
4. 挂载——`mount 设备名称 挂载目录`
   先创建一个新的文件夹`mkdir /newdisk`，然后挂载`mount /dev/sdb1 /newdisk/` 
   卸载——`umount 设备名称或挂载目录`

**用命令行挂载的方式，重启后会失效**

5.通过修改`/etc/fstab` 实现挂载；添加完成后，执行`mount -a` 生效

## 磁盘情况查询

- 查询整体使用情况——`df -h` 显示总容量、已用、可用、挂载点
- 查询指定目录—— `du -h` 
  -s 指定目录的占用大小汇总
  -h带计量单位
  -a含文件
  --max-depth=？子目录深度
  -c 列出明细的同时，显示汇总值
        实例： 查询/opt目录的磁盘占用情况，显示一级子目录 `du -ah --max-depth=1 /opt` 

### 相关的使用指令

1. 统计文件夹下文件的个数
   `ls -l 文件夹` 显示全部——>`ls -l 文件夹 |grep "^-"`用`grep` 过滤，只要以-开头的，就过滤出了文件——>`ls -l 文件夹 |grep "^-" |wc -l` 计数
2. 统计文件夹下目录的个数`ls -l 文件夹 |grep "^d" |wc -l` 以d开头的都是目录
3. 统计文件夹下文件的个数，包括子文件夹里的`ls -lR 文件夹 |grep "^d" |wc -l`  加了R，递归
4. 统计文件夹下目录的个数，包括子文件夹里的`ls -lR 文件夹 |grep "^d" |wc -l`
5. 以树状显示目录结构 `tree` 命令

# 网络配置

## NAT网络原理

## 网络配置指令

`ifconfig指令` 查看IP和网络配置（Linux）`ipconfig` (Win)

`ping 目的主机` 测试当前服务器是否可以连接到目的主机（用的是IP或者网址）

## 实例

### 第一种(自动获 取IP，可以避免冲突，但是每次自动获取的IP都不一样)

### 第二种指定·IP

将IP配置为静态的：通过直接修改 `/etc/network/interfaces` 配置文件，将IP地址等信息写入该文件中，然后重启网络服务或重启系统。

# shell（大部分见课本）

![(9YE43MRKLAXV`EM{4S4_GJ](D:\资料\学科学习资料\编程笔记\linux\(9YE43MRKLAXV`EM{4S4_GJ.jpg)

![H4)L1{VU93~EOIPSR]S[GW4 (2)](D:\资料\学科学习资料\编程笔记\linux\H4)L1{VU93~EOIPSR]S[GW4 (2).jpg)

![CIO2]33`1_0K%}3~%4@1URT](D:\资料\学科学习资料\编程笔记\linux\CIO2]33`1_0K%}3~%4@1URT.png)

## 补充

### 在Shell脚本中，空格通常用于以下几种情况：

1.命令和参数之间：命令和其参数之间需要用空格分隔开，例如：
`ls -l   # 正确，命令ls和参数-l之间有空格
ls -l   # 错误，命令ls和参数-l之间没有空格`
2.运算符和操作数之间：在Shell中使用运算符（如等于号、加号、减号等）时，运算符与操作数之间需要用空格分隔开，例如：
3.方括号（用于测试条件）内的元素之间：在Shell中使用方括号进行条件测试时，方括号内的元素之间需要用空格分隔开，例如：
`if [ $num -eq 10 ]; then  # 正确，方括号内的元素之间有空格
if [$num -eq 10 ]; then  # 错误，方括号内的元素之间没有空格`
4.大括号（用于代码块）前后：在Shell中使用大括号表示代码块时，大括号前后需要有空格分隔开，例如：
`for i in {1..5}; do    # 正确，大括号前后有空格
for i in {1..5}; do    # 错误，大括号前后没有空格`
5.函数名和函数体之间：在Shell中定义函数时，函数名和函数体之间需要有空格分隔开，例如：
`function my_function() { # 正确，函数名和函数体之间有空格
function my_function(){  # 错误，函数名和函数体之间没有空格`

这些是Shell脚本中一些常见的情况，需要注意在这些情况下加入适当的空格，以确保脚本的正确性和可读性。当然，有些情况下Shell脚本对空格的要求可能略有不同，具体的语法规则可以参考相关的Shell文档和教程。

### repeat

如要在屏幕上显示连字符（-）100次，则利用如下的命令：`repeat 100 echo ‘-’`

### apt

`sudo apt install Package-name`
`sudo apt remove package`
`sudo apt upgrade` 

# 啊~~♂

1. shell命令的中断用`Ctrl + C` 
2. `while [ 条件 ]`   它的条件判断是`-lt / -gt` 一套
   `for (( 初始化; 条件; 更改项))`   它的条件判断是正常的比较大小数学符号
3. 获取字符串的长度（变量前加# ）`echo ${#name}` 
4. `expr 1 + 2`  `expr 2 \* 5` 每个运算符两边必须用空格相隔（注意，*有转义）
5. 在条件判断的 []  中， 字符串比较中 `=` 两边若没有空格，则为赋值；若有，则正常比较
6. for  变量名 in ...... <!--一定没有$-->       case 变量 in <!--应有$-->
7. find 语句-name 检索的条件一定带上`‘’` 或者` “”` 
   `ls /etc/[a-e]??`
   `cp /etc/?ost* /var/tmp` 则没有
8. shell命令中使用第一个小表，用来通配文件和目录；文本处理程序（例：grep）使用第二个大表

 


















****

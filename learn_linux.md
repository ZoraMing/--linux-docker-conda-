[TOC]

# 基本操作

查看帮助文档
| 命令   | 语法                 | 说明                                   |
|--------|----------------------|----------------------------------------|
| man    | man [命令或程序]      | 用于查看命令或程序的手册页面。例如，`man ls` 查看 `ls` 命令的手册。|
| info   | info [命令或程序]     | 用于查看命令或程序的信息页面。通常比 `man` 提供更详细的信息。例如，`info ls` 查看 `ls` 命令的信息。|
| help   | help [命令]           | 用于显示shell内建命令的简要帮助。例如，`help cd` 显示 `cd` 命令的帮助。|
| ?      | [命令] --help 或 [命令] -h | 有些命令支持在命令后面加 `--help` 或 `-h` 选项来显示帮助信息。例如，`ls --help` 显示 `ls` 命令的帮助。|
| which     | which [命令]               | 用于显示命令的路径。例如，`which ls` 显示 `ls` 命令的路径。|
| date      | date [选项]                | 显示或设置系统日期和时间。例如，`date` 显示当前日期和时间。|
| arch      | arch                       | 显示计算机架构。例如，`arch` 显示当前系统的架构。|
| netstat   | netstat [选项]             | 显示网络相关的信息，如网络连接、路由表等。例如，`netstat -a` 显示所有网络连接。|
| kill      | kill [选项] 进程号          | 终止指定进程。例如，`kill -9 1234` 终止进程号为 `1234` 的进程。|
| poweroff  | poweroff                   | 关闭系统电源。例如，`poweroff` 关闭系统。|
| shutdown  | shutdown [选项] 时间        | 安排系统关机。例如，`shutdown -h now` 立即关机。|
| reboot    | reboot                     | 重新启动系统。例如，`reboot` 重新启动系统。|

## 简单基础命令,简单管理文件

| 指令 | 语法 | 常用参数及含义 |
|-|-|-|
|ls|ls [选项][路径，空则为当前路径]|-l (显示详细信息)、-a(显示隐藏文件)|
| rm   | rm [选项] 文件或目录 | 用于删除文件或目录。常用选项包括 `-r`（递归删除目录）和 `-f`（强制删除，不提示）。例如，`rm -r directory` 删除目录及其内容。|
| cp   | cp [选项] 源文件 目标目录或文件 | 用于复制文件或目录。常用选项包括 `-r`（递归复制目录）和 `-i`（交互式，提示是否覆盖文件）。例如，`cp file1 file2` 复制文件。|
| cd   | cd [目录] | 用于改变当前工作目录。例如，`cd Documents` 进入 Documents 目录。不带参数时，`cd` 进入用户的主目录。|
| mv   | mv [选项] 源文件或目录 目标目录或文件 | 用于移动文件或目录，也可用于重命名。常用选项包括 `-i`（交互式，提示是否覆盖文件）。例如，`mv file1 directory/` 将文件移动到目录。|
| mkdir   | mkdir [选项] 目录名 | 用于创建新目录。常用选项包括 `-p`（递归创建目录，即使父目录不存在）。例如，`mkdir my_folder` 创建一个名为 `my_folder` 的目录。|
| touch   | touch 文件名 | 用于创建空文件或更新文件的访问和修改时间。例如，`touch myfile.txt` 创建一个名为 `myfile.txt` 的空文件。|
| history | history [选项] | 用于显示命令历史记录。常用选项包括 `-c`（清空历史记录）、`-w`（将当前命令写入历史记录文件）、`-r`（从历史记录文件中读取命令）`！n`（执行第n条历史命令）。例如，`history` 显示命令历史记录。|
| tree    | tree [选项] [目录] | 用于以树状结构显示目录和文件。常用选项包括 `-d`（只显示目录）和 `-L`（指定显示的层级）。`-a` （显示隐藏文件）|
| du      | du [选项] [文件或目录] | 用于显示文件或目录的磁盘使用情况。常用选项包括 `-h`（以人类可读格式显示大小）和 `-s`（仅显示总大小）。例如，`du -h my_folder` 显示 `my_folder` 目录的大小。|
| df      | df [选项] [文件系统] | 用于显示文件系统的磁盘空间使用情况。常用选项包括 `-h`（以人类可读格式显示大小）和 `-T`（显示文件系统类型）。例如，`df -h` 显示所有文件系统的磁盘空间使用情况。|
| uname   | uname [选项] | 用于显示系统信息。常用选项包括 `-a`（显示所有信息）、`-r`（显示内核版本）。例如，`uname -a` 显示系统的所有信息。|
| pwd      | pwd                               | 显示当前工作目录的路径。例如，`pwd` 显示当前工作目录。|
| echo   | echo [字符串]                              | 输出字符串。常用于脚本中，也可用于将文本输出到终端。例如，`echo "Hello, World!"` 输出字符串。|

## 功能符号

| 符号 | 语法 | 说明 |
|------|------|------|
| `>`  | command > file | 将命令的标准输出重定向到指定的文件。如果文件不存在，会创建新文件；如果文件已存在，会覆盖文件内容。例如，`ls > file.txt` 将 `ls` 命令的输出重定向到 `file.txt` 文件。|
| `>>` | command >> file | 将命令的标准输出追加到指定的文件末尾。如果文件不存在，会创建新文件；如果文件已存在，会在文件末尾追加内容。例如，`echo "Hello" >> file.txt` 将 "Hello" 追加到 `file.txt` 文件。|
| `\|`  | command1 \| command2 | 将命令1的输出作为命令2的输入，实现两个命令之间的数据传递。例如，`cat file1.txt | grep "pattern"` 使用管道将 `cat` 的输出传递给 `grep` 进行搜索。|
| `&`  | command & | 将命令放在后台运行，允许用户继续输入其他命令而不必等待当前命令执行完成。在后台运行的命令会在当前终端继续输出信息。例如，`nohup command &` 以后台方式运行 `command`，即使关闭终端，命令也会继续执行。|
| `;`  | command1 ; command2 | 按顺序执行多个命令，不管前一个命令是否成功。例如，`echo "Hello" ; ls -l` 会依次执行两个命令。|
| `$()` 或 `` | result=$(command) 或 result=`command` | 将命令的输出结果赋值给变量。例如，`mydate=$(date)` 会将当前日期和时间赋值给 `mydate` 变量。|
| `*`  | command * | 匹配任意字符，常用于文件名的通配符匹配。例如，`rm *.txt` 删除所有以 `.txt` 结尾的文件。|
| `?`  | command ? | 匹配任意单个字符，常用于文件名的通配符匹配。例如，`ls file?` 匹配 `file1`、`file2` 等。|
| `!`  | !n | 执行历史记录中的第n个命令。例如，`!25` 执行历史记录中的第25个命令。|



## 文件管理
vim                 文本编辑工具
nano                文本编辑工具



| 命令   | 语法                                            | 说明                                      |
|--------|-------------------------------------------------|-------------------------------------------|
| cat    | cat [文件]                                      | 连接文件并打印到标准输出。例如，`cat file.txt` 显示文件内容。|
| more   | more [文件]                                     | 逐屏显示文件内容。可以使用空格键进行逐屏翻页。例如，`more file.txt` 逐屏显示文件内容。|
| less   | less [文件]                                     | 与`more`类似，但提供更多交互式操作。例如，`less file.txt` 以交互方式显示文件内容。|
| tac    | tac [文件]                   | 反向显示文件的内容（从底部到顶部）。例如，`tac file.txt` 反向显示 `file.txt` 文件内容。|
| tail   | tail [选项] [文件]           | 显示文件末尾的内容。常用选项包括 `-n`（显示行数）、`-f`（实时跟踪文件末尾的内容）。例如，`tail -n 10 file.txt` 显示文件末尾的最后10行。|
| head   | head [选项] [文件]           | 显示文件开头的内容。常用选项包括 `-n`（显示行数）。例如，`head -n 5 file.txt` 显示文件开头的前5行。|
| diff   | diff 文件1 文件2                                | 比较两个文件的差异。例如，`diff file1.txt file2.txt` 比较两个文件的不同之处。|
| find   | find [路径] [选项] -name "文件名模式"           | 在指定路径下文件或目录。例如，`find /home/user -name "*.txt"` 查找用户主目录下所有扩展名为 `.txt` 的文件。|
| grep   | grep [选项] "模式" [文件]    | 在文件中搜索指定的模式。常用选项包括 `-i`（忽略大小写）、`-n`（显示行号）、`-r`（递归搜索目录下的文件）。例如，`grep -i "keyword" file.txt` 在文件中搜索包含关键字的行。|
| ln     | ln [选项] 源文件 目标文件                      | 创建链接文件。常用选项包括 `-s`（创建符号链接）和 `-b`（创建备份链接）。例如，`ln -s source.txt link.txt` 创建符号链接。可以-s添加到user/local/bin/中作为环境变量。软链接源文件必须用绝对路径。|
| tar    | tar [选项] 目标文件 [源文件或目录]            | 打包和解包文件。常用选项包括 `-c`（创建归档文件）、`-x`（解包归档文件）、`-z`（使用gzip进行压缩）、`-j`（使用bzip2进行压缩）。例如，`tar -cvf archive.tar file1 file2` 创建归档文件。常用`-cvr`|
| gzip   | gzip [选项] 文件  | 用于压缩文件。例如，`gzip file.txt` 压缩文件。|
|unzip 文件.zip -d 解压到路径|-d 指定解压到路径,默认当前路径|-d 指定解压到路径,默认当前路径|


##  用户管理
| 命令     | 语法                              | 说明                                       |
|----------|-----------------------------------|--------------------------------------------|
| su       | su [用户]                         | 切换用户。如果没有指定用户，则默认切换到超级用户。例如，`su username` 切换到指定用户。|
| who      | who                               | 显示当前登录的用户信息。例如，`who` 显示当前登录用户的信息。|
| whoami   | whoami                            | 显示当前用户的用户名。例如，`whoami` 显示当前用户名。|
| useradd  | useradd [选项] 用户名              | 用于添加新用户。常用选项包括 `-m`（创建用户主目录）、`-g`（指定用户所属的初始组）。例如，`useradd -m -g users newuser` 创建新用户并设置主目录。|
| userdel  | userdel [选项] 用户名              | 用于删除用户。常用选项包括 `-r`（删除用户主目录）。例如，`userdel -r olduser` 删除用户并删除用户主目录。|
| passwd   | passwd [用户]                     | 用于更改用户密码。例如，`passwd username` 更改指定用户的密码。|
| group    | groupadd [选项] 组名              | 用于添加新用户组。例如，`groupadd newgroup` 创建新用户组。|
| mesg     | mesg [y / n]   | 控制是否接受其他用户的写入消息。例如，`mesg n` 禁止接受其他用户的写入消息。|

## 多用户，多设备通信
| 命令   | 语法                                      | 说明                                           |
|--------|-------------------------------------------|------------------------------------------------|
| write  | write 用户名 [终端]                       | 向其他用户发送终端消息。例如，`write user1` 向用户名为 `user1` 的用户发送消息。|
| wall   | wall [文件]                                | 向所有用户发送消息。例如，`wall "系统将在10分钟后重启"` 向所有用户发送系统消息。|
| scp    | scp [选项] 源路径 目标路径                | 用于在本地主机和远程主机之间安全地复制文件或目录。例如，`scp file.txt user@remote:/path/to/destination` 从本地拷贝文件到远程主机。|
| sftp   | sftp [用户@]主机                          | 用于以交互式方式安全地传输文件。进入 sftp 会话后，可以使用类似FTP的命令进行文件传输。例如，`sftp user@remote` 连接到远程主机的sftp服务器。|
| tftp   | tftp [选项] 主机                         | 用于在本地主机和远程主机之间进行简单的文件传输。通常用于无需用户交互的自动化场景。例如，`tftp -g -r file.txt remote` 从远程主机获取文件。|



**有时图形界面消失,别急,可能是切换了控制界面**

虚拟控制台切换快捷键`Alt+Ctel+F1~F6`快速在不同终端切换
或在桌面未启动情况下使用`startx`启动图形桌面环境


## 文件权限和用户权限
| 命令   | 语法                                                | 说明                                      |
|--------|-----------------------------------------------------|-------------------------------------------|
| chmod  | chmod [选项] 权限 文件或目录                       | 更改文件或目录的权限。权限可以使用数字或符号表示。例如，`chmod 755 file.txt` 将文件权限设置为 `-rwxr-xr-x`。|
| chown  | chown [选项] 用户名:组名 文件或目录                | 更改文件或目录的所有者和所属组。例如，`chown user:group file.txt` 将文件所有者设置为 `user`，所属组设置为 `group`。|
| umask  | umask [新掩码]                                      | 设置文件创建时的默认权限掩码。例如，`umask 022` 设置新文件默认权限为 `-rw-r--r--`。|
| ./     | ./可执行文件                                       | 执行当前目录下的可执行文件。例如，`./my_program` 执行当前目录下名为 `my_program` 的可执行文件。|

## 常用快捷键
| 快捷键          | 描述                                              | 示例                                                      |
|-----------------|---------------------------------------------------|-----------------------------------------------------------|
| `Ctrl + C`      | 中断当前运行的命令                                | 例如，运行一个长时间的命令，按下 `Ctrl + C` 中断执行。     |
| `Ctrl + Z`      | 暂停当前进程并放入后台（后续使用 `bg` 恢复）       | 例如，运行一个进程，按下 `Ctrl + Z` 暂停进程。              |
| `Ctrl + D`      | 注销当前会话或者结束输入（在命令行中输入时有效） | 例如，输入 `exit` 或者 `logout`，然后按下 `Ctrl + D`。      |
| `Ctrl + A`      | 光标移动到行首                                    | 在编辑命令时，将光标移动到输入行的开头。                   |
| `Ctrl + E`      | 光标移动到行尾                                    | 在编辑命令时，将光标移动到输入行的末尾。                   |
| `Ctrl + U`      | 删除光标之前的文本                                | 删除光标所在位置之前的所有文本。                          |
| `Ctrl + K`      | 删除光标之后的文本                                | 删除光标所在位置之后的所有文本。                          |
| `Ctrl + W`      | 删除光标前的单词                                  | 删除光标所在位置之前的一个单词。                          |
| `Ctrl + Y`      | 粘贴被删除的文本                                  | 将之前使用 `Ctrl + U`、`Ctrl + K` 或 `Ctrl + W` 删除的文本粘贴回来。|
| `Ctrl + L`      | 清屏                                              | 清空终端屏幕。                                            |
| `Ctrl + R`      | 搜索命令历史                                      | 按下后，输入关键字，终端会自动搜索并显示匹配的历史命令。 |
| `Ctrl + P`      | 上一条命令                                        | 显示上一条执行过的命令。                                  |
| `Ctrl + N`      | 下一条命令                                        | 显示下一条执行过的命令。                                  |
| `Ctrl + T`      | 交换光标位置前的两个字符                          | 将光标前的两个字符进行位置交换。                          |
| `Alt + Backspace`| 删除光标前的单词                                  | 与 `Ctrl + W` 类似，用于删除光标前的一个单词。            |
| `Ctrl + Alt + F1 to F6` | 切换虚拟终端（文本控制台）                  | 切换到不同的虚拟终端。常用于在文本模式下进行操作。       |
| `Ctrl + Alt + F7` | 切换回图形界面（如果有）                        | 从文本控制台切换回图形用户界面。                         |


# 内置工具


## vim
| 快捷键              | 描述                                       |
|---------------------|--------------------------------------------|
| `i`                 | 进入插入模式（在光标前插入文本）           |
| `I`                 | 进入插入模式（在当前行的开头插入文本）     |
| `a`                 | 进入插入模式（在光标后插入文本）           |
| `A`                 | 进入插入模式（在当前行的末尾插入文本）     |
| `o`                 | 在当前行下方插入新行                       |
| `O`                 | 在当前行上方插入新行                       |
| `Esc`               | 退出插入模式（回到普通模式）               |
| `dd`                | 删除当前行                                 |
| `dw`                | 删除当前单词（从光标位置开始）             |
| `D`                 | 删除光标位置到行末                         |
| `x`                 | 删除当前光标位置的字符                     |
| `u`                 | 撤销上一步操作                             |
| `Ctrl + r`          | 重做上一步被撤销的操作                     |
| `yy`                | 复制当前行                                 |
| `yw`                | 复制当前单词（从光标位置开始）             |
| `p`                 | 粘贴剪贴板内容到光标后                     |
| `P`                 | 粘贴剪贴板内容到光标前                     |
| `:w`                | 保存文件                                   |
| `:q`                | 退出Vim（只有在没有修改的情况下生效）     |
| `:wq` 或 `ZZ`       | 保存并退出Vim                              |
| `/pattern`          | 向前搜索指定模式                           |
| `?pattern`          | 向后搜索指定模式                           |
| `n`                 | 查找下一个匹配项                           |
| `N`                 | 查找上一个匹配项                           |
| `:set nu`           | 显示行号                                   |
| `:set nonu`         | 隐藏行号                                   |
| `:set hlsearch`     | 高亮显示搜索结果                           |
| `:set nohlsearch`   | 取消高亮显示搜索结果                       |
| `:set paste`        | 进入粘贴模式（用于粘贴代码）               |
| `:set nopaste`      | 退出粘贴模式                               |
| `:q!`               | 强制退出Vim（放弃修改）                     |


## sftp
sftp基于ssh,互传文件太好用了
| 命令   | 语法     | 说明       |  
|--------|-------|--------------|  
|sftp [user@]hostname| 连接到远程SFTP服务器|`sftp [name666@]192.168.6.66`|                         |
| put    | put [本地文件路径] [远程目录路径]           | 将本地文件上传到远程服务器的指定目录。     |  
| get    | get [远程文件路径] [本地目录路径]           | 从远程服务器下载文件到本地的指定目录。     |  
| mget   | mget [远程文件列表]                         | 从远程服务器下载多个文件到本地。           |  
| mput   | mput [本地文件列表]                         | 将多个本地文件上传到远程服务器。           |  
| rename | rename [原远程文件路径] [新远程文件路径]   | 重命名远程服务器上的文件。                  |  
| rm     | rm [远程文件路径]                          | 删除远程服务器上的文件。                      |  
| rmdir  | rmdir [远程目录路径]                        | 删除远程服务器上的空目录。                    |  
| mkdir  | mkdir [远程目录路径]                        | 在远程服务器上创建新目录。                   |  
| ls     | ls [远程目录路径]                          | 列出远程服务器上的文件和目录列表。            |  
| lcd    | lcd [本地目录路径]                          | 更改本地工作目录。                             |  
| cd     | cd [远程目录路径]                          | 更改远程工作目录。                             |  
| pwd    | pwd                                       | 显示当前远程工作目录的路径。                  |  
| lpwd   | lpwd                                      | 显示当前本地工作目录的路径。                  |  
|rename |在远程服务器上重命名或移动文件|rename oldpath newpath|
| help   | help [命令名] 或 ? [命令名]               | 显示SFTP命令的帮助信息或特定命令的详细说明。 |  
| exit   | exit                                      | 退出SFTP会话。                                 |



## git
| 命令                         | 描述                                       |
|------------------------------|--------------------------------------------|
| `git init`                   | 在当前目录初始化一个新的Git仓库             |
| `git clone <repository>`      | 克隆远程仓库到本地                         |
| `git add <file>`             | 将文件添加到暂存区                         |
| `git add .`                  | 将所有修改过的文件添加到暂存区             |
| `git commit -m "message"`    | 提交暂存区的文件到本地仓库，并添加提交信息 |
| `git status`                 | 显示工作目录的状态                         |
| `git log`                    | 查看提交日志                               |
| `git branch`                 | 列出本地分支                               |
| `git branch <branch-name>`   | 创建新分支                                 |
| `git checkout <branch>`      | 切换到指定分支                             |
| `git merge <branch>`         | 合并指定分支到当前分支                     |
| `git pull`                   | 从远程仓库拉取并合并                       |
| `git push`                   | 推送本地分支到远程仓库                     |
| `git remote -v`              | 查看远程仓库列表                           |
| `git remote add <name> <url>`| 添加远程仓库                               |
| `git diff`                   | 查看工作目录和暂存区的文件差异             |
| `git diff HEAD`              | 查看工作目录和最新提交的文件差异           |
| `git reset <file>`           | 从暂存区中移除文件                         |
| `git reset --hard HEAD`      | 恢复到最新提交                             |
| `git pull origin <branch>`   | 从远程仓库拉取并合并指定分支               |
| `git push origin <branch>`   | 推送本地分支到远程仓库的指定分支           |
| `git tag <tag-name>`         | 创建标签                                   |
| `git fetch`                  | 从远程仓库拉取变更，但不合并               |
| `git checkout -- <file>`     | 撤销工作目录中文件的修改                   |
| `git rm <file>`              | 从版本库中删除文件                         |
| `git remote show <remote>`   | 显示远程仓库的详细信息                     |
| `git stash`                  | 将当前工作目录的修改暂存起来               |
| `git stash apply`            | 恢复最近一次暂存的工作目录修改             |
| `git config --global <key> <value>` | 设置全局配置信息                    |

### 提交文件:
要将一个文件夹（如myproject及其内部所有文件）上传到GitHub，你需要遵循以下步骤：

1. 创建GitHub仓库
访问 GitHub.com 并登录你的账户。
点击页面右上角的加号图标，选择 "New repository"。
输入你的仓库名称（例如 myproject），并选择其他设置（是否公开、是否初始化仓库等）。
点击 "Create repository" 按钮创建仓库。
2. 在本地安装Git
如果你还没有安装Git，你需要先安装它。访问 Git官网 下载并安装适合你操作系统的Git版本。

3. 初始化Git仓库
打开命令行界面（在Windows上是CMD或PowerShell，在Mac或Linux上是终端），导航到你的myproject文件夹，并运行以下命令来初始化Git仓库：

```bash
cd path/to/myproject  
git init
#创建一个名为.git的子文件夹，用于存储Git的所有必要信息,像提交版本记录
```

4. 添加文件到Git仓库
使用git add命令将你的所有文件添加到Git仓库：

```bash
git add .
# 这里的.表示当前目录下的所有文件和子目录。
```

5. 提交更改
使用git commit命令提交你的更改：

```bash
git commit -m "第一次 commit"
# 这里的-m选项后面跟的是你的提交信息，用于描述这次提交的内容。
```
6. 连接到远程仓库
使用git remote命令将你的本地仓库与GitHub上的远程仓库连接起来：

```bash
git remote add origin https://github.com/your-username/myproject.git
# your-username你的GitHub用户名，myproject替换为你提前创建好的仓库名称。
```

7. 推送代码到远程仓库
最后，使用git push命令将你的本地仓库推送到远程仓库：

```bash
git push -u origin master
# 如果仓库使用的是main分支而不是master分支，那么你应该将上面的命令中的master替换为main(时代遗留问题)
```

注意事项：
- 分支名：GitHub的新仓库默认使用main作为主分支，而不是传统的master。确保你推送的分支名与远程仓库的主分支名一致。
- 大文件处理：避免推送大文件到Git仓库。如果需要存储大文件，考虑使用Git LFS（Large File Storage）。
- 敏感信息：不要推送包含敏感信息（如密码、私钥等）的文件到公共仓库。使用.gitignore防止提交这些敏感信息
```bash
# 忽略所有.log文件  
*.log  
  
# 忽略所有.env文件，通常包含敏感的环境变量  
*.env  
  
# 忽略node_modules目录（如果你使用Node.js）  
node_modules/  
  
# 忽略所有编译生成的文件和目录  
build/  
dist/  
```
提交.gitignore文件到Git仓库
现在可以将.gitignore文件添加到Git仓库并提交更改：

```bash
git add .gitignore  
git commit -m "Add .gitignore to exclude sensitive files and directories"
```
- 提交冲突解决：如果在推送代码时遇到冲突，要先拉取远程仓库的最新代码，解决冲突后再推送
```bash
git pull origin master
git add <冲突的文件>  
git commit -m "Resolved merge conflict with remote updates"
```
解决冲突并提交冲突后,再次更新推送
```bash
git push origin master
```


### 回退版本

查看 Git 项目的提交历史并回退到指定的版本，通常以下步骤操作：

1. 查看提交历史
首先，你可以使用 git log 命令来查看项目的提交历史。这将会列出所有的提交，包括每个提交的哈希值、提交者、提交日期和提交信息。

```bash
git log
# commit 3c1111111111111102904be38 (HEAD -> master)为该次提交哈希值
```
简洁地查看log
```bash
git log --oneline
```
2. 找到要回退的提交
从 git log 的输出中，找到你想要回退到的提交的哈希值或者引用（比如 HEAD~n，其中 n 是你想要回退到的提交之前的提交数）。

3. 使用 git reset 回退到指定提交
一旦你找到了要回退的提交的哈希值或引用，你可以使用 git reset 命令来回退到那个提交。注意，git reset 会改变你的当前分支的 HEAD 指针，并可能改变工作目录中的文件。

如果你想保留工作目录和暂存区的更改，可以使用 --soft 选项：

```bash
git reset --soft <commit-hash>
```
如果你还想丢弃暂存区的更改，但保留工作目录中的文件，可以使用 --mixed默认保留

```bash
git reset <commit-hash>
```
如果你还想丢弃工作目录中的更改，使文件回到指定提交时的状态，可以使用 --hard 选项：

```bash
git reset --hard <commit-hash>
```
警告：使用 --hard 选项会丢弃工作目录和暂存区的所有更改，这通常是不可逆的。确保在执行此操作之前，你已经备份了所有重要的更改。

4. 推送更改（如果需要）
如果你已经推送了之前的提交到远程仓库，并且你想要远程仓库也反映你的回退操作，你需要使用 git push 命令，并带上 --force 或 --force-with-lease 选项来强制推送你的更改。

bash
git push origin <branch-name> --force
或者更安全的：

bash
git push origin <branch-name> --force-with-lease
--force-with-lease 会在推送之前检查远程引用是否仍然指向你上次拉取时它所指向的对象。如果不是，它会拒绝推送，从而防止你覆盖其他人的工作。

再次警告：强制推送会覆盖远程仓库的历史记录，这可能会影响其他协作者的工作。确保你了解这一操作的后果，并与其他协作者沟通好。

最后，请谨慎使用 git reset 和 git push --force，因为它们会改变项目的历史记录

## apt apt-get
apt和apt-get类似,apt-get在apt上发展而来,常用apt-get
国内使用源可能有问题,出现问题建议换源(清华源有时只给教育网用,不是很推荐)
备份原有的源文件：在进行任何更改之前，建议备份原有的源文件。使用以下命令进行备份：

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list_bak
# 编辑源文件：使用文本编辑器（如nano、vim等）打开源文件。例如，使用nano编辑器：
```
更改好后要刷新一些apt配置
```bash
sudo apt update
```
检查新的源是否生效

```bash
apt-cache policy <package-name>
# 将<package-name>替换为你想检查的软件包名称。命令的输出将显示该软件包的可用版本及其来源
```

## gcc/g++
gcc是对c语言文件进行链接编译为可执行文件的编译器。
gcc也可以编译c++文件，但是在linux上可能会出现无法链接c++库的现象，通常编译c++使用g++，参数含义与gcc一致

预处理、编译、汇编、链接和运行
``` bash
vi reverse. c
gcc -E reverse.c -o reverse.i
gcc -S reverse.i -o reverse.s
gcc -c reverse.s -o reverse.o
gcc reverse.o -o reverse
./reverse
```

对于头文件引用，需要事先将库文件编译文可执行文件，再进行打包，使用gcc进行包文件和目标c文件进行连接编译为单一可执行文件
```bash
gcc -c reverse-m c
ar -cvr libreverse.a reverse-mo
gcc -c reverse.c
gcc -o reverse reverse.o 1ibreverse.a
./reverse
```

常用编译执行
```bash
if ($?) { g++ c.cpp -o c } ; if ($?) { .\c }
```

```bash
if ($?) { g++ c.cpp -o c }：
```
这一行表示如果上一个命令的退出状态为0（即成功），则执行下面花括号中的命令。
具体命令是使用C++编译器 g++ 编译一个名为 c.cpp 的C++源文件，并将输出的可执行文件命名为 c。
```bash
if ($?) { .\c }：
```
同样，这一行表示如果上一个命令的退出状态为0（即编译成功），则执行下面花括号中的命令。运行当前目录下的可执行文件 c。


或者编写markfile文件自动化编译
```bash
palind:palind.opalind-moreverse-mo
        gcc palind. palind-m o reverse-m o -o palind
palind-mo:palind-mc
        gcc -c palind-m c
palind.o:palind.c
        gcc -c palind.c
reverse-mo:reverse-mc
        gcc -c reverse-m c
```




g++可能会出现编码格式错误，出现显示乱码
当使用g++编译时，确保在编译命令中加上参数 -fexec-charset=utf-8，以确保支持 UTF-8 编码。另外，你也可以设置终端的字符集为 UTF-8。

例如：

```bash
g++ your_file.cpp -o your_output -fexec-charset=utf-8
```
这个参数告诉编译器将输出文件的字符集设置为 UTF-8。

如果在终端中运行程序时还是出现乱码，可以尝试设置终端的字符集为 UTF-8。在大多数终端中，可以通过执行以下命令来设置：

```bash
export LANG=en_US.UTF-8
```
或者，如果你使用的是 Windows 的 CMD 终端，可以使用以下命令：

```bash
chcp 65001
```
这将设置终端的代码页为 UTF-8。请注意，不同的终端和操作系统可能需要不同的设置方式
### 调试c,c++文件 gdb
在linux下调试c文件可以使用gdb 









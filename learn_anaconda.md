[TOC]


# Anaconda和虚拟环境

## anaconda和miniconda配环境
**miniconda**   下载60mb左右
1. 包含conda。一个版本python
2. 体积小

**Anaconda**    下载560mb以上
_占空间几G到几十G，目前我的win上34G_

1. 包含miniconda所有内容
2. 包含很多数据分析科学技术算包
3. 包含jupyter notebook和常用包及lab
4. 包含一个经常出bug卡的要死的，QT写的图形管理界面Anaconda Navigator

![Alt text](./img/1.jpg)

**安装**

官网下载
- <a href="https://www.anaconda.com/download/">anconda下载</a>

- <a href="https://docs.conda.io/en/latest/miniconda.html">miniconda下载</a>
  
*安装路径最好是全英文，尽量全ASCII码，不能有空格、中文*

**设置环境变量**

**win**
 
- 进入控制面板 `win+r` `control`
- 搜索 编辑系统变量
- 环境变量
- 系统变量下的path 新建
- 添加anconda的安装目录，Scripts，library\bin 
  如:`E:\Anaconda3`
`E:\Anaconda\Scripts`
`E:\Anaconda\Library\bin`
- cmd 输入conda -v测试安装和设置是否成功

**linux**
_miniconda_
- 在用户路径创建miniconda文件夹 `mkdir miniconda`
- 进入这个文件夹 `cd miniconda`
- 查看机器架构根据版本选择对应安装包 `uname -m` 这里使用`x86`版本
- 使用wget清华源下载比官网更快 `wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh`
- 执行程序安装 `bash Miniconda3-latest-Linux-x86_64.sh` 中途记得输入yes
- conda初始化 `conda init`
- 重启终端后 输入conda -v测试安装和设置是否成功
  
以后使用Anaconda Prompt进入终端时自动进入base环境
如果要取消自动进入base环境`conda config --set auto_activate_base false`

**换源**
查看conda当前源 `conda config --show-sources`
添加想安装源：
`conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/`
删除刚刚装的安装源：
`conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/`


顺手换pip源`pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`
或者每次下载时添加源地址
`pip install 要下的包名 -i https://pypi.tuna.tsinghua.edu.cn/simple`
对于pytorch还要添加pytorch自己的源
`conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/`

关于conda下载源的文件保存在.condarc中,也可以直接修改该配置文件进行配置

## conda和虚拟环境操作

| conda操作 | 命令 |
| :----:| :---: |
|查看已有虚拟环境|conda env list|
|查看已有虚拟环境|conda info -e|
|创建环境 |conda create --name myenv python=3.9|
|进入环境|conda activate myenv|
|退出环境|conda deactivate|
|conda下载包|conda install 包名==版本号|
|删除环境及环境里所有包|conda remove -n myenv --all|
|更新包|conda update 包名|
|搜索指定包|conda search 包名|
|导出当前环境的conda包|conda env export > requirements.yaml|
|创建环境并载入conda包|conda env create -f requirements.yaml|
|查看帮助信息|conda -h|


|pip操作|命令|
|:-----:|:-------:|
|当前环境包|pip list|
|通过requirements批量安装|pip -r requirements|
|pip下载包|pip install 包名==版本号|
|更新包|pip install --upgrade 包名|
|搜索指定包|pip search 包名|
|查看包信息|pip show 包名|
|提取当前环境pip包|pip freeze > requirements.txt|
|进入虚拟环境后导入pip包|pip install -r requirements.txt|
|查看帮助信息|pip -h|


> 小技巧 可以使用管道符过滤需要的信息。比如查找jupyter相关的包，可以这样:
```bash
pip list |findstr "jupyter"
conda list|findstr "jupyter"
```



conda install和pip install的安装位置

> conda install xxx：这种方式安装的库都会放在`anaconda3/pkgs`目录下，这样的好处就是，当在某个环境下已经下载好了某个库，再在另一个环境中还需要这个库时，就可以直接从pkgs目录下将该库复制至新环境而不用重复下载。
> pip install xxx：分两种情况
> - 一种情况就是当前conda环境的python是conda安装的，和系统的不一样，那么xxx会被安装到`anaconda3/envs/myenv/lib/python3.x/site-packages`文件夹中
> - 如果当前conda环境用的是系统的python，那么xxx会通常会被安装到`~/.local/lib/python3.x/site-packages`文件夹中 

因此要分开导出和导入包，并且先用conda创建环境导入

## conda和pip的区别

1. conda可以管理非python包，pip只能管理python包。
2. conda自己可以用来创建环境，pip不能，需要依赖virtualenv之类的。
3. conda安装的包是编译好的二进制文件，安装包文件过程中会自动安装依赖包；pip安装的包是wheel或源码，装过程中不会去支持python语言之外的依赖项。
4. conda安装的包会统一下载到一个目录文件中，当环境B需要下载的包，之前其他环境安装过，就只需要把之间下载的文件复制到环境B中，下载一次多次安装。pip是直接下载到对应环境中。
5. conda只能在conda管理的环境中使用，例如比如conda所创建的虚环境中使用。
6. pip可以在任何环境中使用，在conda创建的环境 中使用pip命令，需要先安装pip（conda install pip ），然后才可以 环境A 中使用pip
7. conda 安装的包，pip可以卸载，但不能卸载依赖包，pip安装的包，只能用pip卸载

当混用时，可能会在某个环境中安装一个包，出现以下打印信息，导致无法安装对应版本
```bash
Collecting Django==1.10.6 
Using cached Django-1.10.6-py2.py3-none-any.whl
```

这里“Using cached Django ...” 的意思就是Django安装包已经（在base环境或者别的环境中）之前安装过了，在缓存中有安装包，所以就不会重新下载，而是直接利用了。
解决办法，删掉 ~/anaconda3/pkgs/cache 目录下的所有缓存文件

**不要混用conda和pip，尽量使用conda**

## 一些报错处理
1. 


解决方法：


--
# jupyter notebook

# 换源
## conda换源
### Windows下
1. conda源更换为北京外国语大学

Anaconda 是一个用于科学计算的 Python 发行版，支持 Linux, Mac, Windows, 包含了众多流行的科学计算、数据分析的 Python 包。
Windows 用户无法直接创建名为 .condarc 的文件，可先执行 conda config --set show_channel_urls yes 生成该文件之后再修改。

TUNA 还提供了 Anaconda 仓库与第三方源（conda-forge、msys2、pytorch等，查看完整列表）的镜像，各系统都可以通过修改用户目录下的 .condarc 文件:

```bash
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.bfsu.edu.cn/anaconda/cloud
  msys2: https://mirrors.bfsu.edu.cn/anaconda/cloud
  bioconda: https://mirrors.bfsu.edu.cn/anaconda/cloud
  menpo: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.bfsu.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.bfsu.edu.cn/anaconda/cloud
```
2. 注意如果需要pytorch, 还需要添加pytorch的镜像：

```bash
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/pytorch/
```
3. 如果需要换回conda的默认源，直接删除channels即可，命令如下：

`conda config --remove-key channels`
### Linux下
将以上配置文件写在~/.condarc中
```bash
vim ~/.condarc

channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.bfsu.edu.cn/anaconda/cloud
  msys2: https://mirrors.bfsu.edu.cn/anaconda/cloud
  bioconda: https://mirrors.bfsu.edu.cn/anaconda/cloud
  menpo: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.bfsu.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.bfsu.edu.cn/anaconda/cloud
```
补充：

不要使用清华源，清华源教育网好使，非教育网不好使

上海交通大学开源镜像站

```bash
channels:
  - https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/main/
  - https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/free/
  - https://mirrors.sjtug.sjtu.edu.cn/anaconda/cloud/conda-forge/
ssl_verify: true
```

## pip换源
1、临时使用
```bash
pip install xxxx -i https://mirrors.bfsu.edu.cn/pypi/web/simple --trusted-host mirrors.bfsu.edu.cn

清华源 -i https://pypi.tuna.tsinghua.edu.cn/simple
```
注意，simple 不能少, 是 https 而不是 http

2、永久设定
编辑 pip 的配置文件 pip.conf，将 index-url 修改为镜像站的地址。

pip 的配置文件一般位于（如果没有该文件，请直接创建）：
```
· Unix/Linux:   $HOME/.pip/pip.conf
· macOS:        $HOME/Library/Application Support/pip/pip.conf
· Windows:      %APPDATA%\pip\pip.ini
```
修改后的 pip 配置文件示例如下：
```bash
[global]
index-url = https://mirrors.bfsu.edu.cn/pypi/web/simple
format = columns
trusted-host = mirrors.bfsu.edu.cn
```
当 pip 和 pip3 并存时，只需修改 ~/.pip/pip.conf。

使用 pip 时如果出现 configparser.MissingSectionHeaderError: File contains no section headers.，说明 pip.conf 没有加上 [global] 这一行。

补充：


永久换源

```bash
阿里云镜像源
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
临时换源安装matplotlib

pip install -i https://mirrors.aliyun.com/pypi/simple/ matplotlib 
```




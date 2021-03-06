+++
date = "2019-02-20T19:25:43+08:00"
draft = true
title = "linux工具使用"

+++


## linux必装软件：
    sudo apt install curl vim-gnome git cmake nethogs \
        unity-tweak-tool python-pip shadowsocks polipo
    sudo -H pip2 install --upgrade pip


## 配置中文环境
    locale 查看当前环境
    locale -a 查看可使用的环境列表
    sudo apt install language-pack-zh-hans 安装中文语言包
    sudo bash -c 'echo "LC_ALL=zh_CN.UTF-8" >> /etc/default/locale'


    sudo apt install curl

## c++ environment
    sudo apt install build-essential cmake



## 安装docker
    curl -sSL https://get.daocloud.io/docker | sh
    写在docker:
        sudo apt remove docker docker-engine
    安装 Docker Compose:
        sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
        sudo chmod +x /usr/local/bin/docker-compose
    安装方式见:http://get.daocloud.io/

    Error:
        Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.36/version: dial unix /var/run/docker.sock: connect: permission denied
        添加当前用户至docker组(非root用户使用docker，需要添加docker组):
        sudo usermod -aG docker maxu
        cat /etc/group | grep ^docker
        注销重新登录即可

## 安装Kitematic(docker的gui工具)
    https://github.com/docker/kitematic/releases/download/v0.17.3/Kitematic-0.17.3-Ubuntu.zip


## install download tool: mwget
    wget http://jaist.dl.sourceforge.net/project/kmphpfm/mwget/0.1/mwget_0.1.0.orig.tar.bz2
    tar -xjvf mwget_0.1.0.orig.tar.bz2
    cd mwget_0.1.0.orig
    ./configure
    error:
        configure: error: The pkg-config script could not be found or is too old.
    sudo apt install -y pkg-config
    error:
        No package 'openssl' found
    sudo apt install libssl-dev
    ./configure
    error:
        Your intltool is too old.  You need intltool 0.35.0 or later.
    sudo apt install intltool
    make
    sudo make install


## 安装gimp
    sudo add-apt-repository ppa:otto-kesselgulasch/gimp
    sudo apt install gimp

## 安装gparted: 磁盘管理,开机引导
    sudo apt install gparted
    sudo gparted

## 安装谷歌浏览器，并使用代理
    sudoapt install chromium-browser
    chromium-browser --proxy-server=socks5://127.0.0.1:1080

## 安装wine:
     sudo add-apt-repository ppa:wine/wine-builds && sudo apt update
     sudo apt install --install-recommends winehq-staging
## 卸载wine
     1).卸载wine主程序，在终端里输入：
        sudoapt remove --purge wine
     2).然后删除wine的目录文件：
        rm -r ~/.wine
     3).卸载残留不用的软件包：
        sudoapt autoremove

## 安装qq:
    https://phpcj.org/wineqq/
## 卸载qq:
    rm -rf ~/.wine
    rm -rf ~/.local/share/applications/wine-QQ.desktop
    rm -rf ~/.local/share/icons/hicolor/256x256/apps/QQ.png

## install python3.6
    wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
    tar -xvf Python-3.6.2.tar.xz
    cd Python-3.6.2
    ./configure
    make
    make install


## 安装shadowsocks的加速服务kcptun:
    https://github.com/kuoruan/shell-scripts/raw/master/kcptun/kcptun.sh
    chmod +x kcptun.sh
    ./kcptun.sh
    这里配置的端口是:10086

    下载客户端:



## 安装virtualbox
    ubuntu:
        sudo apt install virtualbox virtualbox-ext-pack virtualbox-guest-additions-iso
        sudo usermod -a -G vboxusers peak
        sudo reboot now

    virtualBox虚拟机报错NS_ERROR_FAILURE, 可能是刚升级了内核,virtualBox的内核驱动没有成功被加载, 重启virtualbox服务即可:
    sudo systemctl restart virtualbox.service

    下载地址:https://www.virtualbox.org/wiki/Downloads
    看不到usb3设备?下载下面的插件:
    http://download.virtualbox.org/virtualbox
    【管理】->【全局设定】->【扩展】,选择扩展文件后,就安装成功了
    还要在【usb设备】中选择usb3.0控制器

    下载了usb3的驱动(不知道是否真的需要):http://www.displaylink.com/downloads/ubuntu
    下面三个需要测一测是否需要,我是添加了:
    sudo groupadd usbfs
    sudo adduser maxu vboxusers
    sudo adduser maxu usbfs

    重启本机之后,就发现有了


## 安装kde桌面:
    sudo apt-get install kubuntu-desktop
    报错:
    Errors were encountered while processing:
    /var/cache/apt/archives/kde-config-telepathy-accounts_4%3a15.12.3-0ubuntu1_amd64.deb
    E: Sub-process /usr/bin/dpkg returned an error code (1)
    解决:
    sudo dpkg -P unity-scope-gdrive account-plugin-google account-plugin-facebook
    sudo apt-get install -f

    中文:
    sudo apt-get install language-pack-zh-hant language-pack-zh-hans
    sudo apt-get install kde-l10n-zhcn
    sudo apt-get install ttf-wqy-*


    sudo apt purge kubuntu-desktop
    sudo apt autoremove

## 安装xfce4:
    sudo apt install xfce4


## 安装截图工具:
    sudo add-apt-repository ppa:dhor/myway
    sudo apt update
    sudo apt install hotshots


## polipo ss代理转为http/https代理
    sudo apt install -y polipo
    修改配置文件/etc/polipo/config

        # 设置本地代理地址
        proxyAddress = "::0"

        # 设置ss代理地址和端口
        socksParentProxy = "localhost:1080"
        socksProxyType = socks5

    sudo systemctl start polipo

    设置环境(polipo默认的port是8123):
    export http_proxy=http://127.0.0.1:8123
    export https_proxy=http://127.0.0.1:8123

    测试(这里应该会看到你的代理服务器的ip)
    curl ip.gs


## 流量监控软件
    https://www.linuxidc.com/Linux/2018-01/150604.htm
    sudo apt install nethogs
    sudo apt install iftop
    sudo apt install vnstat

    sudo nethogs
    显示所有应用程序及其进程号及网速

    用命令iftop来检查带宽使用情况. netstat用来查看接口统计报告,还有top监控系统当前运行进程.
    但是如果你想要找一个能够按进程实时统计网络带宽利用率,那么NetHogs就是你所需要的唯一工具

### ubuntu16安装jdk-8
    这个时候jdk10预览版都出来了,可是ubuntu16还是不能成功安装openjdk-9-jdk,
    执行sudo apt install openjdk-8-jdk后未成功,所以
    sudo apt install openjdk-8-jdk,
    java -version, 显示jdk9, 是个错误版本,未安装成功的jdk9,
    sudo update-alternatives --config java, 选择java-8

### 安装openvpn
    sudo apt install openvpn -y

### centos安装lsb_release
    yum provides */lsb_release
    yum install -y lsb_release

### centos安装nginx
    vim /etc/yum.repos.d/nginx.repo
    yum clean all && yum makecache
    yum install -y nginx

### wine3安装
    sudo dpkg --add-architecture i386
    wget -nc https://dl.winehq.org/wine-builds/Release.key
    sudo apt-key add Release.key
    sudo apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/
    sudo apt-get update
    sudo apt-get install --install-recommends winehq-stable

    wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks
    chmod +x winetricks
    sudo mv winetricks /usr/local/bin


### aria2使用:
    sudo apt -y install aria2
    sudo yum install aria2 -y

    aria2c --conf-path=<PATH>

    JSON-RPC Path:
        http://token:123@localhost:6800/jsonrpc

### apt设置代理
    sudo vim /etc/apt/apt.conf:
        Acquire::http::Proxy "http://127.0.0.1:8123";
        Acquire::https::Proxy "http://127.0.0.1:8123";


 # 载入公钥
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
# 安装ELRepo
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
# 载入elrepo-kernel元数据
yum --disablerepo=\* --enablerepo=elrepo-kernel repolist
# 查看可用的rpm包
yum --disablerepo=\* --enablerepo=elrepo-kernel list kernel*
# 安装最新版本的kernel
yum --disablerepo=\* --enablerepo=elrepo-kernel install -y kernel-ml.x86_64

# 删除旧版本工具包
yum remove kernel-tools-libs.x86_64 kernel-tools.x86_64
# 安装新版本工具包
yum --disablerepo=\* --enablerepo=elrepo-kernel install -y kernel-ml-tools.x86_64


## cadence安装
这些库都是cadence安装需要的环境配置
    yum install ksh libXext.so.6 libXtst.so.6 libXt.so.6 –y
    yum install libGLU.so.1 --setopt=protected_multilib=false
    yum install libelf.so.1  libXrender.so.1 libXp.so.6 -y libXrandr.so.2 *xorg* libXp ld-linux.so.2 openmotif libstdc++.so.5 xterm –y

下面这些库是装MMSIM需要的
yum install -y gcc gcc-c++ ksh csh libXp *xorg-X11-fonts* compat-libstdc++-33.i686
yum install -y alliance-libs alliance glibc-2.12-1.107.el6.i686 glibc-devel.i686 glibc
    ##没有：yum install -y compat-readline5-5.2-17.1.el6.i686
    ##没有：yum install -y xterm-253-1

安装yum-axelget插件
yum-axelget 是 EPEL 提供的一个 yum 插件。使用该插件后用 yum 安装软件时可以并行下载，大大提高了软件的下载速度，减少了下载的等待时间:
    sudo yum install yum-axelget

https://www.jianshu.com/p/436391d31d7f

ELRepo:
The Community Enterprise Linux Repository (ELRepo)提供一些硬件驱动，包括显卡、声卡、网卡等。其homepage上有安装指南。
sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm

Nux Dextop:

安装dnf
wget http://springdale.math.ias.edu/data/puias/unsupported/7/x86_64/dnf-conf-0.6.4-2.sdl7.noarch.rpm
wget http://springdale.math.ias.edu/data/puias/unsupported/7/x86_64//dnf-0.6.4-2.sdl7.noarch.rpm
wget http://springdale.math.ias.edu/data/puias/unsupported/7/x86_64/python-dnf-0.6.4-2.sdl7.noarch.rpm
yum install python-dnf-0.6.4-2.sdl7.noarch.rpm  dnf-0.6.4-2.sdl7.noarch.rpm dnf-conf-0.6.4-2.sdl7.noarch.rpm

查看依赖
yum whatprovides libstdc++.so.6

多版本控制
update-alternatives


mplayer没有声音:
    mknod /dev/dsp c 14 3
    chmod 666 /dev/dsp


    ## centos7 opencv3.4.1编译
    yum install gcc gcc-c++
    yum install cmake
    yum install python-devel numpy
    yum install gtk2-devel
    yum install libdc1394-devel
    yum install libv4l-devel
    yum install gstreamer-plugins-base-devel

    安装ffmpeg
    https://trac.ffmpeg.org/wiki/CompilationGuide/Centos


## centos7安装chrome-gnome-shell:
    yum install gtk3-devel.x86_64
    pip install PyGObject
    git clone git://git.gnome.org/chrome-gnome-shell
    cd chrome-gnome-shell
    mkdir out && cd out
    cmake -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_EXTENSION=OFF ../
    make && sudo make install


    vi ~/.lftp/rc:
        set ftp:charset GBK
        set file:charset UTF-8
        set ftp:passive-mode no

## 编译amule:
    yum install -y make automake autoconf gettext zlib-devel wxGTK-devel gcc gcc-c++ kernel-headers binutils-devel bison libupnp

先编译crypto++:
git clone https://github.com/weidai11/cryptopp.git
cd cryptopp
make -j4
sudo make install

可以选择编译libpng:
git clone https://github.com/glennrp/libpng.git
cd libpng
./autogen.sh
mkdir out && cd out
../configure
make -j4
sudo make install

wget https://jaist.dl.sourceforge.net/project/amule/aMule/2.3.2/aMule-2.3.2.tar.xz
tar -xvf aMule-2.3.2.tar.xz
cd aMule-2.3.2
./autogen.sh
mkdir out && cd out
../configure --enable-profile --enable-optimize --enable-geoip --enable-wxcas --enable-mmap --with-boost --enable-wxcas --enable-cas --enable-alcc --enable-alc --enable-amule-daemon --enable-amulecmd --enable-amule-gui --enable-webserver
make -j4

报错:
ClientCreditsList.cpp:315:10: error:
.... has no member named ‘DEREncode’
   pubkey.DEREncode(asink);
解决:
https://github.com/amule-project/amule/pull/120/commits/d1d1368c7909ffd8423730afaa811ce7b6a3a8aa

make -j4


多版本:
yum install centos-release-scl-rh

安装GCC&GCC-C++：yum install devtoolset-3-gcc devtoolset-3-gcc-c++

这里面devtoolset-3是第3个版本，目前针对CentOS6&7支持3，4，6三个版本，分别对应GCC4.9，GCC5.3，GCC6.2，用户可以根据自己的需要选择安装哪一个版本，当然可以同时安装多个版本

切换:
source /opt/rh/devtoolset-3/enable

源码安装的gcc的卸载:
cd build/gcc
sudo make uninstall

blas-devel gcc-c++ gcc-gfortran gobject-introspection-devel lapack-devel libquadmath-devel libtool pygobject3-devel vtk-devel xorg-x11-drv-wacom-devel xorg-x11-server-devel xorg-x11-util-macros



ubuntu18.04添加 WineHQ signing key and repository:
sudo dpkg --add-architecture i386
wget -qO- https://dl.winehq.org/wine-builds/Release.key | sudo apt-key add -
sudo apt-add-repository 'deb http://dl.winehq.org/wine-builds/ubuntu/ xenial main'
安装stable WineHQ:
sudo apt-get install --install-recommends winehq-stable


ubuntu安装dia做流程图
sudo apt install dia-common

Dia 无法输入中文:
用 vim 打开 /usr/bin/dia 将内容改成下面这样
dia-normal "$@"


## ssh工具 putty
    sudo apt install putty -y


## gcp 拷贝工具


## audacity 声音录制

## 串口工具
    cutecom picocom

## chrome 插件: 百度下载工具
    baidu-dl
    执行: aria2c --enable-rpc

## python 升级
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt update && sudo apt install -y python3.7
    
    cd /usr/lib/python3/dist-packages
    sudo ln -s apt_pkg.cpython-{35m,37m}-x86_64-linux-gnu.so
    
    sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
    sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
    
    sudo update-alternatives --config python3

## install lastest pip
    curl https://bootstrap.pypa.io/get-pip.py | sudo -H python3

## ubuntu nvidia graphics drivers
    sudo apt purge nvidia*
    sudo add-apt-repository -y ppa:graphics-drivers && sudo apt update
    sudo apt install nvidia-410
    
## ubuntu bison flex
    sudo apt install bison flex

## 源码安装qemu
    # 参考https://wiki.qemu.org/Hosts/Linux
    sudo apt purge "qemu*" && sudo apt autoremove -y && sudo apt install checkinstall -y && sudo apt build-dep qemu -y
    下载[qemu-4.0.0](https://download.qemu.org/qemu-4.0.0.tar.xz)
    tar -xvf qemu-4.0.0.tar.xz && cd qemu-4.0.0
    ./configure --enable-debug && make -j11
    sudo checkinstall make install
    # sudo apt install ./*.deb

## 安装pipenv
    curl https://raw.githubusercontent.com/kennethreitz/pipenv/master/get-pipenv.py | python

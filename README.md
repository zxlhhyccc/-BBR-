# -BBR-

借鉴Linux-NetSpeed的一键脚本，通过修改debian的内核，安装最新版本的debian内核，并开启魔改版的BBR和暴力魔改版bbr

方法：

1、修改版本号，如最新版本（4.9.140）：kernel_version="4.9.140"

2、修改下载最新内核，如版本号（4.9.140）：

wget -N --no-check-certificate http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.140/linux-headers-4.9.140-0409140_4.9.140-0409140.201811231231_all.deb

wget -N --no-check-certificate http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.140/linux-headers-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb

wget -N --no-check-certificate http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.140/linux-image-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb

3、修改安装内核名称，如版本号（4.9.140）：

dpkg -i linux-headers-4.9.140-0409140_4.9.140-0409140.201811231231_all.deb

dpkg -i linux-headers-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb

dpkg -i linux-image-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb

4、安装gcc-4.9版本（debian9默认安装gcc-6.3，因此需要添加使用Debian 8的源）：

vi /etc/apt/sources.list

deb http://ftp.us.debian.org/debian/ jessie main contrib non-free

deb-src http://ftp.us.debian.org/debian/ jessie main contrib non-free

:wq

5、安装gcc-4.9

apt-get update

apt-get install gcc-4.9 g++-4.9 g++-4.9-multilib

6、该脚本默认安装的内核是（4.9.140），如果仅使用该内核，直接运行：

wget -N --no-check-certificate "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/tcp.sh"  && chmod +x tcp.sh && ./tcp.sh 


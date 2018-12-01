# 魔改版的BBR和暴力魔改版BBR

借鉴Linux-NetSpeed的一键脚本，通过修改debian的内核，安装最新版本的debian内核，并开启魔改版的BBR和暴力魔改版bbr

方法：

1、修改版本号，如最新版本（4.9.140）：kernel_version="4.9.140"

debian内核版本下载地址：

http://kernel.ubuntu.com/~kernel-ppa/mainline/

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

6、该脚本默认安装的内核是（debian9为4.9.142，centos7为4.19.5-1），如果仅使用该内核，直接运行：

A、不带gcc-4.9菜单需按第5步先安装gcc-4.9的脚本：

wget -N --no-check-certificate "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/bbr.sh"  && chmod +x bbr.sh && ./bbr.sh 

B、带gcc-4.9安装菜单，在安装魔改版内核后，先执行菜单安装gcc-4.9，然后再安装魔改版BBR的一键脚本：

wget -N --no-check-certificate "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/bbr/bbr.sh" && chmod +x bbr.sh && ./bbr.sh

C、centos7和debian9合一安装魔改版BBR内核脚本（菜单安装gcc-4.9为debian专用，centos7不需安装）：

wget -N --no-check-certificate  -O bbr.sh "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/centos7_debian9_bbr.sh" && chmod +x bbr.sh && ./bbr.sh

注意：不知道什么原因，debian9在安装内核后重新运行该脚本可能出现无法下载脚本的现象，为保险起见，安装内核并服务器重启后请先单独运行(./bbr.sh)，或者运行apt upgrade做一次软件包升级，然后就可运行该脚本了。centos7没有此问题。

7、centos7开启魔改版BBR，请使用centos7_bbr.sh,改脚本最新内核已修改为4.9.5-1，如果需升级内核，请比照上述方法修改

wget -N --no-check-certificate "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/centos7_bbr.sh"  && chmod +x centos7_bbr.sh && ./centos7_bbr.sh
-----
centos7内核版本下载地址：

https://elrepo.org/linux/kernel/el7/x86_64/RPMS/

http://mirror.rc.usf.edu/compute_lock/elrepo/kernel/el7/x86_64/RPMS/

# 魔改版的BBR和暴力魔改版BBR

借鉴Linux-NetSpeed的一键脚本，通过修改debian的内核，安装最新版本的debian内核，并开启魔改版的BBR和暴力魔改版bbr

方法：

1、修改版本号，如最新版本（4.9.140）：kernel_version="4.9.140"

debian、ubuntu的内核版本下载地址（4.9.*内核为debian的，4.19.*内核为ubuntu的）：
```
http://kernel.ubuntu.com/~kernel-ppa/mainline/
````
2、修改下载最新内核，如版本号（4.9.140）：
`````
wget -N --no-check-certificate http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.140/linux-headers-4.9.140-0409140_4.9.140-0409140.201811231231_all.deb

wget -N --no-check-certificate http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.140/linux-headers-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb

wget -N --no-check-certificate http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.140/linux-image-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb
``````
3、修改安装内核名称，如版本号（4.9.140）：
````````
dpkg -i linux-headers-4.9.140-0409140_4.9.140-0409140.201811231231_all.deb

dpkg -i linux-headers-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb

dpkg -i linux-image-4.9.140-0409140-generic_4.9.140-0409140.201811231231_amd64.deb
````````
4、安装gcc-4.9版本（debian9默认安装gcc-6.3，因此需要添加使用Debian 8的源）：
````````
vi /etc/apt/sources.list

deb http://ftp.us.debian.org/debian/ jessie main contrib non-free

deb-src http://ftp.us.debian.org/debian/ jessie main contrib non-free

:wq
````````
5、安装gcc-4.9
```````
apt-get update

apt-get install gcc-4.9 g++-4.9 g++-4.9-multilib
````````
6、该脚本默认安装的内核是（debian9为4.9.142，centos7为4.19.5-1），如果仅使用该内核，直接运行：

A、不带gcc-4.9菜单需按第5步先安装gcc-4.9的脚本：
````````
wget -N --no-check-certificate "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/bbr.sh"  && chmod +x bbr.sh && ./bbr.sh 
````````
B、带gcc-4.9和nginx1.14.2安装菜单，在安装魔改版内核后，先执行菜单安装gcc-4.9，然后再安装魔改版BBR的一键脚本：
`````
wget -N --no-check-certificate "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/bbr/bbr.sh" && chmod +x bbr.sh && ./bbr.sh
`````
C、centos7和debian9合一安装魔改版BBR内核脚本（菜单安装gcc-4.9为debian专用且在菜单中对应按照gcc-4.9编译器，centos7不需安装）：
`````
wget -N --no-check-certificate -O bbr.sh "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/centos7_debian9_bbr.sh" && chmod +x bbr.sh && ./bbr.sh
`````
D、centos7、debian9、ubuntu16.04/18.04/18.10三合一安装魔改版BBR内核脚本（增加了安装nginx，且调整了相应菜单）：
`````
wget -N --no-check-certificate -O bbr.sh "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/centos7_debian9_ubuntu18.04_bbr.sh"  && chmod +x bbr.sh && ./bbr.sh
`````
debian内核升级完成后单独卸载无效软件包（也可不卸载）：
`````
sudo apt autoremove -y gettext-base grub-common grub2-common libfreetype6 libfuse2 libpng16-16
`````
ubuntu内核升级完成后单独卸载无效软件包（也可以不卸载）：
``````
sudo apt autoremove -y grub-common grub2-common（两个或两个其中的一个，有提示）
```````
注意：修正了debian9在安装内核后重新运行该脚本可能需要等待一会才能下载脚本问题,增加了设置root用户，再就是,ubuntu16.04需要先安装： libssl1.1。

7、centos7开启魔改版BBR，请使用centos7_bbr.sh,改脚本最新内核已修改为4.9.5-1，如果需升级内核，请比照上述方法修改
`````
wget -N --no-check-certificate -O bbr.sh "https://raw.githubusercontent.com/zxlhhyccc/-BBR-/master/centos7_debian9_ubuntu18.04_bbr.sh" && chmod +x bbr.sh && ./bbr.sh
`````
centos7内核版本下载地址：
````
https://elrepo.org/linux/kernel/el7/x86_64/RPMS/

http://mirror.rc.usf.edu/compute_lock/elrepo/kernel/el7/x86_64/RPMS/
````

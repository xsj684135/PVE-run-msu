# PVE-run-msu

由于HPE只发布了rpm版本的Marvell RAID MSU 
所以我的HPE ProLiant MicroServer Gen10不能在除了Windows和支持rmp的发行版上查看并管理RAID的状态
我安装的PVE8，PVE8是基于Debian12的，所以在网上各种研究，解决了这个rmp转换为deb的方法。仅适用于我个人，只做记录备忘。（理论上别的系统也行 但是esxi并没有试过 有尝试过的可以跟我说说）

另外：github上有大神做了docker的版本 各位可以去看看https://github.com/stegm/marvell_msu_docker

开始：

引用一位德国老哥的：https://blog.florianheinle.de/raid-controller-marvell-88SE9230-hp-microserver-gen10-linux-debian

HPE也有提供 但是这个最新，所以在这里下载：https://support.lenovo.com/de/en/downloads/ds504249

安装alien fakeroot用于转换
apt-get install alien fakeroot

开始转换
fakeroot alien MSU-4.1.10.2042-1.x86_64.rpm
跑完没报错就开始下一步，如果报错的话自己研究研究
![image](https://github.com/xsj684135/PVE-run-msu/assets/50570049/522affaa-b5dc-46b2-892d-9f63385c9910)

跑这个
rpm -qlp --scripts MSU-4.1.10.2042-1.x86_64.rpm

然后跑这个
apt-get install equivs
--------
cat <<EOF >> libssl1.0.0.ctl
Section: misc
Priority: optional
Standards-Version: 3.9.2

Package: libssl-1.0.0
Version: 1.0.1
Description: dummy package to install MSU
 Marvel Storage Utility requires old libssl version
 .
 This is just the fake package to satisfy that dependency
EOF
-----

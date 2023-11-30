# -PVE-MSU
https://blog.florianheinle.de/raid-controller-marvell-88SE9230-hp-microserver-gen10-linux-debian

HPE也有提供 但是这个最新，所以在这里下载：https://support.lenovo.com/de/en/downloads/ds504249

安装alien fakeroot用于转换
apt-get install alien fakeroot

开始转换
fakeroot alien MSU-4.1.0.2032-1.x86_64.rpm


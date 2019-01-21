# Make sure you have git install
apt install git

mkdir wifiDrivers
cd wifiDrivers
Git clone https://github.com/cilynx/rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959
cd rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959
cd rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959
VER=$(sed -n 's/\PACKAGE_VERSION="\(.*\)"/\1/p' dkms.conf)
sudo rsync -rvhP ./ /usr/src/rtl88x2bu-${VER}
sudo ARCH=arm dkms add -m rtl88x2bu -v ${VER}
sudo ARCH=arm dkms build -m rtl88x2bu -v ${VER}
sudo ARCH=arm dkms install -m rtl88x2bu -v ${VER}
sudo modprobe 88x2bu

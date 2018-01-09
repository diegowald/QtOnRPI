# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.


  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/xenial64"
  #config.vm.box = "xenji/ubuntu-17.04-server"
  # config.vm.box = "bento/ubuntu-17.04"
  # config.vm.box = "bento/ubuntu-17.10"
  #config.vm.box_version = "201710.25.0"  

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  #config.vm.network "forwarded_port", guest: 8080, host: 28080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./", "/code"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
     vb.name = "crossCompiler"
     vb.gui = true

   end
  config.disksize.size = "30GB"
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

#config.vm.provision "file", source: "wheezy-raspbian-latest.zip", destination: "/root/opt/wheezy-raspbian-latest.zip"
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
     apt update
     apt upgrade -y
     #apt-get install -y apache2
     #apt-get install -y xfce4
     #apt-get install -y build-essential mesa-common-dev
     #apt-get install -y qt5-default qt5-doc qt5-doc-html qt5-qmake-arm-linux-gnueabihf qt5gstreamer-dbg qt5-gtk-platformtheme qt5-qmltooling-plugins qt5-image-formats-plugins qt5serialport-examples qt5keychain-dev qt5-style-plugins qtcreator
     #apt-get install -y libboost-all-dev libtag1-dev libpulse-dev
     #apt-get install -y qtmultimedia5-dev libqt5multimediawidgets5 libqt5multimedia5-plugins libqt5multimedia5 ffmpeg
     #startxfce4 &
     #echo Downloading Qt
     #wget -c --no-check-certificate -nv https://download.qt.io/archive/qt/5.8/5.8.0/qt-opensource-linux-x64-android-5.8.0.run
     #echo Installing Qt
     #/code/vagrantServer/extract-qt-installer qt-opensource-linux-x64-android-5.8.0.run $PWD/Qt

mkdir ~/opt
cd ~/opt
apt install -y unzip
#wget http://downloads.raspberrypi.org/raspbian_latest -O wheezy-raspbian-latest.zip
# unzip wheezy-raspbian-latest.zip
#mkdir /mnt/rasp-pi-rootfs
#mount -o loop,offset=48234496 2017-11-29-raspbian-stretch.img  /mnt/rasp-pi-rootfs

if [ ! -f /code/wheezy-raspbian-latest.zip ]; then
	wget http://ftp.jaist.ac.jp/pub/raspberrypi/raspbian/images/raspbian-2015-05-07/2015-05-05-raspbian-wheezy.zip  -O wheezy-raspbian-latest.zip
else
	cp /code/wheezy-raspbian-latest.zip ./
fi
unzip wheezy-raspbian-latest.zip
mkdir /mnt/rasp-pi-rootfs
mount -o loop,offset=62914560 2015-05-05-raspbian-wheezy.img  /mnt/rasp-pi-rootfs


wget https://sourceforge.mirrorservice.org/r/rf/rfidmonitor/crosscompilation-resources/gcc-4.7-linaro-rpi-gnueabihf.tbz
tar -xf gcc-4.7-linaro-rpi-gnueabihf.tbz
apt install -y lib32ncurses5 lib32z1

 git clone https://github.com/darius-kim/cross-compile-tools.git

 git clone git://code.qt.io/qt/qt5.git
cd qt5
./init-repository


apt install -y g++
apt install -y build-essential
apt install -y lib32stdc++6
apt-get build-dep -y qt5-default
apt install -y libfontconfig1-dev libdbus-1-dev libfreetype6-dev libudev-dev
apt install -y '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev
apt install -y flex bison gperf libicu-dev libxslt-dev ruby
apt install -y libssl-dev libxcursor-dev libxcomposite-dev libxdamage-dev libxrandr-dev libdbus-1-dev libfontconfig1-dev libcap-dev libxtst-dev libpulse-dev libudev-dev libpci-dev libnss3-dev libasound2-dev libxss-dev libegl1-mesa-dev gperf bison
apt install -y libasound2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev


cd /root/opt/cross-compile-tools
git checkout  d49f517eaa3bc819f78a01a5eead9e1a697ce6f5

. ./fixQualifiedLibraryPaths /mnt/rasp-pi-rootfs/ /root/opt/gcc-4.7-linaro-rpi-gnueabihf/bin/arm-linux-gnueabihf-gcc

cd /root/opt/qt5
git checkout v5.5.1
git submodule update --init --recursive

ln -s /mnt/rasp-pi-rootfs/lib/arm-linux-gnueabihf /lib/
#cp  -r /mnt/rasp-pi-rootfs/lib/arm-linux-gnueabihf /lib/

cd /root/opt/qt5/qtbase/
./configure -no-use-gold-linker -opengl es2 -device linux-rasp-pi-g++ -device-option CROSS_COMPILE=/root/opt/gcc-4.7-linaro-rpi-gnueabihf/bin/arm-linux-gnueabihf- -sysroot /mnt/rasp-pi-rootfs -opensource -confirm-license -optimized-qmake -reduce-exports -release -make libs -prefix /usr/local/qt5pi -hostprefix /usr/local/qt5pi

cd /root/opt/cross-compile-tools
. ./fixQualifiedLibraryPaths /mnt/rasp-pi-rootfs/ /root/opt/gcc-4.7-linaro-rpi-gnueabihf/bin/arm-linux-gnueabihf-gcc
cd /root/opt/qt5/qtbase/
make
make install

cd ../qtimageformats
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtsvg
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtscript
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtxmlpatterns
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtdeclarative
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtsensors
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qt3d
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtgraphicaleffects
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtlocation
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtdocgallery
/usr/local/qt5pi/bin/qmake .
make 
make install




cd ../qtquickcontrols
/usr/local/qt5pi/bin/qmake .
make 
make install


cd ../qtfeedback
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtwebsockets
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtserialport     
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtsystems
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtcanvas3d
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtmultimedia
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qttools
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtconnectivity
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtpim
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qttranslations
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtquick1
/usr/local/qt5pi/bin/qmake .
make 
make install

cd ../qtwebchannel
/usr/local/qt5pi/bin/qmake .
make 
make install


   SHELL
end

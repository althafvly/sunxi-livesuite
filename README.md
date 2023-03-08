This repository contains the latest LiveSuit binary and supporting
kernel module.

LiveSuit is a tool to flash Images to the NAND of Allwinner devices.

For more information on this repository or on this utility, check our
wiki at http://linux-sunxi.org/LiveSuit

## Install dependencies
```
sudo apt-get install dkms git build-essential zlib1g-dev
wget https://ppa.launchpadcontent.net/linuxuprising/libpng12/ubuntu/pool/main/libp/libpng/libpng_1.2.54.orig.tar.xz
tar Jxfv libpng_1.2.54.orig.tar.xz
cd libpng-1.2.54
./configure
make
sudo make install
sudo ln -s /usr/local/lib/libpng12.so.0.54.0 /usr/lib/libpng12.so
sudo ln -s /usr/local/lib/libpng12.so.0.54.0 /usr/lib/libpng12.so.0
```

## Installing the kernel module for usb drivers.
```
git clone https://github.com/linux-sunxi/sunxi-livesuite.git
cd sunxi-livesuite/awusb
sudo make
sudo cp awusb.ko /lib/modules/`uname -r`/kernel/
sudo depmod -a
sudo modprobe awusb
cd ..
```

## Install USB Rules
```
cp awusb/50-awusb.rules /etc/udev/rules.d/50-awusb.rules
sudo udevadm control --reload-rules
```

## Running LiveSuit.
```
sudo bash LiveSuit.sh
```

This will determine whether your system is x86 or x86-64 and will then
start the right binary.

## Flashing your device.

Warning: if you attach your FEL enabled device before you start
LiveSuit, then LiveSuit will not detect it. You need to first start the
LiveSuit application.

First, properly power down the device by either pressing and holding the
power button for about 10 seconds, or by cutting all power in case of
development board.

Start LiveSuit and select an image for flashing, if you haven't already
done so.

Then, hold the FEL button, and power up the device. Either by attaching
the power lead, or by pressing the power button for 1-2s and then
pressing and releasing the power button several times in quick
succession. This will have made your device enter FEL mode.

Now attach the USB OTG lead. LiveSuit should now detect your device and
start flashing.

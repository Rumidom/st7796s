# Orange pi zero 2 W drivers for IPS 3.5 ST7796U SPI screen 
[3.5inch_IPS_SPI_Module_ST7796](https://github.com/Rumidom/st7796s/blob/main/600px-MSP3526-2.jpg)


https://www.lcdwiki.com/3.5inch_IPS_SPI_Module_ST7796

## Install st7796s drivers for Orange pi zero 2 W
Install kernel headers
```
sudo dpkg -i /opt/linux-headers*.deb
```
Then clone repo
```
git clone https://github.com/rumidom/st7796s.git
cd st7796s/kernel_module/
```
Build kernel module and install it
```
make
sudo make install
make clean
sudo depmod -A
sudo bash -c 'echo "fb_st7796s" >> /etc/initramfs-tools/modules'
sudo update-initramfs -u
```
Then install dts and reboot device.
```
cd ../dts/
sudo orangepi-add-overlay sun50i-h618-st7796s-w2.dts
sudo reboot
```
### If you want mirror desktop to screen, follow these instructions

Check framebuffer port
```
ls /dev/fb*
```
Create new file
```
sudo vim /etc/X11/xorg.conf.d/99-fbdev.conf
```
Copy paste this content and remember to change framebuffer port
```
Section "Device"
  Identifier "myfb"
  Driver "fbdev"
  Option "fbdev" "/dev/fb0"
EndSection
```

Orange Pi Zero 2W wiring:
```
MOSI      	PH7 SPI1_MOSI
MISO      	PH8 SPI1_MISO
CLK       	PH6 SPI1_CLK
TFT_CS    	PH5
DC        	PH4 
RST       	PI0
TOUCH_CS  	PH9
TOUCH_IRQ 	PI15
LED       	3.3V
BEEPER		PL2
```

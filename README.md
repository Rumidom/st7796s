# st7796s

## Install st7796s drivers for Orange pi zero 2 W
Install kernel headers
```
sudo dpkg -i /opt/linux-headers*.deb
```
Then clone repo
```
git clone https://github.com/rikovalkonen/st7796s.git
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
5V --> VCC & LED
GND --> GND
PH4 -->  DC/RS
SPI1_CS0 --> CS
SPI1_CS1 --> T_CS
SPI1_MOSI --> T_DIN & SDI(MOSI)
SPI1_MISO --> T_DO
SPI1_CLK --> T_CLK & SCK
TWI2_SDA/UART3_RX --> RESET
PI0 --> T_IRQ

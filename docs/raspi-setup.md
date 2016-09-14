# Initial setup

- Download Raspian
- Format SDHC to FAT32
- Install Raspian on SDHC
- Connect mouse, keyboard, HDMI, and power to raspi 3

# After boot

- Open Menu->Preferences->Raspberry Pi Configuration
  - Open Interfaces tab
  - Enable Camera and Serial (probably I2C and maybe SPI as well)
  - Open Localisation tab
  - Set values for Locale, Timezone, Keyboard, and WiFi Country
  - close and reboot
- Open terminal
  - `sudo apt-get update`
  - `sudo apt-get upgrade`
  - `sudo apt-get install vim`
- Setup WiFi
  - Only need if using raspi 3 and if you wish to connect to your wifi
  - Click network icon in menbar (two computer icon at top-right)
  - Select your network
  - Enter your network password
- Setup static IPv4 address
  - see https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update
  - edit /etc/dhcpcd.conf
    - add `interface eth0\nstatic ip_address=192.168.0.x/24`

# Serial access from mac os

- See https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all
- Get USB Console Cable #954 from Adafruit
- Install PL2303_MacOSX_1_6_0_20151022 driver
- Connect cable to raspi
  - IMPORTANT: determine if USB will power or if you'll provide power
- Connect cable to mac
- Open terminal
- type `screen /dev/cu.usbserial 115200`

# X Windows on mac os

- Install XQuartz from https://www.xquartz.org
- Open terminal
- Shell into raspi
  - `ssh -X pi@192.168.0.1`
- run X app from raspi session
  - for example: `geany &`
  - for example: `idle3 &`
    - You can even run the python scripts for the camera this way but the preview shows on the raspi display, not in x windows

# VNC

- Install VNC server and start it on raspi
  - `sudo apt-get install tightvncserver`
  - `tightvncserver`
  - set password
- Connect from Mac
  - cmd-K
  - vnc://pi@192.168.0.1:5901
  - enter password

# i2c tools

- `sudo apt-get install i2c-tools`

# git

- `ssh-keygen -t rsa -b 4096 -C "kevin@kevlindev.com"`
- `eval "$(ssh-agent -s)"`
- `sudo apt-get install git-gui`
- `git config --global user.email "kevin@kevlindev.com"`
- `git config --global user.name "Kevin Lindsey"`

# Apple File Sharing

- `sudo apt-get install netatalk`
- `sudo /etc/init.d/netatalk stop`
- `sudo vim /etc/netatalk/AppleVolumes.default`
  - Edit last line, if necessary
- `sudo /etc/init.d/netatalk start`
# enclosure-picroft-touch7
This repoistory is to keep track of my efforts to build a Mycroft platform using a Raspberry Pi4 and 7" Touchscreen.

# Hardware
I had a goal to try and keep this project under $150.
Here is a list of suggested hardware items needed to build a picroft-touch7.
- Raspberry Pi4 (4G) - $50 - [microcenter](https://www.microcenter.com/product/609038/raspberry-pi-4-model-b---4gb-ddr4)
- 7" Touchscreen - $60 - [microcenter](https://www.microcenter.com/product/613541/element-14-7-pi-touchscreen-lcd-display)
- Fan Case - $7 - [microcenter](https://www.microcenter.com/product/610384/micro-connectors-acrylic-stackable-raspberry-pi-4-case-with-power-adapter-and-fan)

  Note: Any case will do, but a fan is really needed to avoid overheating, especially when playing videos.
  Note: When you connect the fan to a 3v supply, it tends to be very quiet and is good enough to keep the temperature under 60degC
- Microphone - $30 - [TONOR G11](https://www.tonormic.com/products/tonor-g11-conference-usb-microphone)
  Note: Any microphone should work.  I like this one because of the multidirectional capability, but I've tried others and they work too.
- Stand - $0 - I just 3d printed a simple set of legs.
- Speaker - ?? - I love the Ultimate Ears Boom speakers for playing music.  I already had a few of these around the house, so I am using these.
  Note: Any speaker will work, it just depends on the quality you want.  The Pi4 analog output is not very good, so I'd recommend a BT speaker or add a DAC hat.
  
# Software
I tried many distributions (Lubuntu, Kubuntu, Ubuntu, Majaro, Plasma bigscreen, etc).  All caused issues with overheating and package issues.
Finally, I ended up using a Picroft/Rasbian base.  The problem was the older versions of Qt in buster.  In my case, I went ahead and added the bullseye distros from debian (armhf) to get to the versions needed for all the skills and for mycroft-gui-app.
- Rasbian install - [Raspios - armhf](https://downloads.raspberrypi.org/raspios_full_armhf_latest)
- Debian Bullseye - /etc/apt/sources.list - deb http://deb.debian.org/debian bullseye main contrib non-free
- Then I just did a standard mycroft-core and mycroft-gui download install (git clone, bash dev_setup.sh)
- I added two files in the .config/autostart directory to start the core and gui on boot (pi user autologin)
- Added a lxde-pci-rc.xml file to the ~/.config/openbox directory (/etc/xdg/openbox/lxde-pi-rc.xml), then add lines to the <applications> secton:
    <application title="mycroft.gui">
      <skip_taskbar>yes</skip_taskbar>
      <decor>no</decor>
      <shade>no</shade>
      <layer>normal</layer>
      <fullscreen>yes</fullscreen>
    </application>
- Added skills as needed.




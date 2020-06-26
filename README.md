# enclosure-picroft-touch7
This repoistory is to keep track of my efforts to build a Mycroft platform using a Raspberry Pi4 and 7" Touchscreen.

# Hardware
I had a goal to try and keep this project under $150.
Here is a list of suggested hardware items needed to build a picroft-touch7.
- Raspberry Pi4 (4G) - $50 - [microcenter](https://www.microcenter.com/product/609038/raspberry-pi-4-model-b---4gb-ddr4)
- 7" Touchscreen - $60 - [microcenter](https://www.microcenter.com/product/613541/element-14-7-pi-touchscreen-lcd-display)
- Fan Case - $17 - [microcenter](https://www.microcenter.com/product/610384/micro-connectors-acrylic-stackable-raspberry-pi-4-case-with-power-adapter-and-fan)

  Note: Any case will do, but a fan is really needed to avoid overheating, especially when playing videos.
  Note: When you connect the fan to a 3v supply, it tends to be very quiet and is good enough to keep the temperature under 60degC
- Microphone - $30 - [TONOR G11](https://www.tonormic.com/products/tonor-g11-conference-usb-microphone)

  Note: Any microphone should work.  I like this one because of the multidirectional capability, but I've tried others and they work too.
- SD Card - $8 - 16G is fine. [walmart](https://www.walmart.com/ip/SanDisk-Imaging-Ultra-microSDHC-16GB-UHS-I-Memory-Card/46700581)
- Stand - $0 - I just 3d printed a simple set of legs.
- Speaker - ?? - I love the Ultimate Ears Boom speakers for playing music.  I already had a few of these around the house, so I am using these.

  Note: Any speaker will work, it just depends on the quality you want.  The Pi4 analog output is not very good, so I'd recommend a BT speaker or add a DAC hat.
  
# Software
I tried many distributions (Lubuntu, Kubuntu, Ubuntu, Majaro, Plasma bigscreen, etc).  All caused issues with overheating and package issues.
Finally, I ended up using a Picroft/Rasbian base.  The problem was the older versions of Qt in buster.  In my case, I went ahead and added the bullseye distros from debian (armhf) to get to the versions needed for all the skills and for mycroft-gui-app.
- Rasbian install - [Raspios - armhf](https://downloads.raspberrypi.org/raspios_full_armhf_latest)
- Debian Bullseye - /etc/apt/sources.list - deb http://deb.debian.org/debian bullseye main contrib non-free
- Then I just did a standard mycroft-core and mycroft-gui download and install (git clone, bash dev_setup.sh)
- I added two files in the .config/autostart directory to start the core and gui on boot (pi user autologin)
- Make sure QT_FILE_SELECTORS is set to picroft_touch7 

  .bashrc: export QT_FILE_SELECTORS=picroft_touch7
  In desktop files: Exec=env QT_FILE_SELECTORS=picroft_touch7 mycroft-gui-app --hideTextInput --maximize
  This is so that the skills will use the picroft_touch7 versions of screen layouts.
- Added a lxde-pci-rc.xml file to the ~/.config/openbox directory (/etc/xdg/openbox/lxde-pi-rc.xml), then add lines to the "applications" secton:
```
   <application title="mycroft.gui">
      <skip_taskbar>yes</skip_taskbar>
      <decor>no</decor>
      <shade>no</shade>
      <layer>normal</layer>
      <fullscreen>yes</fullscreen>
    </application>
```
- Modified /etc/mycroft/mycroft.conf to use this enclosure
```
{
  "enclosure": {
     "platform": "picroft_touch7"
  }
}
```

- Added skills as needed.

# Skills
Here is a list of skills and capabilities I wanted to make sure worked on this platform.
*Hey Mycroft*
- What's the weather forcast?
- What’s the weather?
- Play positive encouraging K-Love on IHeartRadio
- Play contemporary on Spotify
- Set a timer for ??? Minutes
- Announce – Dinner is ready
- Add milk to list Safeway
- Turn on den light
- Turn off basement stairs light
- Youtube Nobody by casting crowns
These are the main skills I use and have modified to support the 7" screen
- mycroft-picroft_touch7.mycroftai - a copy of mycroft-mark-2.mycroftai with modifications for display and sound/volume.
- mycroft-playback-control.mycroftai (Modified to use picroft_touch7 UI)
- todoist-skill - Personally developed skill to interact with Todoist
- homeassistant.mycroftai - Added UI capabilities
- mycroft-skill-iheartradio.johnbartkiw - Added UI capabilities
- youtube-skill.aiix - Used as is, but I needed to install several packages and use QtMultimedia 12 instead of 13
- mycroft-spotify.forslund - Used as is
*To Do*
I want to modify these skills to use the 7" screen.
- mycroft-alarm.mycroftai
- mycroft-timer.mycroftai

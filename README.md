# Making Debian suitable for gaming, streaming and video editing distro

 # 1) Use one of these images https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/
https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/
 # 2) Use Rufus(http://rufus.ie/) or whatever software you like to burn the usb stick
 # 3) Boot from the image
 # 4) Select Graphical Installer
 # 5) Install Debian on the desired partition. Make sure to be connected to the internet via cable, as there can be some firmware issues with Wi-Fi drivers!

# 6) Once the installation is complete login using Gnome interface.

# Remember to go into Software and Updates GUI and check the following options : 

* Officially supported (main)
* DFSG-compatible Software with Non-Free Dependencies (contrib)
* Non DFSG-compatible Software (non-free)

# Add security updates later in the updates section via GUI after finishing all these steps:

# Go to Terminal and input: 
* sudo apt-get update
* sudo apt-get upgrade

# 7) Optional,if you typed your password during installation twice as Root and as User:

# Open terminal in activities and add your user, for example test to sudoers file and use the following commands:

* su 
* gedit /etc/sudoers
#User privilege specification
test

# Testing if everything works
# Switch back to test using this command: 

* su  test

# Run the following command: 

* sudo whoami

# Answer should be: 

* root

# NB! If you don’t have the sudo option install sudo under Su:

* su

* apt install sudo

* su 

* gedit /etc/sudoers

#User privilege specification
test

# Switch back to test: 

* su  test

# Run the following command: 

* sudo whoami

# Answer should be:

* root

# 8) Installing Multiarch very important! (you’ll need it for NVIDIA drivers, Steam and other stuff)

* sudo dpkg --add-architecture i386

* sudo apt-get update

* sudo apt-get upgrade 

# 9) Installing NVIDIA drivers:

# First do this just in case:

* sudo apt install nvidia-detect

* sudo nvidia-detect

* sudo apt-get update

# Then install NVIDIA Drivers:

* sudo apt-get install nvidia-driver

# Wait for the installation to finish and reboot, type the following commands after reboot:

* sudo apt-get update

* sudo apt-get upgrade

# NB! There might be a missing firmware errors in the terminal during installtion, usually its Realtek but just to be sure run the following command:

* sudo dmesg 

# Once you are sure use these commands:

* sudo apt-get install firmware-realtek

* sudo apt-get update

# Go to activities menu and type NVIDIA it should give you a GUI.

# 10) Install Steam with the following commands, if you did all the steps before correctly Steam should install without issues:

* sudo apt install steam

# 11) Optional for media playback and vlc install snap:

* sudo apt-get update

* sudo apt install snapd

* sudo snap install vlc

# 12) Optional for streaming install OBS Studio(for HVENC support some additional stuff is required)

* sudo apt install ffmpeg

* sudo apt install obs-studio

* sudo apt-get install smplayer 

* sudo apt-get install libnvidia-encode1 

* sudo apt-get install simplescreenrecorder

# NDI for OBS-Studio download .deb files here:https://github.com/Palakis/obs-ndi/releases/tag/4.7.1

* sudo dpkg -i libndi3_4.0.0-1_amd64.1.deb
* sudo dpkg -i obs-ndi_4.7.1-1_amd64.deb

# 13) Alternative OBS-Studio snap version(Does not support NDI plugin!):

* sudo snap install obs-studio

* sudo apt-get install smplayer 

* sudo apt-get install libnvidia-encode1 

* sudo apt-get install simplescreenrecorder 

# 14) Optional, install Shotcut for video/photo editing:

* sudo snap install shotcut --classic

# 15) Upgrade OS version and install all updates
 
 * sudo apt-get update
 
 * sudo apt-get upgrade
 
 * sudo apt-get dist-upgrade

# 16) Optional install discord app,go to https://discordapp.com/  select Download for Linux choose .deb:
# Open Terminal in Downloads folder and use the following commands:

* sudo apt install gdebi-core
* sudo gdebi discord-0.0.9.deb

# NB! In case of "A start job is running for update the operating system while offline" on Debian-based systems during updates while dual-booting press E then F10 and wait for the update process to finish.

Ok, thank you, happy gaming and streaming on Debian.
Hopefully same settings will work on the future Debian distros!
Enjoy!
#gimalaji_blake

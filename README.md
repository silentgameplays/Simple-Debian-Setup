# Making Debian suitable for gaming, streaming and video editing distro

 # 1) Use one of these images:
 # Free:
https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/
# Non-free
https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/
 # 2) Use Rufus or whatever software you like to create a bootable USB: 
 http://rufus.ie/ 
 
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

# 9) Installing NVIDIA drivers update the sources list if necesary for non-free:
# Updating the sources list with non-free:

* sudo nano /etc/apt/sources.list

* deb http://deb.debian.org/debian distro_name main contrib non-free
* deb-src http://deb.debian.org/debian distro_name main contrib non-free

* deb http://deb.debian.org/debian-security/ distro_name/updates main contrib non-free
* deb-src http://deb.debian.org/debian-security/ distro_name/updates main contrib non-free

* deb http://deb.debian.org/debian distro_name-updates main contrib non-free
* deb-src http://deb.debian.org/debian distro_name-updates main contrib non-free

* sudo apt-get update
* sudo apt-get upgrade

# For testing:
* deb      http://ftp.uk.debian.org/debian/        testing             main non-free contrib
* deb-src  http://ftp.uk.debian.org/debian/        testing             main non-free contrib

# security
* deb      http://security.debian.org              testing-security    main non-free contrib
* deb-src  http://security.debian.org              testing-security    main non-free contrib

# updates
* deb      http://ftp.uk.debian.org/debian/        testing-updates     main non-free contrib
* deb-src  http://ftp.uk.debian.org/debian/        testing-updates     main non-free contrib

# First do this just in case:

* sudo apt install nvidia-detect

* sudo nvidia-detect

* sudo apt-get update

# Then install NVIDIA Drivers:

* sudo apt-get install nvidia-driver

* sudo apt install nvidia-settings vulkan-utils

* sudo apt install libvulkan1 libvulkan-dev vulkan-utils

* sudo apt-get update

* sudo apt-get upgrade

# (Optional) Install newer NVIDIA Drivers via backports on stable:

Add buster-backports to your /etc/apt/sources.list, for example:
* sudo nano /etc/apt/sources.list

# Add this line:
* deb http://deb.debian.org/debian buster-backports main contrib non-free

* sudo apt-get update

* sudo apt-get upgrade

# install the package nvidia-driver.
* sudo apt update

* sudo apt install -t buster-backports nvidia-driver 

* sudo apt-get update

* sudo apt-get upgrade

# Wait for the installation to finish and reboot, type the following commands after reboot:

* sudo apt-get update

* sudo apt-get upgrade

# NB! There might be a missing firmware errors in the terminal during installtion, usually its Realtek but just to be sure run the following command:

* sudo dmesg 

# Once you are sure use these commands:

* sudo apt-get install firmware-realtek

* sudo apt-get update

# Go to activities menu and type NVIDIA it should give you a GUI.

# 10) Gaming section install Steam,Lutris,Wine,DXVK with the following commands, if you did all the steps before correctly Steam should install without issues:

* sudo apt install steam

# Install wget:

* sudo apt install wget

# Get and register Wine key:

* wget -nc https://dl.winehq.org/wine-builds/winehq.key

* sudo apt-key add winehq.key

# Edit the /etc/apt/sources.list file:

* sudo nano /etc/apt/sources.list

# if the Vulkan libs are installed you can install dxvk

* sudo apt install dxvk

# For Testing and Stable do the following: 

# Testing:

* deb https://dl.winehq.org/wine-builds/debian/ distro_name main

* sudo apt install --install-recommends winehq-stable

# Stable: 

* deb https://dl.winehq.org/wine-builds/debian/ distro_name main

# For Stable install Wine via software center or via command: 

* sudo apt install wine

# For Lutris:

* sudo touch /etc/apt/sources.list.d/lutris.list

# Then do this:
* echo "deb http://download.opensuse.org/repositories/home:/strycore/Debian_9.0/ ./" |
# Inside > enter this command:
* sudo tee /etc/apt/sources.list.d/lutris.list

# For any distro to install lutris get the key

* wget -q https://download.opensuse.org/repositories/home:/strycore/Debian_9.0/Release.key -O- | sudo apt-key add -

# Then run:
* sudo apt-get update
* sudo apt-get upgrade
# Finally,install Lutris:

* sudo apt-get install lutris
* sudo apt-get update
* sudo apt-get upgrade

# 11) Optional install snap:

* sudo apt install snapd

# 12) Optional for streaming install OBS Studio(for HVENC support some additional stuff is required)

* sudo apt install ffmpeg

* sudo apt install obs-studio

* sudo apt-get install smplayer 

* sudo apt-get install libnvidia-encode1 

* sudo apt-get install simplescreenrecorder

# NDI for OBS-Studio download .deb files here:
https://github.com/Palakis/obs-ndi/releases/tag/4.7.1

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

# 16) Optional install discord app,go to: 
https://discordapp.com/  
# select Download for Linux choose .deb:
# Open Terminal in Downloads folder and use the following commands:

* sudo apt install gdebi-core
* sudo gdebi discord-0.0.10.deb

# 17) Automount using gnomedisk utility:
# Edit mount options
# Add this line:

nosuid,nodev,nofail,x-gvfs-show,auto

# 18) #(Optional)Benchmarking games on linux got to https://www.phoronix-test-suite.com/?k=downloads and download latest for Debian:
* sudo apt install gdebi-core
# 
* sudo gdebi phoronix-test-suite_*.deb


# NB! In case of "A start job is running for update the operating system while offline" on Debian-based systems during updates while dual-booting press E then F10 and wait for the update process to finish.

Ok, thank you, happy gaming and streaming on pure Debian.
Hopefully same settings will work on the future Debian distros!
Enjoy!
#gimalaji_blake

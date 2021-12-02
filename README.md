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

* sudo apt update

# Then install NVIDIA Drivers:
* sudo apt install nvidia-driver firmware-misc-nonfree  nvidia-settings libvulkan-dev nvidia-vulkan-icd vulkan-tools  vulkan-validationlayers vulkan-validationlayers-dev
* 
* sudo apt update

* sudo apt upgrade

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
* sudo apt install wine
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

# 12) Optional for streaming/recording install OBS Studio(for NVENC support some additional stuff is required)

* sudo apt install ffmpeg

* sudo apt install libnvidia-encode1 

* sudo apt install nvidia-cuda-toolkit

* sudo apt install flatpak

* sudo apt install mingw-w64 

* sudo apt install ffmpeg2theora  flvmeta  mencoder  mjpegtools x265 x264 nvidia-vdpau-driver mpv mpg123 libxvidcore4


# With GNOME Software store(for point and click installs)

* apt install gnome-software-plugin-flatpak

* flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

* flatpak install flathub com.obsproject.Studio

# NDI for OBS-Studio download .deb files here:
https://github.com/Palakis/obs-ndi/releases/tag/4.7.1

* sudo dpkg -i libndi3_4.0.0-1_amd64.1.deb
* sudo dpkg -i obs-ndi_4.7.1-1_amd64.deb

# 13) Optional, install Shotcut for video/photo editing:

* flatpak install flathub org.shotcut.Shotcut

# 14) Upgrade OS version and install all updates
 
 * sudo apt-get update
 
 * sudo apt-get upgrade
 
 * sudo apt-get dist-upgrade

# 15) Optional install discord app,go to: 
https://discordapp.com/  
# select Download for Linux choose .deb:
# Open Terminal in Downloads folder and use the following commands:

* sudo apt install gdebi-core
* sudo gdebi discord-0.0.10.deb

# 16) Automount using gnomedisk utility:
# Edit mount options
# Add this line:

nosuid,nodev,nofail,x-gvfs-show,auto

# 17) #(Optional)Benchmarking games on linux got to https://www.phoronix-test-suite.com/?k=downloads and download latest for Debian:
* sudo apt install gdebi-core
# 
* sudo gdebi phoronix-test-suite_*.deb
# (100% Optional NB!Might cause issues) upgrading the kernel via backports
* sudo nano /etc/apt/sources.list - 
Add this line: 
* deb http://deb.debian.org/debian buster-backports main 
* sudo apt update 
* sudo apt -t buster-backports install linux-image-amd64 
* sudo reboot

# 18) Creating a bootable Windows 10 USB using Disks utility (Possible on any linux distro even without GNOME)
* Download a Windows image from MS link below:
* https://www.microsoft.com/en-us/software-download/windows10
* Insert USB Drive
* Launch Disks Utility
* Select your USB Drive and in the top right=corner click the menu select Format Disk
* In Partitioning select Compatible with modern systems and hard disks>2TB (GPT)
* Click Format wait for it to finish 
* Click Partition>For Use with Windows(NTFS) (in Volume label type Windows or ESD)
* Mount the USB and Open it
* Go to the place where you downloaded Windows 10 ISO and select Open with Disk Image Mounter
* Open Copy everything from the Windows 10 ISO and paste into your USB Drive,wait for it to finish(takes a while)
# (Optional) Install shadowplay as an obs plugin
* # Get nvidia-patch: https://github.com/keylase/nvidia-patch
* Extract and go to the folder
* Open in terminal
* sudo ./patch-fbc.sh
* # Get obs-nvfbc: https://gitlab.com/fzwoch/obs-nvfbc
* Extract and go to folder
* Open in terminal 
* sudo apt-get install libgl-dev libobs-dev libsimde-dev meson ninja-build
* meson build
* ninja -C build
* Go back to GUI and copy nvfbc.so
* Enable hidden files and fodlers
* Go to /home/user/.config/obs-studio
* Create the following folders plugins->nvfbc->bin->64bit
* paste nvfbc.so into 64bit
* Go to OBS Studio and add the NvFBC Source to your scene
# NB! In case of "A start job is running for update the operating system while offline" on Debian-based systems during updates while dual-booting press E then F10 and wait for the update process to finish.

Ok, thank you, happy gaming and streaming on pure Debian.
Hopefully same settings will work on the future Debian distros!
Enjoy!
# Credit for compilation goes to gimalaji_blake

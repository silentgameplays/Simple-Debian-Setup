# Debian-Stretch-Setup-for-gaming-and-streaming
Complete tutorial on how to setup a pure Debian Stretch 9.9.0 Distro to play games and stream with OBS and create awesome videos with Shotcut.
Making Debian Stretch 9.9.0 suitable for gaming, streaming and video editing distro

 1) Use this image https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/
 2) Use Rufus or whatever software you like to burn the usb stick
 3) Boot from the image
 4) Select Graphical Installer
 5) Install Debian Stretch 9.9.0 on the desired partition. Make sure to be connected to the internet via cable, as there can be some firmware issues with Wi-Fi drivers!
 6) Once the installation is complete login using Gnome interface.
Remember to go into Software and Updates GUI and check the following options : 
* Officially supported (main)
* DFSG-compatible Software with Non-Free Dependencies (contrib)
* Non DFSG-compatible Software (non-free)
Add security updates later in the updates section via GUI after finishing all these steps:

Go to Terminal and input: 
* sudo apt-get update

7) Open terminal in activities and add your user, for example test to sudoers file and use the following commands:

* Su 
* adduser test
* usermod -aG sudo test

Testing if everything works

Switch back to test using this command: 
* su  test

Run the following command: 

* sudo whoami

Answer should be: 
* root

NB! If you don’t have the sudo option install sudo under Su:
* Su
* apt install sudo
* adduser test
* usermod -aG sudo test

Switch back to test: 
* su  test

Run the following command: 
* sudo whoami

Answer should be:
* root

8) Installing Multiarch very important! (you’ll need it for NVIDIA drivers, steam and other stuff)
* sudo dpkg --add-architecture i386
* sudo apt-get update
* sudo apt-get upgrade 
9) Installing NVIDIA drivers:
First do this just in case:
* sudo apt install nvidia-detect
* sudo nvidia-detect
* sudo apt-get update
Then do this:
* sudo apt-get install nvidia-driver

Wait for the installation to finish and reboot, type the following commands after reboot:
* sudo apt-get update
* sudo apt get upgrade

NB! There might be a missing firmware errors in the terminal during installtion, usually its Realtek but just to be sure run the following command:
* sudo dmesg 
Once you are sure use these commands:
* sudo apt-get install firmware-realtek
* sudo apt-get update
Go to activities menu and type NVIDIA it should give you a GUI.

10) Install Steam with the following commands, if you did all the steps before correctly Steam should install without issues:
* sudo apt install steam

11) Optional for media playback and vlc install snap:
* sudo apt-get update
* sudo apt install snapd
* sudo snap install vlc

12) Optional for streaming install OBS Studio

* sudo apt install ffmpeg
* sudo apt install obs-studio

Alternative:

* sudo snap install obs-studio

13) Optional install shotcut for video/photo editing:

* snap install shotcut –classic

14) Optional adding and mounting a disk to Debian 9.9.0
 Make sure to format the desired disk in the GUI Disks section to Ext4:

Then name the disk like ”disk1” and go to Terminal and use the following commands:
* sudo gedit /etc/fstab 

Input the following line at the bottom of the file:
* /dev/sdc /disk1 ext4 defaults 1 2

Save and run the following commands:
* sudo mount /dev/sdc/ disk1
* sudo apt-get update

Ok, thank you, happy gaming and streaming on Debian Stretch 9.9.0.
Hopefully same settings will work on the future Debian distros!
Enjoy!
#gimalaji_blake

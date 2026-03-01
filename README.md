# Making Debian suitable for gaming, streaming and video editing distro
**Optional doing a fresh wipe before installing Debian,use Live Boot option:**
**Formatting the SSD/HDD properly before installing Debian or any other Linux distribution or operating system:**

* ``sudo cfdisk /dev/sda``
* ``sudo cfdisk /dev/nvme0n1``
  
**Delete everything you see then Write>>Yes**

**Wiping the partition schemes:**

* ``sudo wipefs -a /dev/sda``
* ``sudo wipefs -a /dev/nvme0n1``
  
**Deleting everything properly so no forencisc recovery is possible:**

* ``sudo shred -f -v /dev/sda``
* ``sudo shred -f -v /nvme0n1``

**Without seeing progress:**
* ``sudo shred /dev/sda``
* ``sudo shred /dev/nvme0n1``

**Deleting everything the fast way:**
* ``sudo blkdiscard -f /dev/sda``
* ``sudo blkdiscard -f /dev/nvme0n1``

# 1. Use one of the provided images for Debian:
 https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/

# 2. Use Rufus or whatever software you like to create a bootable USB: 
 http://rufus.ie/ 
 
# 3. Boot from the image
 
# 4. Select Graphical Installer
 
# 5. Install Debian on the desired partition. Make sure to be connected to the internet via cable, as there can be some firmware issues with Wi-Fi drivers!

**Once the installation is complete login into the prefered Desktop Environment"**

**Remember to go into Software and Updates GUI and check the following options:**

* Officially supported (main)
* DFSG-compatible Software with Non-Free Dependencies (contrib)
* Non DFSG-compatible Software (non-free)

**Add security updates later in the updates section via GUI or sources list after finishing all these steps:**

**Go to Terminal and input:** 

* ``sudo apt update``
* ``sudo apt upgrade``

**Or:**

* ``sudo apt update && sudo apt upgrade``

**(Optional)if you typed your password during installation twice as Root and as User:**

# Open terminal in activities and add your user, for example test to sudoers file and use the following commands:

* ``su``

* ``gedit /etc/sudoers``

**User privilege specification**

* ``user``

**Test if everything works**
**Switch back to test using this command:**

* ``su  user``

**Run the following command:** 

* ``sudo whoami``

**Answer should be:** 

* root

**NB!If you don’t have the sudo option install sudo under su:**

* ``su``

* ``apt install sudo``

* ``su`` 

* ``gedit /etc/sudoers``

**Or:** 

* ``nano /etc/sudoers``

**User privilege specification**

* user

**Switch back to user:** 

* ``su  user``

**Run the following command:**

* ``sudo whoami``

**Answer should be:**

* root

# 6. Updating the /etc/apt/sources list with additional non-free repositiories, this changes depending on the Debian version:**

* ``sudo nano /etc/apt/sources.list``

* deb http://deb.debian.org/debian trixie main non-free-firmware
* deb-src http://deb.debian.org/debian trixie main non-free-firmware

* deb http://deb.debian.org/debian-security/ trixie-security main non-free-firmware
* deb-src http://deb.debian.org/debian-security/ trixie-security main non-free-firmware

* deb http://deb.debian.org/debian trixie-updates main non-free-firmware
* deb-src http://deb.debian.org/debian trixie-updates main non-free-firmware

* deb http://deb.debian.org/debian trixie contrib non-free
* deb-src http://deb.debian.org/debian trixie contrib non-free 

* ``sudo apt update && sudo apt upgrade``

**For testing:**

* deb      http://ftp.uk.debian.org/debian/ testing main non-free contrib
* deb-src  http://ftp.uk.debian.org/debian/ testing main non-free contrib

**security**

* deb      http://security.debian.org testing-security main non-free contrib
* deb-src  http://security.debian.org testing-security main non-free contrib

**updates**

* deb      http://ftp.uk.debian.org/debian/ testing-updates main non-free contrib
* deb-src  http://ftp.uk.debian.org/debian/ testing-updates main non-free contrib

# New debian.sources.list:

* ``sudo nano /etc/apt/sources.list.d/debian.sources``

# For current stable Trixie:

* ``Types: deb deb-src``
* ``URIs: https://deb.debian.org/debian``
* ``Suites: trixie trixie-updates``
* ``Components: main non-free-firmware``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

* ``Types: deb deb-src``
* ``URIs: https://security.debian.org/debian-security``
* ``Suites: trixie-security``
* ``Components: main non-free-firmware``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

# With contrib non-free:

* ``Types: deb deb-src``
* ``URIs: https://deb.debian.org/debian``
* ``Suites: trixie trixie-updates``
* ``Components: main non-free-firmware contrib non-free``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

* ``Types: deb deb-src``
* ``URIs: https://security.debian.org/debian-security``
* ``Suites: trixie-security``
* ``Components: main non-free-firmware contrib non-free``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``


# With backports:

* ``Types: deb deb-src``
* ``URIs: https://deb.debian.org/debian``
* ``Suites: trixie trixie-updates``
* ``Components: main non-free-firmware contrib non-free trixie-backports ``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

* ``Types: deb deb-src``
* ``URIs: https://security.debian.org/debian-security``
* ``Suites: trixie-security``
* ``Components: main non-free-firmware contrib non-free trixie-backports ``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

# Testing

* ``Types: deb deb-src``
* ``URIs: https://deb.debian.org/debian``
* ``Suites: forky forky-updates``
* ``Components: main non-free-firmware contrib non-free``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

* ``Types: deb deb-src``
* ``URIs: https://security.debian.org/debian-security``
* ``Suites: forky-security``
* ``Components: main non-free-firmware contrib non-free``
* ``Enabled: yes``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``


# SID

* ``Types: deb``
* ``URIs: https://deb.debian.org/debian/``
* ``Suites: sid``
* ``Components: main contrib non-free non-free-firmware``
* ``Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg``

# 7. Adding Multiarch is very important! 
**(You will need it for AMD and NVIDIA drivers,Vulkan,Steam,Lutris,Heroic and other gaming related things)**

* ``sudo dpkg --add-architecture i386``

* ``sudo apt update && sudo apt upgrade``

**If not installed (should be on Trixie)**

* ``sudo apt install firmware-misc-nonfree``

**For Intel CPU's:** 

* ``sudo apt install intel-microcode``

**For AMD CPU's(if not installed):**

* ``sudo apt install amd64-microcode``

* ``sudo update-initramfs -c -k all``

* ``sudo apt update && sudo apt upgrade``

# 8. Installing NVIDIA and AMD Drivers update the sources list if necesary for non-free:

**First do this just in case:**

* ``sudo apt install nvidia-detect``
* ``sudo nvidia-detect``
* ``sudo apt update && sudo apt upgrade``

**Then install linux headers and NVIDIA Drivers or AMD Drivers:**

**x64 bit**

* ``sudo apt install linux-headers-amd64``

**x32 bit**
  
* ``sudo apt install linux-headers-686``

**PAE x32bit**

* ``sudo apt install linux-headers-686-pae``

**For NVIDIA Choose one of the two options**

**(Option 1)Install the proprietary NVIDIA drivers with dependencies like vulkan,etc:**

* ``sudo apt install nvidia-kernel-dkms nvidia-driver nvidia-settings libvulkan-dev nvidia-vulkan-icd vulkan-tools  vulkan-validationlayers``
* ``sudo apt update && sudo apt upgrade``

**(Option 2)Install the open NVIDIA  drivers for RTX GPU's with dependencies like vulkan**

* ``sudo apt install nvidia-open-kernel-dkms nvidia-driver nvidia-settings libvulkan-dev nvidia-vulkan-icd vulkan-tools  vulkan-validationlayers``
* ``sudo apt update && sudo apt upgrade``

**Additional stuff For NVIDIA Only:**

* ``sudo apt install libnvidia-encode1``

* ``sudo apt install libnvidia-fbc1``

* ``sudo apt install nvidia-cuda-toolkit``

**Wayland support for NVIDIA:**

* ``sudo nano /etc/default/grub``

**Find:** ``GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume"``

**Change to:** ``GRUB_CMDLINE_LINUX_DEFAULT="quiet nvidia-drm.modeset=1 nvidia-drm.fbdev=1 splash resume"``

* ``sudo update-grub``

* ``sudo update-initramfs -u``

* ``sudo reboot``

**Check if it worked:**
  
* ``sudo cat /sys/module/nvidia_drm/parameters/modeset``

**(Optional) Install newer NVIDIA Drivers via backports on stable:**

**Add distroname-backports to your** ``/etc/apt/sources.list`` **,for example:**

* ``sudo nano /etc/apt/sources.list``

**Add this line:**

* deb http://deb.debian.org/debian distro_name-backports main contrib non-free
* deb-src http://deb.debian.org/debian distro_name-backports main contrib non-free

* ``sudo apt update && sudo apt upgrade``

**Install the package nvidia-driver.**

* ``sudo apt update && sudo apt upgrade``
* ``sudo apt install -t distro_name-backports nvidia-driver nvidia-settings libvulkan-dev nvidia-vulkan-icd vulkan-tools  vulkan-validationlayers vulkan-validationlayers-dev``

* ``sudo apt update && sudo apt upgrade``

**(100% Optional) Might cause issues upgrading the kernel via backports:**

* ``sudo nano /etc/apt/sources.list``

**Add this line:**

* deb http://deb.debian.org/debian trixie-backports main

**Run:**

* ``sudo apt update && sudo apt upgrade``
* ``sudo apt -t trixie-backports install linux-image-amd64``
* ``sudo apt update && sudo apt upgrade``
* ``sudo reboot``

**Wait for the installation to finish and reboot, type the following commands after reboot:**

* ``sudo apt update``

* ``sudo apt upgrade``
  
**Or:**

* ``sudo apt update && sudo apt upgrade``


**NB! There might be missing firmware errors in the terminal during installtion, usually its Realtek but just to be sure run the following command:**

* ``sudo dmesg`` 

**Once you are sure use these commands:**

* ``sudo apt-get install firmware-realtek``

* ``sudo apt update && sudo apt upgrade``

**Go to activities menu and type NVIDIA it should give you a GUI now on both Wayland and X11.**

**AMD GPU Drivers installation with dependencies for gaming, you will need the x32 bit architecture from one of the previous steps enabled** 

* ``sudo apt install firmware-amd-graphics libgl1-mesa-dri libgl1-mesa-dri:i386 libglx-mesa0 libglx-mesa0:i386 mesa-vulkan-drivers mesa-vulkan-drivers:i386 xserver-xorg-video-all``

* ``sudo apt update && sudo apt upgrade``

**(Optional) On some kernels it is posible to experience GPU hangs because of ring 0 issues.Check AMD GPUs for ring 0 issues**
* ``sudo journalctl -b -1 -o cat --no-pager | grep "amdgpu: ring"``
* ``sudo journalctl -b -2 -o cat --no-pager | grep "amdgpu: ring"``
* ``sudo journalctl -b -0 -o cat --no-pager | grep "amdgpu: ring"``

**If all is normal then the response will be normal, issues will look like an error with "ring ... timeout","ring vcn...timeout" or "ring comp... timeout" or "ring gfx... timeout"**
**To fix the ring 0 issues user needs to remove any overclocking in BIOS,another way is revert to 6.12 LTS stable kernel version,other way is to install LACT, and set Performance Level to Manual, and the Power Profile Mode to 3D_FULL_SCREEN permanently**

**Increase vm.max_map_count to Steam Deck values to prevent games crashing:**

* ``sudo nano /etc/sysctl.d/99-sysctl.conf``

* **Add**:``vm.max_map_count = 2147483642``

* ``sudo sysctl --system``

* ``sudo reboot``

* ``cat /proc/sys/vm/max_map_count``

**Enable VRR (freesync/gsync) Support for GNOME**

* ``gsettings set org.gnome.mutter experimental-features "['variable-refresh-rate']"``

**Exit the current Wayland session, re-login and type to check, the output should be "variable-refresh-rate"**

* ``gsettings get org.gnome.mutter experimental-features``

**Disable VRR for GNOME**
* ``gsettings set org.gnome.mutter experimental-features "[]"``

**Exit the current Wayland session, re-login and type to check, the output should be "[]"**

* ``gsettings get org.gnome.mutter experimental-features``

**Disable the annoying Force Quit pop up on GNOME:**

**60 seconds**

* ``gsettings set org.gnome.mutter check-alive-timeout 60000``

**Never check***
* ``gsettings set org.gnome.mutter check-alive-timeout 0``
**Disable notification sounds on GNOME DE**
* ``gsettings set org.gnome.desktop.sound event-sounds false``

# 8. Gaming section install Steam,Lutris,Wine with the following commands, if you did all the steps before correctly then Steam should install without issues:

* ``sudo apt install steam lutris wine wine32 wine64 libwine libwine:i386 fonts-wine scummvm dosbox ``

**For Steam it's optional to add main user to video and audio groups**

* ``sudo usermod -a -G video,audio,adm user``

**(Optional) Additional dependencies for Wine/Gaming:**

* ``sudo apt install gvfs:i386 wine32-preloader:i386 wine64-preloader wine-binfmt gstreamer1.0-libav:i386 gstreamer1.0-plugins-bad:i386 gstreamer1.0-plugins-ugly winetricks gstreamer1.0-tools:i386 opus-tools:i386 gstreamer1.0-alsa gamemode timidity gstreamer1.0-plugins-ugly:i386``

* ``sudo apt install fizmo-sdl2 libsdl2-2.0-0 libsdl2-dev libsdl2-gfx-1.0-0 libsdl2-gfx-dev libsdl2-image-2.0-0 libsdl2-mixer-2.0-0 libsdl2-net-2.0-0``

* ``sudo apt install mingw-w64 flvmeta smpeg-plaympeg lame mjpegtools x265 x264 mpv mpg123 libxvidcore4 fluidsynth``

**(Optional) Mono package for NET framework support on Linux**

* ``sudo apt install mono-complete``

**Steam package has issues launching on Debian 13 Trixie even after instlaling all of the required dependencies, how to fix**

1. Install ``steam`` package and try to launch from GUI
2. Launch terminal and type ``steam``
3. Go into Steam Settings select toggle Interface>Run Steam when my computer starts,see picture:
<img width="1906" height="467" alt="Screenshot_20250907_064032" src="https://github.com/user-attachments/assets/aa360317-98d6-43a7-a420-9c286bad680c" />
4. Steam should start automatically another option is to use the terminal to launch the Steam client every time.


**Another way to fix Steam not launching from GUI**
1. Install steam package and try to launch from GUI
2. Launch terminal and type steam
3. Go into Steam Settings select toggle Enable GPU accelerated rendering in web views, you need to Disable this setting.
4. Steam should start automatically another option is to use the terminal to launch the Steam client every time.

**(Optional) Install Glourious Eggroll Proton GE the easy way:**

 * Download the latest release here: https://github.com/GloriousEggroll/proton-ge-custom/releases
 * Extract,enable hidden files and folders 
 * Create a folder in your /home/user/steam/root/compatibilitytools.d if it does not exist.
 * Copy/paste the extracted GE folder into /home/user/config/.steam/root/compatibilitytools.d
 * Restart Steam,enjoy the custom GE build
 
**(Optional) Opensource games:**

* ``sudo apt install supertux supertuxkart wesnoth 0ad kapman freedroidrpg``

**(Optional) Opensource games based on scummvm:**

* ``sudo apt install beneath-a-steel-sky drascula flight-of-the-amazon-queen lure-of-the-temptress``

**(Optional) Python and free IDE installation:**

* ``sudo apt install python3 python3-pip bpython thony``

# 9. Additional Pipewire dependencies, Easy Effects, disable hibernation and other tips.

* ``sudo apt install ffmpeg``

**Fixing audio issues:**

**Most gaming audio related issues in Proton/Pipewire happen because Secure Boot is enabled, installing Debian with Secure Boot disabled in BIOS/UEFI will help in these cases, Steam Deck has no Secure Boot.**

**Install additional alsa and pipewire dependencies and restart pipewire service**

* ``sudo apt install libasound2t64 libasound2-plugins alsa-utils alsa-firmware-loaders pipewire-audio pipewire pipewire-audio-client-libraries pipewire-pulse pipewire-alsa libcanberra-pulse pipewire wireplumber``
* ``systemctl --user restart wireplumber pipewire pipewire-pulse``

**Select Pro Audio,especially for USB headphones instead of Analog Stereo Duplex:**

* ``sudo nano /usr/share/pipewire/pipewire.conf``

**Find this line:**

* #default.clock.allowed-rates = [ 48000 ]

**Change to:**

* #default.clock.allowed-rates = [ 44100 48000 96000 ]

 
**(Optional)To fix audio crackling remove speech-dispatcher**

* ``sudo apt purge speech-dispatcher``
* ``sudo apt autoremove``

**(Optional) easyeffects package and more audio plugins:**

* ``sudo apt install easyeffects``
* ``sudo apt install lsp-plugins-lv2 calf-plugins x42-plugins zam-plugins``


**Launch EasyEffects and apply presets that you can download from the repo provided here LoudnessEqualizer.json:**

* https://github.com/Digitalone1/EasyEffects-Presets


**(Desktop Only) Disable hibernate, sleep and other default settings for gaming purposes works best on KDE Plasma/XFCE, do not use on laptops!**

* ``sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target``
* ``sudo reboot``

**Another "PROPER" way to disable suspend and hybernate**

* ``sudo nano /etc/systemd/sleep.conf``

**Uncomment and set to no**
* ``[Sleep]``
* ``#AllowSuspend=yes`` 
* ``#AllowHibernation=yes``
* ``#AllowSuspendThenHibernate=yes``
* ``#AllowHybridSleep=yes``
  
**To disable suspend it should look like this**

* ``[Sleep]``
* ``AllowSuspend=no``
* ``AllowHibernation=no``
* ``AllowSuspendThenHibernate=no``
* ``AllowHybridSleep=no`` 

**Check if worked**
* ``systemctl suspend``
**This is the error message you should get**
* ``Call to Suspend failed: Sleep verb 'suspend' is disabled by config``
**To re-enable suspend just revert the changes**

**(Additional steps) Disable suspend on GNOME**

**Check types if active will reply `suspend`**

* ``gsettings get org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type``

**Check states should reply `true`**

* ``gsettings writable org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type``

**Check range of available states**

* ``gsettings range org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type``
  
**Enter**

* ``gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type 'nothing'``

**Check again should reply `nothing`**

* ``gsettings get org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type``


**Disable or remove apparmor**

* ``sudo systemctl disable apparmor``

*``sudo apt remove --assume-yes --purge apparmor``


**(Optional) Different file system support:**

**BTRFS**

* ``sudo apt install btrfs-progs duperemove``

**XFS**

* ``sudo apt install xfsprogs xfsdump attr quota``

**(Optional) Install flatpak support**

**Flatpak with GNOME Software store(for point and click software center application installations)**

* ``sudo apt install flatpak``

* ``sudo apt install gnome-software-plugin-flatpak``

* ``flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo``

* ``sudo apt update && sudo apt upgrade``
  
**(Optional) GNOME extensions and tweaks**

* ``sudo apt install gnome-tweaks gnome-shell-extension-manager gnome-shell-extensions gnome-shell-extensions-extra``
  
**Flatpak with KDE Plasma Discover (for point and click software center application installations)**

* ``sudo apt install flatpak``

* ``flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo``

* ``sudo apt install plasma-discover-backend-flatpak``

* ``sudo apt update && sudo apt upgrade``
  
**(Optional) Installing flatpak apps from the command line**
* ``flatpak install protontricks vcmi fheroes2 openmw``

**Let protontricks app have permissions for other drives on Steam**

* ``flatpak override --user --filesystem=/mnt/MySSDName/SteamLibrary com.github.Matoking.protontricks``

**Install a flatpak app with --system wide or --user wide permissions**
* ``flatpak install openmw --system``
* ``flatpak isntall openmw --user``

**Remove flatpak apps**
* ``flatpak uninstall openmw``
* ``flatpak remove openmw``

**(Optional) virt manager and QEMU Installation for Virtualization**

* ``sudo apt install virt-manager qemu-system``

**Quick .deb way to install popular applications with debian ports like gzdoom,zoom,teamviewer with dpkg(if you need it):**

* https://zdoom.org/downloads
* https://zoom.us/download
* https://www.teamviewer.com/en/download/linux/
* https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/releases/
* ``sudo dpkg -i gzdoom_4.7.1_amd64.deb``
* ``sudo dpkg -i zoom_amd64.deb``
* ``sudo dpkg -i teamviewer_15.28.8_amd64.deb``
* ``sudo dpkg -i Heroic-2.20.0-linux-amd64.deb``

**(Optional) removing apps with dpkg along with their config files**

* ``sudo dpkg -r -P heroic``
* ``sudo dpkg --remove --force-depends heroic``
* ``sudo dpkg --purge --force-depends heroic``

# 10. (Optional) install Shotcut/KDENlive/Gimp/Krita for video/photo editing:

* ``sudo apt install shotcut kdenlive gimp krita``

# 11. Upgrade OS version and install all updates
 
 * ``sudo apt-get update``
 
 * ``sudo apt-get upgrade``
   
 * ``sudo apt update && sudo apt upgrade``
 
 * ``sudo apt-get dist-upgrade``

# 12. Optional install discord app,go to: 

* https://discordapp.com/  

**Select Download for Linux choose .deb:**

**Open Terminal in Downloads folder and use the following commands dpending on the .deb file version:**

* ``sudo apt install gdebi-core``
* ``sudo gdebi discord-0.0.10.deb``

# 13. Automount using gnomedisk utility:

* ``sudo apt install gnome-disk-utility``

**Edit mount options**

**Add this line:**

* nosuid,nodev,nofail,x-gvfs-show,auto

**Or just move the slider in the app for all of the unmounted disks, this method has less issues**
  

# 14. Benchmarking games and using FPS limiters with mangohud:

* ``sudo apt install mangohud mangohud:i386``

# 15. Creating a bootable Windows 10 USB using Disks utility (Possible on any linux distro even without GNOME)
* ``sudo apt install gnome-disk-utility``
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

**(Optional) Install Glourious Eggroll Proton GE the easy way:**

 ***Download the latest release here:** https://github.com/GloriousEggroll/proton-ge-custom/releases
 * Extract,enable hidden files and folders in your file manager Dolphin/Nemo
 * Create a folder in your /home/user/steam/root/compatibilitytools.d if it does not exist.
 * Copy/paste the extracted GE folder into /home/user/config/.steam/root/compatibilitytools.d
 * Restart Steam,enjoy the custom GE build

**(Optional) comand similar to mkinitcpio,useful sometimes:**

* ``sudo update-initramfs -u``

**(Optional) check for obsolete packages**

* ``sudo apt list '?obsolete'``

**(Optional) install better fonts and icon themes:**

 * ``sudo apt install fonts-hack-ttf``
 * ``sudo apt install papirus-icon-theme``

**Mass install fonts on GNOME**
* Mass copy the desired fonts to the ``/usr/local/share/fonts/ ``
* ``fc-cache /usr/local/share/fonts/``

**View BIOS/UEFI/SLOT/CPU/Memory Info**

* ``sudo dmidecode | less``
* ``sudo dmidecode -s bios-version``
* ``sudo dmidecode -s bios-release-date``
* ``sudo dmidecode -t bios``
* ``sudo dmidecode -t baseboard``
* ``sudo dmidecode -t 2``
* ``sudo dmidecode -t slot``
* ``sudo dmidecode -t processor``
* ``sudo dmidecode -s processor-version``
* ``sudo dmidecode -s processor-frequency``
* ``sudo dmidecode -t memory``
* ``cat /sys/devices/virtual/dmi/id/board_{vendor,name,version}``
* ``sudo lspci -v | less``

**View temps, if not installed then install the sensors package**
  
* ``sudo apt install lm-sensors``
* ``sensors``
  
**How to check mesa vulkan driver versions:**

* ``glxinfo | grep "Mesa" ``
* ``glxinfo | grep OpenGL``
* ``vulkaninfo``
  
**How to check pipewire version**

* ``pactl info|grep "Server Name"``

**(Optional) Adding a secondary SSD/HDD in fstab manually:**

**If it is an existing SSD/HDD that you already formatted with ext4 or btrfs and automounted in filemanager like Dolphin or Nemo,then you have to check in properties for example "/media/user/Backup" that is your mount point.**

* ``sudo lsblk -f``

* ``sudo nano /etc/fstab``

 **Contents of FSTAB:**

**< file system > < mount point >   < type >  < options >                        < dump >  < pass >**

* ``/ was on /dev/sda2 during installation``
* ``UUID=362fe9a2-29fc-43fe-824d-09d1d93b1549 /               ext4    errors=remount-ro 0       1``
* ``/boot/efi was on /dev/sda1 during installation``
* ``UUID=64EF-0C84  /boot/efi       vfat    umask=0077      0       1``

* ``swap was on /dev/sda3 during installation``
* ``UUID=b36261ad-191e-4cb5-ba0e-f2715e32f82c none            swap    sw              0       0``
* ``/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0``

**Add your SSD/HDD with its mount point here:**

* ``/dev/sdb1       /media/user/Backup                        ext4    defaults,noatime 0      2``

**Save the changes and exit,reboot,you are good**

# 16. Cyber security

**Firewall install and enable via GUI:**

* ``sudo apt install ufw``

**ClamAV**

* ``sudo apt install clamav``
* ``sudo freshclam``
* ``clamscan -r --bell -i /home /tmp /var/tmp``
* ``sudo systemctl start clamav-daemon``

**Full scan if you have time:**

* ``clamdscan --multiscan --fdpass / ``

**Rootkit hunter:**

* ``sudo apt install rkhunter``
* ``sudo rkhunter --update``
* ``sudo rkhunter --check``

**Check manually for malware activity with ls or in your file browser,XDG autostart jobs, bash or zsh (weird entries and services):**

* ``ls ~/.config/autostart/ ``

* ``ls ~/.bashrc /``

* ``ls ~/.zshrc ``

**Systemd user services:**
  
* ``ls ~/.config/systemd/user/``

* ``ls /etc/systemd/system/``

* ``ls  /usr/local/bin/ ``

**Checking strage cron jobs**

* ``crontab -e``

* ``sudo crontab -e``

**Check suspicious shadow bin entries:**

* ``ls /usr/local/bin/``

**Check process tree for strange activity:**

* ``pstree -a -p``

**Look for anything strange such as:**

* makepkg → gcc → wget → /tmp/a.out → runs as root

* xdg-open readme.eml → bash → curl <IP> → ./payload

**History of execution for today**

* ``journalctl _COMM=exe -S today``

* ``ausearch -m execve --success yes``

**Check and clean apt cache**
* ``ls /var/cache/apt/archives``
* ``sudo du -sh /var/cache/apt/archives``
* ``sudo apt-get clean --dry-run``
* ``sudo apt-get clean``


**Check and delete history:**
* ``history``
* ``history -c; rm ~/.bash_history``

**A way to remove packages that are not downloaded from repositories, standar oudated .deb files**

* ``sudo apt autoclean --dry-run``
* ``sudo apt autoclean``

**Fix Wayland iBUS message on KDE Plasma**

* ``sudo nano /usr/share/im-config/data/21_ibus.rc``
* Comment these lines out with # so they look like this:
* ``# GTK_IM_MODULE=ibus``
* ``# QT_IM_MODULE=ibus``
* ``# CLUTTER_IM_MODULE=ibus``
* Go into System Settings>Virual Keyboard and apply iBUS
* ``sudo reboot``

**(Bonus) Nice network tools to have:**

* ``sudo apt install spedtest-cli bind9 bind9-doc  bind9-dnsutils  resolvconf  mmdb-bin``
* ``sudo apt install wireshark john torbrowser-launcher``

**(Bonus) Reset Windows Password from a Debian Live USB**
* ``sudo apt install chntpw``
* ``sudo sfdisk -l``

**For regular SSD's/HDD's:**

* ``sudo mount /dev/sda2 /mnt/Microsoft/``

**For NVME SSD's:**

* ``sudo mount /dev/nvme0n1p2 /mnt/Microsoft``
* ``cd /mnt/Microsoft/Windows/System32/config/``
* ``sudo chntpw -i SAM``

**Then type 1 (for Edit user data and passwords):**
![passwordreset_username-1](https://github.com/user-attachments/assets/c41cd77c-6420-4620-a4fd-869bb4f87f6a)

**Type your user account name (i.e., Archit-PC in this example) for the username:**
![passwordreset_username-2](https://github.com/user-attachments/assets/44eabc2a-6a23-4cbf-b26a-4b8a4c58c99e)

**Type 1 to clear the user password or 2 to set a new password for the Archit-PC user, then quit and save the changes:**
![passwordreset_username-1](https://github.com/user-attachments/assets/e7bfc201-c189-4198-869d-64eba3a29a9b)

![passwordreset_username-2](https://github.com/user-attachments/assets/142fec77-b047-43a7-b5ce-62b8a3f820a3)

**Reboot into Windows and login**

**NB! In case of "A start job is running for update the operating system while offline" on Debian-based systems during updates while dual-booting press E then F10 and wait for the update process to finish.**
Ok, thank you, happy gaming and streaming on pure Debian.
Hopefully same settings will work on the future Debian distros!
Enjoy!
# YouTube:
**silentgameplays**
https://www.youtube.com/@silentgameplays


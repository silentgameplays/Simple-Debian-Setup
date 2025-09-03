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

**Install the NVIDIA drivers with stuff like vulkan,etc:**

* ``sudo apt install nvidia-driver nvidia-settings libvulkan-dev nvidia-vulkan-icd vulkan-tools  vulkan-validationlayers``
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

**Increase vm.max_map_count to Steam Deck values to prevent games crashing:**

* ``sudo nano /etc/sysctl.d/99-sysctl.conf``

**Add** ``vm.max_map_count = 2147483642``

* ``sudo sysctl --system``

* ``sudo reboot``

* ``cat /proc/sys/vm/max_map_count``

# 8. Gaming section install Steam,Lutris,Wine with the following commands, if you did all the steps before correctly then Steam should install without issues:

* ``sudo apt install steam lutris wine wine32 wine64 libwine libwine:i386 fonts-wine scummvm dosbox ``

**(Optional) Additional dependencies for Wine/Gaming:**

* ``sudo apt install gvfs:i386 wine32-preloader:i386 wine64-preloader wine-binfmt gstreamer1.0-libav:i386 gstreamer1.0-plugins-bad:i386 gstreamer1.0-plugins-ugly winetricks gstreamer1.0-tools:i386 opus-tools:i386 gstreamer1.0-alsa gamemode timidity``

* `` sudo apt install mono-complete``

* ``sudo apt install fizmo-sdl2 libsdl2-2.0-0 libsdl2-dev libsdl2-gfx-1.0-0 libsdl2-gfx-dev libsdl2-image-2.0-0 libsdl2-mixer-2.0-0 libsdl2-net-2.0-0``

* ``sudo apt install mingw-w64 flvmeta smpeg-plaympeg lame mjpegtools x265 x264 mpv mpg123 libxvidcore4 fluidsynth``

**(Optional) Opensource games:**

* ``sudo apt install supertux supertuxkart wesnoth 0ad kapman freedroidrpg``

**(Optional) Opensource games based on scummvm:**

* ``sudo apt install beneath-a-steel-sky drascula flight-of-the-amazon-queen lure-of-the-temptress``

**(Optional) Python and free IDE installation:**

* ``sudo apt install python3 python3-pip bpython thony``

# 9. Optional for streaming/recording install OBS Studio(for NVENC support some additional stuff is required)

* ``sudo apt install ffmpeg``

**Fixing audio issues:**

**To fix audio crackling remove speech-dispatcher**

* ``sudo apt purge speech-dispatcher``
* ``sudo apt aurotemove``
  
**Install additional alsa and pipewire dependencies and restart pipewire service**

* ``sudo apt install libasound2 libasound2-plugins alsa-utils alsa-oss alsa-firmware-loaders``
* ``sudo apt install pipewire pipewire-audio-client-libraries pipewire-pulse pipewire-alsa``
* ``systemctl --user restart wireplumber pipewire pipewire-pulse``

**Select Pro Audio,especially for USB headphones instead of Analog Stereo Duplex:**

* ``sudo nano /usr/share/pipewire/pipewire.conf``

**Find this line:**

* #default.clock.allowed-rates = [ 48000 ]

**Change to:**

* #default.clock.allowed-rates = [ 44100 48000 96000 ]

**(Optional) easyeffects package:**

* ``sudo apt install easyeffects``

**Launch EasyEffects and apply presets that you can download from the repo provided here LoudnessEqualizer.json:**

* https://github.com/Digitalone1/EasyEffects-Presets

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

**Flatpak with KDE Plasma Discover (for point and click software center application installations)**

* ``sudo apt install flatpak``

* ``flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo``

* ``sudo apt install plasma-discover-backend-flatpak``

* ``sudo apt update && sudo apt upgrade``
  
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
* ``sudo dpkg -i Heroic-2.18.1-linux-amd64.deb``

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

**(Optional) install better fonts and icon themes:**

 * ``sudo apt install fonts-hack-ttf``
 * ``sudo apt install papirus-icon-theme``

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
  
**View temps, if not installed then install the sensors package**
  
* ``sudo apt install lm-sensors``
* ``sensors``
  
**How to check mesa vulkan driver versions:**

* ``glxinfo | grep "Mesa" ``

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

**(Bonus) Nice network tools to have:**

* ``sudo apt install spedtest-cli bind9 bind9-doc  bind9-dnsutils  resolvconf  mmdb-bin``
* ``sudo apt install wireshark john torbrowser-launcher``


**NB! In case of "A start job is running for update the operating system while offline" on Debian-based systems during updates while dual-booting press E then F10 and wait for the update process to finish.**
Ok, thank you, happy gaming and streaming on pure Debian.
Hopefully same settings will work on the future Debian distros!
Enjoy!
# YouTube:
**silentgameplays**
https://www.youtube.com/@silentgameplays


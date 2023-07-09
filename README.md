# Thinkpad X220 / T420s Guide
Work in Progress - This is to document the steps I did to rebuild my old Thinkpad X220 from 2011 and make it usable in 2023!

Initially this is for the Thinkpad X220, but after using it for several days the biggest drawback for me is the 1366x768 TN panel. I decided to remove the components and transplant it to my T420s instead with a 1080p IPS panel.

# Why?!?
I don't have a good reason except that I like the 7row keyboard, Thinklight, it is compact and it still works good in 2023!!!
![image](https://github.com/ryanrudolfoba/Thinkpad-X220-Guide/assets/98122529/1bb43929-2825-4c53-b60f-3cb5688ff0af)


## Hardware Configuration / Hardware Mods
CPU - Intel 2.5GHz Core i5 2520M \
Display - 1080p IPS panel using LVDS to eDP converter \
RAM - 16GB SODIMM DDR3 RAM \
Main Storage - 2TB SATA SSD \
Secondary Storage - 256GB mSATA SSD via cdrom caddy \
WIFI1 - Alfa AWPCIE 1900 RTL8814au via wwan slot \
WIFI2 - Intel Dual Band 7260ac via wifi slot \
Bluetooth - Bluetooth 4.0 via Intel Dual Band 7260ac

![image](https://github.com/ryanrudolfoba/Thinkpad-X220-Guide/assets/98122529/1c1b878c-5d0b-4d88-a83b-71b9db25f4c5)


## OS Installation
1. Download Fedora 38 Everything ISO. It is the minimal net installer for Fedora.

2. Burn the ISO using Ventoy.

3. Boot the ISO and on the software selection select KDE desktop, Firefox web browser, KDE Multimedia support, LibreOffice, C Development Tools and Libraries.

4. Perform a manual disk partitioning with this layout - \
   400MB ESP mounted as /boot/efi \
   128GB xfs mounted as / \
   16GB swap \
   the remaining as xfs mounted as /home

5. Create the user account and assign the password.

6. Start the install process. This will take around 10 minutes as the packages are downloaded and installed.


## Software Installation
1. Remove unneeded packages - \
   sudo dnf remove iwl* hyperv* open-vm* qemu-guest* b43* xorg-x11-drv-amdgpu xorg-x11-drv-vmware xorg-x11-drv-nouveau xorg-x11-drv-ati xorg-x11-drv-wacom amd* nvidia* qt5-qdbusviewer akregator k3b elisa* dragon*

2. Install rpmfusion repositories - \
   sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

3. Install tlp repository - \
   sudo dnf install https://repo.linrunner.de/fedora/tlp/repos/releases/tlp-release.fc$(rpm -E %fedora).noarch.rpm
   
4. Install tlp - \
   sudo dnf install tlp tlp-rdw \
   sudo dnf remove power-profiles-daemon \
   sudo systemctl enable tlp.service \
   sudo systemctl mask systemd-rfkill.service systemd-rfkill.socket \
   sudo dnf install kernel-devel akmod-tp_smapi
   
5. Install packages for rpmfusion multimedia - \
   sudo dnf swap ffmpeg-free ffmpeg --allowerasing \
   sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin \
   sudo dnf groupupdate sound-and-video \
   sudo dnf install libva-intel-driver \
   sudo dnf install rpmfusion-free-release-tainted \
   sudo dnf install libdvdcss \
   sudo dnf install rpmfusion-nonfree-release-tainted

6. Install packages for hardware acceleration - \
   sudo dnf install libva-utils \
   sudo dnf install libva-intel-driver \
   sudo dnf install libva-vdpau-driver \
   sudo dnf install libvdpau-va-gl \
   sudo dnf install igt-gpu-tools
   
8. Install packages -\
   sudo dnf install git zcfan rtorrent mpv android-tools neofetch mpd ncmpc unrar discord lm_sensors java-17-openjdk
   
9. Install jdownlader2 \

10. To be continued . . .


## Software Configuration
1. Enable hardware decoding in mpv - \
   echo hwdec=auto >> ~/.config/mpv/mpv.conf

2. Configure fan control via zcfan - \
   sudo tee /etc/zcfan.conf << EOF \
   max_temp 70 \
   med_temp 65 \
   low_temp 60 \
   EOF

   rmmod thinkpad_acpi && modprobe thinkpad_acpi fan_control=1 \
   sudo systemctl enable zcfan \
   sudo systemctl start zcfan

3. To be continued. . .

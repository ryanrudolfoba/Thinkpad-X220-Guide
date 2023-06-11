# Thinkpad X220 Guide
Steps I did to rebuild my old Thinkpad X220 and make it usable in 2023!

# Why?!?
I don't have a good reason except that I like the 7row keyboard, Thinklight, it is compact and it still works good in 2023 - 12 years after its initial release!

## Hardware Configuration
CPU - Intel 2.6GHz Core i5 2540M 
RAM - 2x8GB SODIMM DDR3
Main Storage - 2TB SATA SSD
Secondary Storage - 256GB mSATA SSD (awaiting parts)
WIFI - Alfa AWPCIE 1900 RTL8814au
Bluetooth - TPLINK Bluetooth 5.0 USB dongle via


## OS Installation
1. Download Fedora 38 Everything ISO. It is the minimal net installer for Fedora.
2. Burn the ISO using Ventoy.
3. Boot the ISO and on the software selection select KDE desktop.
4. Perform a manual disk partitioning with this layout - 
   400MB ESP mounted as /boot/efi
   128GB xfs mounted as /
   16GB swap
   the remaining as xfs mounted as /home
5. Create the user account and assign the password.
6. Start the install process. This will take around 10 minutes as the packages are downloaded and installed.


## Software Configuration
1. Remove unneeded packages -
    sudo dnf remove iwl* hyperv* open-vm* qemu-guest* b43*

2. sadsaa
3.

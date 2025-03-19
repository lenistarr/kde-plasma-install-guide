# kde-plasma-install-guide

sudo pacman -Syu 
sudo pacman -S linux-headers dolphin ffmpegthumbs firefox gwenview kate keepassxc konsole mpv okular plasma sddm transmission-qt yt-dlp thunderbird nvidia-open-dkms nvidia-utils
sudo systemctl enable sddm


Remove kms from the HOOKS array in /etc/mkinitcpio.conf and regenerate the initramfs. This will prevent the initramfs from containing the nouveau module making sure the kernel cannot load it during early boot. The nvidia-utils package contains a file which blacklists the nouveau module once you reboot. 

Nvidia does not load kernel mode setting by default, enabling it is required to make Wayland compositors function properly:

    sudo vim /etc/mkinitcpio.conf # In the MODULES array, add the following module names:
            MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
    sudo vim /etc/modprobe.d/nvidia.conf # Write the following:
            options nvidia_drm modeset=1 fbdev=1
    sudo mkinitcpio -P
    reboot


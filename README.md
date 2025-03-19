# KDE Plasma Install Guide
## Base Install 
```
sudo pacman -Syu 
sudo pacman -S dolphin ffmpegthumbs firefox gwenview kate keepassxc konsole mpv okular plasma sddm thunderbird transmission-qt yt-dlp 
sudo systemctl enable sddm
```
## For Nvidia GPUs
The following script will install nvidia-open-dkms, if you have an older GPU, change the nvidia package accordingly in the script.
```
sudo pacman -Syu 
sudo pacman -S linux-headers nvidia-open-dkms nvidia-utils
```
Nvidia does not load kernel mode setting by default, enabling it is required to make Wayland compositors function properly:
##
<dl><dd>
<pre>
sudo vim /etc/mkinitcpio.conf <i># In the MODULES array, remove "kms" from the "HOOKS" array, then add the following module names:
        MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)</i> 
Remove kms from the HOOKS array in /etc/mkinitcpio.conf and regenerate the initramfs. This will prevent the initramfs from containing the nouveau module making sure the kernel cannot load it during early boot. The nvidia-utils package contains a file which blacklists the nouveau module once you reboot. 
    
sudo vim /etc/modprobe.d/nvidia.conf # <i>Write the following:
        options nvidia_drm modeset=1 fbdev=1</i>
sudo mkinitcpio -P
reboot
</pre>
</dd></dl>



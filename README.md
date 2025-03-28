# KDE Plasma Install Guide
## Base Install 
```
sudo pacman -Syu 
sudo pacman -S dolphin ffmpegthumbs firefox gwenview kate keepassxc konsole mpv okular plasma sddm thunderbird transmission-qt yt-dlp 
sudo systemctl enable sddm
```
## For Nvidia GPUs
The following commands will install nvidia-open-dkms, if you have an older GPU, change the nvidia package according to your supported GPU family in the script.
```
sudo pacman -Syu 
sudo pacman -S linux-headers nvidia-open-dkms nvidia-utils
```
Nvidia drivers do not load kernel mode setting by default, enabling it is required to make Wayland compositors function properly:
##
<dl><dd>
<pre>
sudo vim /etc/mkinitcpio.conf <i># First remove "kms" from the HOOKS array, then, in the MODULES array, add the following module names:
        MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)</i> 
sudo vim /etc/modprobe.d/nvidia.conf # <i>Write the following:
        options nvidia_drm modeset=1 fbdev=1</i>
sudo mkinitcpio -P
reboot
</pre>
</dd></dl>

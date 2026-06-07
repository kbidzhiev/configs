# Linux and vim configs

## Linux mint XFCE configs
```bash
#!/usr/bin/env bash

# Dell Latitude 7480 + Linux Mint XFCE optimization

# Install useful packages:
# inxi        - detailed hardware and system information
# tlp         - laptop power management and battery optimization
# tlp-rdw     - additional TLP radio device management (Wi-Fi/Bluetooth)
# earlyoom    - prevents freezes when RAM is exhausted
# zram-tools  - compressed RAM swap for better multitasking
# htop        - interactive process and resource monitor
# btop        - modern system monitor with CPU/RAM/disk/network views
# ncdu        - fast disk usage analyzer
# fwupd       - Linux firmware update manager
# neofetch    - quick system information display

sudo apt update

sudo apt install -y \
    inxi \
    tlp \
    tlp-rdw \
    earlyoom \
    zram-tools \
    htop \
    btop \
    ncdu \
    fwupd \
    neofetch

# Enable weekly SSD TRIM
sudo systemctl enable --now fstrim.timer

# Enable EarlyOOM protection
sudo systemctl enable --now earlyoom

# Enable TLP power management
sudo systemctl enable tlp
sudo systemctl start tlp

# Verify hardware information
inxi -Fxxx

# Verify SSD TRIM status
systemctl status fstrim.timer

# Verify TLP status
sudo tlp-stat -s

# Verify ZRAM after reboot
swapon --show

# Interactive process viewer
htop

# Advanced system monitor
btop

# Disk usage analyzer
ncdu /

# Quick system overview
neofetch

# Firmware update workflow
fwupdmgr refresh
fwupdmgr get-updates
sudo fwupdmgr update

# Manual XFCE Tweaks:
# - Disable compositor if desktop feels sluggish
# - Reduce transparency and animations
# - Disable unused startup applications
# - Use Firefox + uBlock Origin
# - Prefer web versions of Slack, Teams, and Discord
# - Consider Geany or VSCodium instead of VS Code

# Expected benefits:
# - Better battery life
# - Lower temperatures
# - Better RAM utilization
# - Reduced freezes under memory pressure
# - Improved SSD longevity
# - Faster overall responsiveness
```

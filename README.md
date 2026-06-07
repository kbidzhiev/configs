# Linux and vim configs

## Linux mint XFCE configs
```bash
```bash
#!/usr/bin/env bash

set -e

echo "=== Dell Latitude 7480 + Linux Mint XFCE Optimization ==="

sudo apt update

# inxi        - detailed hardware and system information
# tlp         - laptop power management and battery optimization
# tlp-rdw     - additional Wi-Fi/Bluetooth power management
# earlyoom    - prevents system freezes when RAM is exhausted
# zram-tools  - compressed RAM swap for better multitasking
# thermald    - Intel CPU thermal management
# lm-sensors  - temperature, voltage, and fan monitoring
# powertop    - power consumption diagnostics
# preload     - learns usage patterns and speeds up app startup
# htop        - interactive process viewer
# btop        - modern system monitor
# ncdu        - disk usage analyzer
# fwupd       - firmware update manager
# neofetch    - quick system information display
# timeshift   - system snapshot and rollback tool

sudo apt install -y \
    inxi \
    tlp \
    tlp-rdw \
    earlyoom \
    zram-tools \
    thermald \
    lm-sensors \
    powertop \
    preload \
    htop \
    btop \
    ncdu \
    fwupd \
    neofetch \
    timeshift

# Enable SSD TRIM
sudo systemctl enable --now fstrim.timer

# Enable memory pressure protection
sudo systemctl enable --now earlyoom

# Enable laptop power optimization
sudo systemctl enable tlp
sudo systemctl start tlp

# Enable Intel thermal management
sudo systemctl enable --now thermald

# Enable preload
sudo systemctl enable --now preload

# Tune swappiness for ZRAM-based systems
echo "vm.swappiness=100" | sudo tee /etc/sysctl.d/99-zram-swappiness.conf >/dev/null
sudo sysctl --system

echo
echo "=== Optional Post-Install Steps ==="
echo
echo "# Detect available hardware sensors"
echo "sudo sensors-detect"
echo
echo "# View temperatures and fan speeds"
echo "sensors"
echo
echo "# Check hardware information"
echo "inxi -Fxxx"
echo
echo "# Monitor running processes"
echo "htop"
echo
echo "# Modern system monitor"
echo "btop"
echo
echo "# Analyze disk usage"
echo "ncdu /"
echo
echo "# Display system summary"
echo "neofetch"
echo
echo "# Check TLP status"
echo "sudo tlp-stat -s"
echo
echo "# Verify ZRAM"
echo "swapon --show"
echo
echo "# Firmware updates"
echo "fwupdmgr refresh"
echo "fwupdmgr get-updates"
echo "sudo fwupdmgr update"
echo
echo "# Power diagnostics"
echo "sudo powertop"
echo
echo "=== Recommended Manual XFCE Tweaks ==="
echo "- Disable compositor if desktop feels sluggish"
echo "- Reduce transparency and animations"
echo "- Disable unused startup applications"
echo "- Use Firefox + uBlock Origin"
echo "- Prefer web versions of Slack, Teams, and Discord"
echo
echo "Optimization complete."
```
One note: in 2026, preload is not maintained on all distributions and may not provide noticeable gains on SSD-based systems. If apt can't find it, simply remove preload from the package list and the related service commands. Everything else is worth keeping.

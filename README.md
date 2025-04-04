# Raspberry Pi Zero W – USB OTG Networking & WiFi Switching Guide

This guide explains how to configure USB networking (`usb0`) on a Raspberry Pi Zero W using NetworkManager, so you can stay connected via SSH or a web UI even when switching WiFi networks. Useful for CyberViking or other headless setups.

---

## 🧰 What this setup does

✅ Enables `usb0` OTG networking with static IP  
✅ Allows the Pi to be managed via USB cable  
✅ Keeps USB connection alive during WiFi switches  
✅ Automates setup at boot with a systemd service  

---

## 📦 Step 1: Create the startup script

```
sudo nano /usr/local/bin/usb0-setup.sh
```
Paste the following:

```
#!/bin/bash

# Add usb0 connection if it doesn't already exist
nmcli connection show usb0 >/dev/null 2>&1
if [ $? -ne 0 ]; then
    nmcli connection add type ethernet ifname usb0 con-name usb0 ipv4.addresses 172.20.2.1/24 ipv4.method manual
fi

# Ensure NetworkManager handles usb0
sudo sed -i 's/managed=false/managed=true/' /etc/NetworkManager/NetworkManager.conf

# Restart NetworkManager
sudo systemctl restart NetworkManager

# Bring up the usb0 connection
sudo nmcli connection up usb0
```

Make it executable:

```
sudo chmod +x /usr/local/bin/usb0-setup.sh
```

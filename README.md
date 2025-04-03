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

# 🚀 Universal macOS Installer via Terminal

This project provides a **safe and universal method** to install macOS on any APFS volume using the Terminal — compatible with all Apple official installers like Sequoia, Tahoe, Ventura, and more.

## ▶️ Video Tutorial

Watch the full tutorial video here:  
[![Watch on YouTube](https://img.youtube.com/vi/9xOn7dbi47I/0.jpg)](https://youtu.be/9xOn7dbi47I)

Or open directly: [https://youtu.be/9xOn7dbi47I](https://youtu.be/9xOn7dbi47I)

## ✅ Features

- Works with **any Install macOS .app**
- Avoids formatting or erasing your current system
- Supports volume renaming
- Uses `startosinstall` safely without `--eraseinstall`
- Protects against installing on the current running system
- Includes a 60-second reboot delay for safety

## 📜 How to Use

Use this universal Terminal command to safely install macOS:

```

echo "📦 Drag the macOS installer app here and press Enter:"; read installer_app; if [ ! -f "$installer_app/Contents/Resources/startosinstall" ]; then echo "❌ ERROR: Invalid macOS installer. Make sure it's a valid '.app' with startosinstall inside."; exit 1; fi; echo "🔹 Drag the target volume here and press Enter:"; read target_volume; echo "📝 Enter the new name you want to give the volume (or press Enter to keep the current name):"; read custom_name; current_root=$(df / | tail -1 | awk '{print $1}'); dragged_device=$(df "$target_volume" 2>/dev/null | tail -1 | awk '{print $1}'); if [ "$dragged_device" = "$current_root" ]; then echo "❌ ERROR: You are trying to erase the volume where the current system is running. Operation cancelled."; exit 1; fi; original_mount_point="$target_volume"; if [ -n "$custom_name" ]; then diskutil rename "$target_volume" "$custom_name"; target_volume="$(dirname "$original_mount_point")/$custom_name"; fi; echo "✅ Final target volume confirmed: $target_volume"; sudo "$installer_app/Contents/Resources/startosinstall" --volume "$target_volume" --agreetolicense --nointeraction --passprompt --rebootdelay 60

```

> 📌 Copy and paste this into Terminal. It works on Intel Macs and Hackintosh (with SIP disabled). Tested on Sequoia 15.5, Tahoe Beta 4, and Ventura.

## 📁 Full Tutorial

https://www.insanelymac.com/forum/topic/361410-safe-macos-installation-via-terminal-–-universal-script-sequoia-tahoe-ventura/ 

## 🛡 System Integrity Protection (SIP)

**Disable SIP if you're using Hackintosh or a modified system**, otherwise the installer may ignore your selected volume and install over the current one.

To disable SIP:
1. Boot into **Recovery Mode**
2. Open Terminal and run:
    ```
    csrutil disable
	csrutil authenticated-root disable
	reboot
    ```
3. Restart

## 💡 Want to Contribute?

Feel free to fork, improve or translate this project. Pull requests are welcome!

---

© 2025 – This script is free to use and share. Use responsibly.

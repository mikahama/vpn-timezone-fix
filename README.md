# 🌍 VPN Timezone Fix for Linux (GNOME)

If you enable **Automatic Timezone** on Linux (GNOME), your computer detects your location using your internet address (IP). However, if you connect to a **VPN**, your internet address changes to the VPN server's location, causing your system clock to change to the wrong timezone.

This tool solves that problem. It lets you keep **Automatic Timezone** turned on (perfect for traveling) while ensuring your clock **never changes** when you connect to a VPN.

---

## 🤔 How It Works (Simplified)
Once installed, this tool runs quietly in the background and checks your connection every 15 seconds:
* **When you connect to a VPN:** It temporarily turns off GNOME's "Automatic Timezone" setting. Your clock stays locked to your current timezone.
* **When you disconnect from the VPN:** It turns "Automatic Timezone" back on. If you are traveling, your clock will automatically adjust to the local timezone.

---

## 🚀 How to Install

### Option 1: Easy Installation for Ubuntu, Debian, Pop!_OS, and Linux Mint
You can easily build and install this tool as a Debian package. Open your terminal in this directory and run:

1. **Build the package:**
   ```bash
   dpkg-deb --build . vpn-timezone-fix.deb
   ```

2. **Install the package:**
   ```bash
   sudo apt install ./vpn-timezone-fix.deb
   ```

That's it! The installer will automatically set everything up and start the tool in the background.

---

### Option 2: Manual Installation (For other Linux distributions)
If you are not using a Debian/Ubuntu-based system, you can install the files manually:

1. **Copy the guard script** to your system executables:
   ```bash
   sudo cp usr/local/bin/auto-timezone-vpn-guard /usr/local/bin/
   sudo chmod +x /usr/local/bin/auto-timezone-vpn-guard
   ```

2. **Copy the system background services**:
   ```bash
   sudo cp etc/systemd/system/auto-timezone-vpn-guard.* /etc/systemd/system/
   ```

3. **Enable and start the background timer**:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable --now auto-timezone-vpn-guard.timer
   ```

---

## 🔍 How to Check if It is Working

To verify that the tool is active and checking your VPN status:

* **Check the timer status:**
  ```bash
  systemctl status auto-timezone-vpn-guard.timer
  ```
  *(You should see `active (waiting)` or `running`.)*

* **View the system logs:**
  ```bash
  journalctl -t auto-timezone-vpn-guard
  ```
  *(This will show you when the tool detects a VPN connection and toggles the settings.)*

---

## ❌ How to Uninstall

If you ever want to remove the tool:

### If you installed via Option 1 (Debian package):
```bash
sudo apt remove vpn-timezone-fix
```

### If you installed via Option 2 (Manual):
```bash
sudo systemctl disable --now auto-timezone-vpn-guard.timer
sudo rm /usr/local/bin/auto-timezone-vpn-guard
sudo rm /etc/systemd/system/auto-timezone-vpn-guard.service
sudo rm /etc/systemd/system/auto-timezone-vpn-guard.timer
sudo systemctl daemon-reload
```

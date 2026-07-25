# 🌍 VPN Timezone Fix for Linux (GNOME)

If you enable **Automatic Timezone** on Linux (GNOME), your computer detects your location using your internet address (IP). However, if you connect to a **VPN**, your internet address changes to the VPN server's location, causing your system clock to change to the wrong timezone. :-/

This tool solves that problem. It lets you keep **Automatic Timezone** turned on (perfect for traveling) while ensuring your clock **never changes** when you connect to a VPN.

---

## 🤔 How It Works (Simplified)
Once installed, this tool runs quietly in the background and checks your connection every 15 seconds:
* **When you connect to a VPN:** It temporarily turns off GNOME's "Automatic Timezone" setting. Your clock stays locked to your current timezone.
* **When you disconnect from the VPN:** It turns "Automatic Timezone" back on. If you are traveling, your clock will automatically adjust to the local timezone.

---

## 🚀 How to Install

### 1. Add my repo

[Add my repository using these instructions](https://mikakalevi.com/repo/)

### 2. Install vpn-timezone-fix

    sudo apt install vpn-timezone-fix


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



# 🔄 Automate Monthly System Updates on Ubuntu 24.04

A clean, reliable way to keep your **Ubuntu‑based VPN server** fully updated.  
This script performs a full system upgrade, removes old packages, logs the results, and can optionally reboot the server afterward.

---

## 📝 Step 1: Create the Update Script

Create the script file:

```bash
sudo nano /usr/local/bin/auto-update.sh
```

Paste the following:

```bash
#!/bin/bash
# Update package lists and upgrade everything
apt-get update && apt-get dist-upgrade -y

# Clean up old files
apt-get autoremove -y
apt-get autoclean

# Log completion time
echo "Full system update completed on $(date)" >> /var/log/sys_update.log
```

Make it executable:

```bash
sudo chmod +x /usr/local/bin/auto-update.sh
```

---

## ⏱️ Step 2: Schedule Monthly Updates with Cron

Open the root crontab:

```bash
sudo crontab -e
```

Add this line:

```bash
0 3 1 * * /usr/local/bin/auto-update.sh
```

This runs the update script **at 3:00 AM on the 1st of every month**.

---

## 🔁 Step 3: (Optional) Enable Auto‑Reboot

If you want the server to reboot after updates:

```bash
sudo nano /usr/local/bin/auto-update.sh
```

Add this line at the bottom:

```bash
/sbin/reboot
```

---

## ✅ Step 4: Verify Everything

Check scheduled cron jobs:

```bash
sudo crontab -l
```

Check your update log:

```bash
cat /var/log/sys_update.log
```

---

Your Ubuntu 24.04 VPN server will now stay updated, clean, and low‑maintenance with minimal effort.
```

---

If you want, I can also format this as a **GitHub README module**, add **badges**, or create a **one‑page quick‑start** for your whole VPN server project.

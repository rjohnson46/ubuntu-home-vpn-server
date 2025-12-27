# 🖥️ Ubuntu Laptop Home Server + Personal VPN (Tailscale Exit Node)

This guide walks you through converting an Ubuntu laptop into a reliable **home server** and a **personal VPN** using Tailscale.  
You’ll configure the laptop to stay awake with the lid closed, then set it up as a secure VPN exit node accessible from anywhere.

* * *

## 🔧 Phase 1: Prepare the Hardware

### Keep the Laptop Awake With the Lid Closed

Ubuntu suspends when the lid is closed — not ideal for a server.  
Disable this behavior:

1.  Open your terminal.
2.  Edit the logind configuration file:

```bash
sudo nano /etc/systemd/logind.conf
```

3.  Find this line:

```
#HandleLidSwitch=suspend
```

4.  Remove the `#` and change it to:

```
HandleLidSwitch=ignore
```

5.  Save and exit (`Ctrl+O`, Enter, `Ctrl+X`).
6.  Apply the changes:

```bash
sudo systemctl restart systemd-logind
```

Your laptop will now stay awake with the lid closed.

* * *

# 🌐 Turn the Laptop Into a Personal VPN Server

Using **Tailscale**, you can turn your laptop into a secure VPN server that routes your internet traffic through your home network.  
This uses a feature called an **Exit Node**.

* * *

## 🚀 Step 1: Install Tailscale on Ubuntu

1.  Install Tailscale:

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

2.  Start and authenticate:

```bash
sudo tailscale up
```

Follow the URL provided to log in with Google, Microsoft, or GitHub.

* * *

## 🔁 Step 2: Enable Exit Node Mode

### 1\. Enable IP Forwarding

```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

### 2\. Advertise as an Exit Node

```bash
sudo tailscale up --advertise-exit-node
```

* * *

## 🛡️ Step 3: Approve the Exit Node in the Admin Console

1.  Open the Tailscale Admin Console:  
    https://login.tailscale.com/admin/machines
2.  Find your Ubuntu laptop.
3.  Click the **three dots (…)** → **Edit route settings**.
4.  Enable **Use as exit node**.
5.  Save.

Your laptop is now a fully functional VPN server.

* * *

## 📱 Step 4: Connect From iOS or Android

### iPhone / iPad (iOS)

1.  Install **Tailscale** from the App Store.
2.  Log in with the same account.
3.  Tap **Exit Node**.
4.  Select your Ubuntu laptop.
5.  Toggle the VPN switch to **Active**.

### Android

1.  Install **Tailscale** from the Play Store.
2.  Log in and accept the VPN permission.
3.  Tap **Exit Node**.
4.  Select your laptop.
5.  Toggle the connection on.

Your mobile device now routes all traffic through your home server.

* * *

## 🔒 Why This Beats a Commercial VPN

- **Privacy:** You own the server — no third‑party logging.
- **Local Access:** Reach home files, printers, or cameras from anywhere.
- **Zero‑Config:** Tailscale handles NAT, dynamic IPs, and firewall rules automatically.

* * *

## ✔️ Summary

You now have:

- A laptop that stays awake with the lid closed
- A secure, self‑hosted VPN server
- Global access to your home network
- A privacy‑focused alternative to commercial VPNs

* * *

&nbsp;

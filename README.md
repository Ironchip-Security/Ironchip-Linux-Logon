<p align="center">
  <img alt="Ironchip icon" src="/assets/icon.png" width="100"/>
</p>

<h1 align="center">Ironchip Linux</h1>

<p align="center">
  <a href="https://github.com/Ironchip-Security/Ironchip-Linux-Logon/releases/latest">
    <img alt="Latest release" src="https://img.shields.io/github/v/release/Ironchip-Security/Ironchip-Linux-Logon?color=green"/>
  </a>

  <a href="https://github.com/Ironchip-Security/Ironchip-Linux-Logon/releases/latest">
    <img alt="Release date" src="https://img.shields.io/github/release-date/Ironchip-Security/Ironchip-Linux-Logon?color=orange"/>
  </a>
</p>

## IDENTITY PROTECTION

Elevate your cybersecurity strategy with Ironchip Identity Platform, designed to bring the power of Multi-Factor Authentication (MFA) to your desktop computing environment. [Know more](https://www.ironchip.com/en/mobileless-authentication).

**Role-based privilege management:** Set different user privileges to prevent unauthorized users from misusing the system.

**Restrict access from unauthorized places:** Limit access to authorized areas for enhanced security.

**Supervision of accesses in real time:** Monitor user activity, view access history, generate reports, and download them for complete control.

**Intrusion detection system (IDS):** Receive alerts for SIM swapping, phishing, device switching, and more.

---

### Download

Download the latest Ironchip PAM module for Linux (`.so` file):

<p align="left">
  <a href="https://github.com/Ironchip-Security/Ironchip-Linux-Logon/releases/latest/download/ironchip-pam-installer.tar.gz">
    <img alt="Download Ironchip Module" src="https://custom-icon-badges.demolab.com/badge/-Download%20Module-blue?style=for-the-badge&logo=download&logoColor=white">
  </a>
</p>

---

### Basic Usage

Once you've downloaded the `.so` file:

1. Move it to a secure directory:
   ```bash
   sudo mv pam_ironchip_auth.so /usr/local/lib/security/
   ```

2. Edit your desired PAM configuration file (e.g., `/etc/pam.d/sudo`) and add:
   ```bash
   auth required /usr/local/lib/security/pam_ironchip_auth.so host=https://api.ironchip.com api_key=<your_api_key>
   ```

3. Save and close the file (`Ctrl+O`, `Enter`, `Ctrl+X` if using `nano`).

4. Assign access from the [Ironchip Dashboard](https://app.ironchip.com).

---

## Ironchip PAM for Linux

### What it is

This PAM module integrates Ironchip Multi-Factor Authentication (MFA) into the Linux login flow, administrator actions (`sudo`), SSH sessions, and more.

---

## Installation & Configuration

> **Important:** This process can cause permanent system and user locks if not executed correctly. Keep a terminal with administrator permissions open during the process to avoid any irreparable error. It is recommended to first test the integration with `sudo` authentication to avoid being locked out of the system.

### Step 1: Install dependencies (if needed)

Run the following command to install required packages:

```bash
sudo apt-get install libcurl4-openssl-dev libpam-dev uuid-dev
```

### Step 2: Create PAM directory

Create a secure directory to store the module:

```bash
sudo mkdir -p /usr/local/lib/security
```

### Step 3: Move PAM module

Move the downloaded PAM module into the new directory:

```bash
sudo mv pam_ironchip_auth.so /usr/local/lib/security/
```

### Step 4: Configure PAM

Go to `/etc/pam.d/` and edit one of the following files depending on your needs:

- `sudo`: authentication for sudo commands
- `sshd`: authentication for remote SSH
- `gdm-password`: authentication for login GUI
- `common-auth`: apply authentication system-wide

**Example: Add MFA to sudo**

```bash
sudo nano /etc/pam.d/sudo
```

Add the following line at the top:

```bash
auth required /usr/local/lib/security/pam_ironchip_auth.so host=https://api.ironchip.com api_key=<your_api_key>
```

Replace `<your_api_key>` with the actual key provided by Ironchip.

Save and exit: `Ctrl+O`, `Enter`, then `Ctrl+X`.

---

### Uninstall / Revert

To remove Ironchip PAM integration:

1. Remove the added line from the modified `/etc/pam.d/` file.
2. Delete the PAM module:

```bash
sudo rm /usr/local/lib/security/pam_ironchip_auth.so
```

---

### 📘 Documentation

For more information and advanced options, visit the <a href="https://docs.ironchip.com/en/linux-logon" target="_blank" rel="noopener noreferrer">Ironchip Linux documentation</a>.

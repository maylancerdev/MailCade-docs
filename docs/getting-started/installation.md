# Installation

Get MailCade installed on your machine in minutes.

## System Requirements

- **macOS**: 11 or later
- **Windows**: 10 or later  
- **Linux**: Ubuntu 20.04+, Fedora 35+, or similar

## Download

Download the latest version for your platform from the [GitHub releases page](https://github.com/olakunlevpn/MailCade/releases):

- **macOS**: `MailCade-{version}-arm64.dmg`
- **Windows**: `MailCade-Setup-{version}.exe`
- **Linux**: `MailCade-{version}.AppImage`, `.deb`, or `.rpm`

## Installation

### macOS

1. Download `MailCade-{version}-arm64.dmg`
2. Open the DMG file
3. Drag MailCade to Applications
4. Launch from Applications folder

**Security Note**: If macOS blocks the app:
- Go to **System Settings → Privacy & Security**
- Click **"Open Anyway"** next to MailCade

### Windows

1. Download `MailCade-Setup-{version}.exe`
2. Run the installer
3. Follow setup wizard
4. Launch from Start menu or desktop shortcut

### Linux

**AppImage:**
```bash
chmod +x MailCade-{version}.AppImage
./MailCade-{version}.AppImage
```

**Debian/Ubuntu (.deb):**
```bash
sudo dpkg -i MailCade-{version}.deb
mailcade
```

**Fedora/RHEL (.rpm):**
```bash
sudo rpm -i MailCade-{version}.x86_64.rpm
mailcade
```

## First Launch

When you open MailCade for the first time:

1. The SMTP server starts automatically on **port 1025**
2. The inbox is empty
3. You're ready to catch emails

No configuration needed!

## What's Next?

- [Quick Start Guide](quickstart.md) - Send your first test email
- [Configuration](configuration.md) - Customize ports and settings

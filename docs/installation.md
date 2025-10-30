# Installation

Getting MailCade up and running takes about 5 minutes. Here's how.

## System Requirements

- **macOS** 11 or later
- **Windows** 10 or later
- **Linux** (Ubuntu 20.04+, Fedora 35+, or similar)

That's it. No Docker, no database setup, no configuration files to wrestle with.

## Download

Grab the latest version for your platform:

- **macOS**: `MailCade-{version}.dmg`
- **Windows**: `MailCade-Setup-{version}.exe`
- **Linux**: `MailCade-{version}.AppImage` (or `.deb`/`.rpm`)

Find the latest release on the [GitHub releases page](https://github.com/olakunlevpn/MailCade/releases).

## Installation Steps

### macOS

1. Open the `.dmg` file
2. Drag MailCade to your Applications folder
3. Launch MailCade from Applications
4. If you see a security warning, go to **System Settings → Privacy & Security** and click "Open Anyway"

### Windows

1. Run `MailCade-Setup-{version}.exe`
2. Follow the installer prompts
3. Launch MailCade from the Start menu

### Linux

#### AppImage
```bash
chmod +x MailCade-{version}.AppImage
./MailCade-{version}.AppImage
```

#### Debian/Ubuntu (.deb)
```bash
sudo dpkg -i MailCade-{version}.deb
mailcade
```

#### Fedora/RHEL (.rpm)
```bash
sudo rpm -i MailCade-{version}.rpm
mailcade
```

## First Launch

When you first open MailCade:

1. The email server starts automatically on port `1025`
2. The inbox is empty (obviously)
3. You're ready to catch emails

That's it. No signup, no configuration, no hassle.

## What's Next?

- [Configure your app](configuration.md) to send emails to MailCade
- [Start testing](testing-emails.md) your email flows

## Having Trouble?

Check the [Troubleshooting guide](troubleshooting.md) or [open an issue](https://github.com/olakunlevpn/MailCade/issues).

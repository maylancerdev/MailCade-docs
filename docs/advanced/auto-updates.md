# Auto-Updates

Keep MailCade up to date with automatic updates.

## How It Works

MailCade checks for updates automatically:

1. **On startup** - Checks 5 seconds after launch
2. **Periodically** - Checks every 24 hours (if enabled)
3. **Manually** - Via Settings → Updates

When an update is available:
- Notification appears in Settings
- Download happens in background
- You choose when to install

## Checking for Updates

### Automatic Check

**Settings → General → Auto-update**

**Default**: Enabled

Automatically checks for updates and notifies you.

### Manual Check

**Settings → Updates → Check for Updates**

Click to check immediately. Shows:
- Current version
- Latest version
- Release notes
- Download button

## Installing Updates

### Automatic Download

When update is found:
1. Download starts automatically
2. Progress shown in Settings
3. Notification when ready
4. Click "Install Update" to apply

### Manual Installation

1. Go to Settings → Updates
2. Click "Download Update"
3. Wait for download
4. Click "Install and Restart"
5. MailCade restarts with new version

## Update Process

### What Happens

1. **Download** - New version downloads in background
2. **Verify** - Checksum verification ensures integrity
3. **Install** - Replaces old version on restart
4. **Migrate** - Settings carry over automatically

### Your Data

- ✅ **Settings preserved** - All configuration kept
- ✅ **Emails preserved** - Current emails remain
- ✅ **No data loss** - Safe to update anytime

### Timing

**Update anytime**. There's no "bad time" to update.

However, if you're in the middle of important testing:
- Complete your test
- Then install update
- Or install later (update waits for you)

## Update Channels

### Stable (Default)

Production releases only. Tested and stable.

**Recommended for**: Everyone

**Update frequency**: Every few weeks/months

### Beta (Coming Soon)

Early access to new features. May have bugs.

**Recommended for**: Developers, contributors, testers

**Update frequency**: Weekly or more

## Skipping Updates

You can skip an update:

1. Check for updates
2. See update notification
3. Click "Skip This Version"
4. Won't notify about that version again

Next version will still notify normally.

## Offline Updates

If you're offline when update is available:

1. Download later when online
2. Or manually download from GitHub
3. Install `.dmg` / `.exe` / `.AppImage` manually

## Troubleshooting Updates

### Update Check Fails

**Causes**:
- No internet connection
- GitHub API rate limit
- Firewall blocking requests

**Solution**:
- Check internet connection
- Try again in a few minutes
- Manually download from releases page

### Download Fails

**Causes**:
- Connection interrupted
- Insufficient disk space
- Firewall blocking download

**Solution**:
- Retry download
- Free up disk space
- Check firewall settings
- Manual download as fallback

### Install Fails

**Rare, but possible**:

**macOS**: Remove old app, install new one manually  
**Windows**: Run installer as administrator  
**Linux**: Check file permissions

### Update Won't Install

1. Quit MailCade completely
2. Manually download new version
3. Install over old version
4. Launch new version

## Version History

Check what's new:

**Settings → About → Version**

Shows:
- Current version
- Last update date
- Change log link

Or visit: https://github.com/olakunlevpn/MailCade/releases

## Delta Updates

MailCade uses **delta updates** when possible:

- Downloads only changed files
- Faster updates
- Less bandwidth
- Uses `.blockmap` files

First install requires full download.

## Disabling Auto-Update

Not recommended, but possible:

**Settings → General → Auto-update** → Toggle OFF

You'll need to manually check for updates.

## Release Notifications

Get notified about new releases:

1. Watch the repository on GitHub
2. Star the repo for updates
3. Follow release notes

## Security

Updates are secure:

- ✅ **HTTPS downloads** - Encrypted transfer
- ✅ **Checksum verification** - File integrity checked
- ✅ **GitHub releases** - Official source
- ✅ **Code signed** - Verified publisher (macOS)

## What's Next?

- [Troubleshooting](troubleshooting.md) - Fix common issues
- [Contributing](../development/contributing.md) - Help improve MailCade

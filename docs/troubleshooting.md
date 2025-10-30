# Troubleshooting

Running into issues? Here's how to fix the most common problems.

## Server Won't Start

### Check if Port is Already in Use

**Symptoms**: Server shows as stopped, or error message about port being in use.

**Solution**:

```bash
# macOS/Linux - Check what's using port 1025
lsof -i :1025

# Windows - Check what's using port 1025
netstat -ano | findstr :1025
```

**Fix**:
1. Kill the process using the port, OR
2. Change MailCade's SMTP port:
   - Go to **Settings → Server Configuration**
   - Change **SMTP Port** to something else (e.g., `1026`)
   - Click **Restart Server**

### Permission Issues (Linux/macOS)

**Symptoms**: Server fails to start with permission errors.

**Solution**:

Ports below 1024 require root access. Use a higher port number (1025+) instead.

## Emails Not Appearing

### Verify Server is Running

Look at the sidebar:
```
Email Server ● Running  ✅
```

If it says **Stopped**:
1. Click the gear icon ⚙️
2. Click **Start Server**

### Check Your App's Configuration

Make sure your application is sending to:
```
Host: localhost
Port: 1025  (or whatever you configured)
```

**Common mistakes**:
- Using `127.0.0.1` instead of `localhost` (usually fine, but try both)
- Wrong port number
- TLS/SSL enabled (MailCade doesn't use encryption for local dev)
- Authentication enabled (MailCade doesn't require auth)

### Test with Curl

Rule out your application as the problem:

```bash
curl -v smtp://localhost:1025 \
  --mail-from test@example.com \
  --mail-rcpt recipient@example.com \
  --upload-file - <<EOF
Subject: Test from Curl

If you see this, MailCade is working!
EOF
```

If this works but your app doesn't, the issue is in your application's email configuration.

## WebSocket Issues

### Symptoms
- Emails appear after manual refresh
- Real-time updates not working
- Console errors about WebSocket

### Solution

WebSocket connection is automatic, but if it fails:

1. Check if API port is accessible:
```bash
curl http://localhost:8025/api/v1/messages
```

2. If that fails, restart MailCade completely

3. Check firewall settings (rare, but possible)

## Performance Issues

### Inbox Feels Slow

**If you have thousands of test emails**:

1. Go to **Settings → Server Configuration**
2. Lower **Email Retention** to `100` or `200`
3. Old emails will auto-delete
4. Inbox will speed up

### High CPU Usage

**Symptoms**: Fan spinning, battery draining fast.

**Likely cause**: You're rapidly sending thousands of emails.

**Solution**: Slow down email sending in your tests, or pause between batches.

## UI Issues

### Dark Mode Not Working

1. Check your system's dark mode setting
2. Restart MailCade
3. If still broken, go to **Settings** and toggle themes manually

### Window Too Small/Large

The window size is saved automatically. To reset:

1. Quit MailCade completely
2. Relaunch it
3. Resize to your preferred size

### Text Cut Off or Weird Layout

**Try**:
1. Zoom reset: `Cmd/Ctrl + 0`
2. Restart MailCade
3. Update to the latest version

## Installation Issues

### macOS: "App is Damaged"

**Full error**: "MailCade is damaged and can't be opened"

**Solution**:
```bash
xattr -cr /Applications/MailCade.app
```

Then try launching again.

### macOS: Security Warning

**Error**: "MailCade can't be opened because it is from an unidentified developer"

**Solution**:
1. Go to **System Settings → Privacy & Security**
2. Scroll down to the security message
3. Click **Open Anyway**
4. Launch MailCade again

### Windows: SmartScreen Warning

**Solution**:
1. Click **More info**
2. Click **Run anyway**

This happens because the app isn't signed with a certificate yet.

### Linux: AppImage Won't Run

**Make it executable**:
```bash
chmod +x MailCade-*.AppImage
./MailCade-*.AppImage
```

**If you get FUSE errors**:
```bash
# Extract and run directly
./MailCade-*.AppImage --appimage-extract
./squashfs-root/mailcade
```

## Update Issues

### Update Check Fails

**Symptoms**: "Failed to check for updates" message.

**Causes**:
- No internet connection
- GitHub is down (rare)
- Firewall blocking requests

**Solution**: Check your internet connection and try again later. Or manually download from GitHub releases.

### Update Download Stuck

1. Cancel the download
2. Manually download from [GitHub releases](https://github.com/olakunlevpn/MailCade/releases)
3. Install manually

## Platform-Specific Issues

### macOS: Icon Not Showing in Dock

Restart MailCade. If that doesn't work:
```bash
killall Dock
```

### Windows: Tray Icon Missing

Check your system tray settings:
1. **Settings → Personalization → Taskbar**
2. Make sure MailCade is allowed in the system tray

### Linux: Font Rendering Issues

Install required fonts:
```bash
# Ubuntu/Debian
sudo apt install fonts-liberation

# Fedora
sudo dnf install liberation-fonts
```

Then restart MailCade.

## Still Stuck?

### Check the Logs

**macOS**:
```bash
~/Library/Logs/MailCade/
```

**Windows**:
```
%APPDATA%\MailCade\logs\
```

**Linux**:
```bash
~/.config/MailCade/logs/
```

Look for error messages that might give you a clue.

### Get Help

1. Check [existing GitHub issues](https://github.com/olakunlevpn/MailCade/issues)
2. If your problem isn't listed, [open a new issue](https://github.com/olakunlevpn/MailCade/issues/new)

When reporting issues, include:
- Your OS and version
- MailCade version (find it in **Settings → About**)
- Error messages (if any)
- Steps to reproduce the problem

### Common "Not a Bug" Issues

**"MailCade doesn't actually send emails"**  
That's intentional. MailCade is a local testing tool. It catches emails so they don't get sent.

**"I can't access MailCade from another computer"**  
Also intentional. MailCade only accepts emails from `localhost`. For team testing, everyone runs their own instance.

**"Emails don't have DKIM/SPF headers"**  
MailCade is for testing content and functionality, not email authentication. Test those on staging with real mail servers.

## Prevention Tips

**Keep MailCade Updated**  
Check for updates regularly in **Settings → Updates**.

**Don't Send Gigantic Emails**  
If you're testing with large attachments (10MB+), expect slower performance. That's normal.

**Clean Your Inbox**  
Set a reasonable retention limit. You don't need 10,000 test emails sitting there.

**Use Different Ports for Different Projects**  
Avoid port conflicts by planning ahead.

---

That covers the most common issues. If you're still stuck, we're here to help on GitHub!

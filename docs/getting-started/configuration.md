# Configuration

Customize MailCade to fit your workflow.

## Default Configuration

Out of the box, MailCade uses:

- **SMTP Port**: 1025
- **API Port**: 8025 (internal)
- **Email Retention**: 500 emails
- **Auto-start**: Enabled

## Changing Ports

**Settings → Server Configuration**

### SMTP Port

The port where your app sends emails.

**Default**: 1025  
**Range**: 1-65535

After changing, click **Restart Server**.

### API Port

Internal communication port for the web UI.

**Default**: 8025  
**Range**: 1-65535

Most users don't need to change this.

## Email Retention

**Settings → Server Configuration → Email Retention**

Maximum emails to keep before auto-deletion.

**Default**: 500  
**Range**: 10 - 10,000

Older emails are automatically removed when the limit is reached.

## App Settings

### Auto-start Server

**Settings → General → Auto-start Server**

Start the email server when MailCade launches.

**Default**: Enabled  
**Recommendation**: Keep it ON

### Desktop Notifications

**Settings → General → Desktop Notifications**

Get notified when new emails arrive.

**Default**: Enabled

### Theme

**Settings → General → Theme**

Choose your theme:
- **Light**
- **Dark**
- **System** (follows OS settings)

## Server Controls

Quick access to server controls:

1. Look at sidebar → **Email Server** section
2. Click the **gear icon** ⚙️
3. Access Start/Stop/Restart buttons

## Multiple Projects

Running multiple apps? Two options:

**Option 1: Different ports per project**
```
Project A → localhost:1025
Project B → localhost:1026
Project C → localhost:1027
```

Change the SMTP port in MailCade for each testing session.

**Option 2: Same port for all**

All projects send to `localhost:1025`. All emails appear in one inbox.

## Advanced: Environment Variables

If building from source, customize branding with a `.env` file:

```env
VITE_APP_NAME=MailCade
VITE_AUTHOR_NAME=Your Name
VITE_AUTHOR_LINK=https://yoursite.com
VITE_WEBSITE_LINK=https://yoursite.com/mailcade
VITE_DOCS_LINK=https://yoursite.com/docs
VITE_GITHUB_REPO=https://github.com/you/mailcade
```

Then rebuild:
```bash
npm run electron:build
```

## What's Next?

- [Sending Emails](../usage/sending-emails.md) - Connect your applications
- [Settings](../advanced/settings.md) - Deep dive into all settings

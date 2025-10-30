# Configuration

MailCade works out of the box, but you can customize it to fit your workflow.

## Quick Setup: Connect Your App

Point your application to send emails to:

```
Host: localhost
Port: 1025
```

That's the default SMTP configuration. No authentication required.

### Examples

**Laravel (.env)**
```env
MAIL_MAILER=smtp
MAIL_HOST=localhost
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
```

**Node.js (Nodemailer)**
```javascript
const transporter = nodemailer.createTransport({
  host: 'localhost',
  port: 1025,
  secure: false,
  auth: false
});
```

**Python (smtplib)**
```python
import smtplib

server = smtplib.SMTP('localhost', 1025)
server.sendmail(from_addr, to_addr, message)
server.quit()
```

**Rails (config/environments/development.rb)**
```ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address: 'localhost',
  port: 1025
}
```

## Customizing MailCade

### Changing Ports

**Settings → Server Configuration**

- **SMTP Port**: Where your app sends emails (default: `1025`)
- **API Port**: Internal communication (default: `8025`)

After changing ports, click **Restart Server**.

### Email Retention

**Settings → Server Configuration → Email Retention**

Set how many emails to keep. Older emails are auto-deleted when the limit is reached.

- **Default**: 500 emails
- **Range**: 10 - 10,000 emails

Good for keeping your inbox clean during long testing sessions.

### Auto-Start Server

**Settings → General → Auto-start Server**

Toggle this if you want the email server to start automatically when you launch MailCade.

We recommend keeping this **ON** so you don't forget to start it.

### Desktop Notifications

**Settings → General → Desktop Notifications**

Get notified when new emails arrive. Great when you're testing in the background.

## Environment Variables (For Building from Source)

If you're building MailCade yourself, you can customize branding:

**Create `.env` file:**
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

Your custom branding will appear in menus, about dialogs, and links.

## Server Controls

Access server controls quickly:

1. Look at the sidebar (bottom)
2. See **Email Server ● Running**
3. Click the **gear icon** ⚙️
4. You'll jump straight to server settings

From there you can:
- **Start/Stop** the server
- **Restart** after configuration changes
- **Change ports** (requires restart)

## Common Scenarios

### Testing Multiple Apps

Running multiple projects? No problem.

**Option 1: Use different ports per project**
```
Project A → localhost:1025
Project B → localhost:1026
Project C → localhost:1027
```

Change the SMTP port in MailCade settings for each session.

**Option 2: Use the same port**

All projects send to `localhost:1025`. You'll see emails from all projects in one inbox. Filter by subject or sender if needed.

### Testing Production-Like Emails

Want to test with real email addresses without actually sending?

Just send to any email address through MailCade:
```
To: customer@example.com
```

MailCade catches it. The email never leaves your machine. Perfect for testing customer notifications without bothering anyone.

## Resetting to Defaults

1. Go to **Settings → Server Configuration**
2. Set **SMTP Port** to `1025`
3. Set **API Port** to `8025`
4. Set **Email Retention** to `500`
5. Click **Save Settings**
6. Restart the server

You're back to defaults.

## What's Next?

Now that MailCade is configured, let's [send some test emails](testing-emails.md).

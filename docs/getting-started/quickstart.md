# Quick Start

Get started with MailCade in 5 minutes.

## Step 1: Launch MailCade

Open MailCade. The SMTP server starts automatically on **port 1025**.

Check the sidebar to confirm:
```
Email Server ● Running
Port: 1025
```

## Step 2: Configure Your App

Point your application to send emails to MailCade:

```
Host: localhost
Port: 1025
```

**No authentication required.**

### Quick Examples

**Laravel (.env):**
```env
MAIL_MAILER=smtp
MAIL_HOST=localhost
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
```

**Node.js (Nodemailer):**
```javascript
const transporter = nodemailer.createTransport({
  host: 'localhost',
  port: 1025,
  secure: false
});
```

**Python:**
```python
import smtplib

server = smtplib.SMTP('localhost', 1025)
server.sendmail('from@example.com', 'to@example.com', 'Hello!')
server.quit()
```

**Rails:**
```ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address: 'localhost',
  port: 1025
}
```

## Step 3: Send a Test Email

Send an email from your app or test with curl:

```bash
curl smtp://localhost:1025 \
  --mail-from test@example.com \
  --mail-rcpt recipient@example.com \
  --upload-file - <<EOF
Subject: My First Test

Hello from MailCade!
EOF
```

## Step 4: View Your Email

The email appears instantly in MailCade's inbox. Click it to:

- View HTML or plain text content
- Inspect headers
- Read metadata
- Delete or forward

That's it! You're ready to test emails.

## What's Next?

- [Configuration](configuration.md) - Customize settings
- [Sending Emails](../usage/sending-emails.md) - More integration examples
- [Testing Workflows](../usage/testing-workflows.md) - Test real scenarios

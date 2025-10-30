# Sending Emails

Connect your applications to MailCade.

## Basic Configuration

Point your app to send emails to:

```
Host: localhost
Port: 1025
Authentication: None
Encryption: None
```

## Framework Examples

### Laravel

**config/mail.php** or **.env**:
```env
MAIL_MAILER=smtp
MAIL_HOST=localhost
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="noreply@example.com"
MAIL_FROM_NAME="${APP_NAME}"
```

Send a test:
```php
Mail::to('user@example.com')->send(new WelcomeEmail());
```

### Node.js

**Nodemailer:**
```javascript
const nodemailer = require('nodemailer');

const transporter = nodemailer.createTransport({
  host: 'localhost',
  port: 1025,
  secure: false,
  auth: false
});

transporter.sendMail({
  from: 'sender@example.com',
  to: 'recipient@example.com',
  subject: 'Test Email',
  text: 'Hello from Node.js!',
  html: '<p>Hello from Node.js!</p>'
});
```

### Python

**smtplib:**
```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

msg = MIMEMultipart('alternative')
msg['Subject'] = 'Test Email'
msg['From'] = 'sender@example.com'
msg['To'] = 'recipient@example.com'

text = "Hello from Python!"
html = "<p>Hello from Python!</p>"

msg.attach(MIMEText(text, 'plain'))
msg.attach(MIMEText(html, 'html'))

server = smtplib.SMTP('localhost', 1025)
server.sendmail('sender@example.com', 'recipient@example.com', msg.as_string())
server.quit()
```

**Django:**
```python
# settings.py
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'localhost'
EMAIL_PORT = 1025
EMAIL_USE_TLS = False

# Send email
from django.core.mail import send_mail

send_mail(
    'Test Subject',
    'Test message.',
    'from@example.com',
    ['to@example.com'],
    fail_silently=False,
)
```

### Ruby on Rails

**config/environments/development.rb:**
```ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address: 'localhost',
  port: 1025,
  enable_starttls_auto: false
}

config.action_mailer.default_url_options = {
  host: 'localhost',
  port: 3000
}
```

Send a test:
```ruby
UserMailer.welcome_email(@user).deliver_now
```

### PHP

**Native PHP:**
```php
<?php
ini_set('SMTP', 'localhost');
ini_set('smtp_port', 1025);

$to = 'recipient@example.com';
$subject = 'Test Email';
$message = 'Hello from PHP!';
$headers = 'From: sender@example.com';

mail($to, $subject, $message, $headers);
?>
```

### Go

**Using net/smtp:**
```go
package main

import (
    "fmt"
    "net/smtp"
)

func main() {
    from := "sender@example.com"
    to := []string{"recipient@example.com"}
    
    msg := []byte("To: recipient@example.com\r\n" +
        "Subject: Test Email\r\n" +
        "\r\n" +
        "Hello from Go!\r\n")
    
    err := smtp.SendMail("localhost:1025", nil, from, to, msg)
    if err != nil {
        fmt.Println(err)
    }
}
```

### Java

**Using JavaMail:**
```java
Properties props = new Properties();
props.put("mail.smtp.host", "localhost");
props.put("mail.smtp.port", "1025");

Session session = Session.getInstance(props);

try {
    Message message = new MimeMessage(session);
    message.setFrom(new InternetAddress("sender@example.com"));
    message.setRecipients(Message.RecipientType.TO,
        InternetAddress.parse("recipient@example.com"));
    message.setSubject("Test Email");
    message.setText("Hello from Java!");

    Transport.send(message);
} catch (MessagingException e) {
    e.printStackTrace();
}
```

## Testing with cURL

Quick command-line test:

```bash
curl smtp://localhost:1025 \
  --mail-from test@example.com \
  --mail-rcpt recipient@example.com \
  --upload-file - <<EOF
From: test@example.com
To: recipient@example.com
Subject: Test from cURL

This is a test email!
EOF
```

## Docker Containers

If your app runs in Docker, use your host machine's IP instead of `localhost`:

**macOS/Windows:**
```yaml
# docker-compose.yml
environment:
  MAIL_HOST: host.docker.internal
  MAIL_PORT: 1025
```

**Linux:**
```yaml
# docker-compose.yml
extra_hosts:
  - "host.docker.internal:host-gateway"
environment:
  MAIL_HOST: host.docker.internal
  MAIL_PORT: 1025
```

## Troubleshooting

**Emails not appearing?**

1. Check server is running (sidebar shows "● Running")
2. Verify correct host (`localhost`) and port (`1025`)
3. Disable TLS/SSL in your app
4. Disable authentication in your app
5. Test with curl to isolate the issue

**Connection refused?**

- Check firewall settings
- Try `127.0.0.1` instead of `localhost`
- Verify port isn't already in use

## What's Next?

- [Viewing Emails](viewing-emails.md) - Read and inspect emails
- [Testing Workflows](testing-workflows.md) - Test real scenarios

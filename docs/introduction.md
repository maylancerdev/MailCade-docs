# Introduction

**MailCade** is a developer-friendly email testing sandbox for local development.

It captures all outgoing emails from your applications, so you can test email functionality without spamming real inboxes or configuring external SMTP services.


![MailCade Screenshot](/images/cover.png)


---

## What is MailCade?

MailCade is a desktop application that runs a local SMTP server with a clean, modern UI for viewing captured emails. It's perfect for:

- **Testing user registration emails** - Verify welcome emails and activation links
- **Debugging email templates** - Check HTML rendering and responsive design
- **Verifying transactional emails** - Test order confirmations, password resets, etc.
- **Developing email features** - Build and test without sending real emails

---

## Key Features

### 📧 Local SMTP Server
Runs on `localhost:1025` by default. No configuration needed.

### 🎨 Modern UI
Clean interface with dark mode support for viewing and inspecting emails.

### 🚀 Zero Configuration
Works out of the box. Just point your app to `localhost:1025` and start testing.

### 🔒 Fully Local
No cloud services, no external dependencies, complete privacy.

### ⚡ Fast & Lightweight
Minimal resource usage, instant email display.

### 🌐 Cross-Platform
Available for macOS, Windows, and Linux.

---

## Quick Example

**1. Launch MailCade**  
The SMTP server starts automatically.

**2. Configure your app**
```env
MAIL_HOST=localhost
MAIL_PORT=1025
```

**3. Send a test email**
```bash
curl smtp://localhost:1025 \
  --mail-from test@example.com \
  --mail-rcpt user@example.com \
  --upload-file email.txt
```

**4. View in MailCade**  
Email appears instantly in the inbox.

---

## Who Is This For?

- **Full-stack developers** testing authentication flows
- **Backend developers** verifying email notifications
- **Frontend developers** checking email template rendering
- **QA engineers** testing email functionality
- **Anyone** who needs to test emails locally

---

## How It Works

MailCade bundles [Mailpit](https://mailpit.axllent.org/), a powerful email testing tool, into a beautiful desktop application with:

- Automatic server management
- Cross-platform binary handling
- Persistent settings
- Auto-update functionality
- Native desktop experience

---

## What MailCade Is NOT

- ❌ **Not a production email server** - For development/testing only
- ❌ **Not an email client** - Doesn't send or receive real emails
- ❌ **Not a mail relay** - Emails stay local, never leave your machine

---

## Getting Started

Ready to start testing emails?

→ **[Installation Guide](getting-started/installation.md)** - Install MailCade on your machine

→ **[Quick Start](getting-started/quickstart.md)** - Get up and running in 5 minutes

→ **[Table of Contents](toc.md)** - Browse all documentation

---

## Support

- **GitHub**: [github.com/olakunlevpn/MailCade](https://github.com/olakunlevpn/MailCade)
- **Issues**: [Report a bug or request a feature](https://github.com/olakunlevpn/MailCade/issues)
- **Releases**: [Download latest version](https://github.com/olakunlevpn/MailCade/releases)

---

**Ready to test emails like a pro?** Get started with the [installation guide](getting-started/installation.md)!

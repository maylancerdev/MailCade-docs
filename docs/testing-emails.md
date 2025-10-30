# Testing Emails

Let's catch and inspect some emails.

## Your First Test Email

### Step 1: Make Sure MailCade is Running

Look at the sidebar. You should see:
```
Email Server ● Running
Port: 1025
```

If it says **Stopped**, click the gear icon ⚙️ and click **Start Server**.

### Step 2: Send an Email from Your App

Use your application's normal email sending method. Here's a quick test with curl:

```bash
curl -v --url 'smtp://localhost:1025' \
  --mail-from 'sender@example.com' \
  --mail-rcpt 'recipient@example.com' \
  --upload-file - <<EOF
From: sender@example.com
To: recipient@example.com
Subject: Test Email

This is a test email!
EOF
```

### Step 3: See It in MailCade

The email appears instantly in the inbox. No refresh needed.

## Reading Emails

Click any email in the list to view it.

You'll see:

- **Sender** and **recipients**
- **Subject line**
- **Date/time** sent
- **Email body** (HTML or plain text)
- **Full headers** (on the Headers tab)

### Switching Between HTML and Text

Some emails have both HTML and plain text versions. Switch between them using the tabs:

- **Content**: HTML version (if available)
- **Text**: Plain text version
- **Headers**: Raw email headers

## Testing Common Scenarios

### User Registration Emails

1. Fill out your app's registration form
2. Check MailCade inbox
3. Verify the welcome email
4. Click links to test redirects (they work!)

### Password Reset Flows

1. Request a password reset in your app
2. Find the reset email in MailCade
3. Copy the reset link
4. Test the flow end-to-end

### Transactional Emails

Testing order confirmations, shipping notifications, etc:

1. Complete an action in your app
2. Check the email content
3. Verify dynamic data (order numbers, totals, etc.)
4. Confirm formatting looks good

### Email Templates

Perfect for testing design changes:

1. Send a test email
2. View it in MailCade (HTML tab)
3. Check layout, images, buttons
4. Make changes in your code
5. Send again and compare

No need to check multiple email clients. Get it right in MailCade first.

## Managing Your Inbox

### Deleting Emails

Click an email, then click the **Delete** button.

Or delete all emails at once:

1. Go to **Settings**
2. Find **Email Retention**
3. Set it to a very low number (like `10`)
4. Wait a few seconds
5. Old emails auto-delete

Then set it back to your preferred limit.

### Searching (Coming Soon)

Email search isn't available yet, but it's coming. For now:
- Use descriptive subjects during testing
- Delete old test emails regularly
- Keep your inbox manageable

## Forwarding Emails

Need to send a test email to your actual inbox?

1. Click an email
2. Click **Forward**
3. Your default email client opens
4. Send it to yourself

Great for testing on real devices or email clients.

## Reading Email Details

### Headers Tab

See technical details:

- **Message-ID**: Unique email identifier
- **MIME-Version**: Email format version
- **Content-Type**: HTML, text, or multipart
- **Custom Headers**: X-headers, tracking pixels, etc.

Useful for debugging delivery issues or testing SPF/DKIM (when you're ready for production).

### Metadata Section

Check:
- **From/To**: All recipients (including CC/BCC)
- **Date**: When it was sent
- **Size**: Email size in bytes

## Tips for Effective Testing

### 1. Test Edge Cases

Don't just test the happy path:
- Long email subjects
- Special characters in names
- Multiple recipients
- Large attachments (if your app sends them)
- Empty fields

### 2. Test Mobile Preview

Resize the MailCade window to see how emails look at different widths. Not perfect, but gives you an idea.

### 3. Keep Test Data Realistic

Use real-looking names and addresses:
```
✅ john.smith@example.com
❌ test@test.com
```

You'll catch typos and formatting issues.

### 4. Test Across Development Stages

- **Local dev**: Test functionality
- **Staging**: Test with production-like data
- **Pre-release**: Final checks before going live

Use MailCade at every stage.

## Automated Testing

MailCade is perfect for automated email tests.

### E2E Testing Example (Playwright)

```javascript
test('user receives welcome email', async ({ page }) => {
  // Register a new user
  await page.goto('http://localhost:3000/register');
  await page.fill('[name="email"]', 'newuser@example.com');
  await page.click('button[type="submit"]');
  
  // Check MailCade API for the email
  const response = await fetch('http://localhost:8025/api/v1/messages');
  const data = await response.json();
  
  const welcomeEmail = data.messages.find(
    email => email.To[0].Address === 'newuser@example.com'
  );
  
  expect(welcomeEmail).toBeDefined();
  expect(welcomeEmail.Subject).toContain('Welcome');
});
```

### API Access

MailCade exposes Mailpit's API on port `8025`:

```bash
# Get all emails
curl http://localhost:8025/api/v1/messages

# Get specific email
curl http://localhost:8025/api/v1/message/{id}

# Delete all emails
curl -X DELETE http://localhost:8025/api/v1/messages
```

Perfect for CI/CD pipelines.

## What If...

**Email doesn't appear?**  
Check [Troubleshooting](troubleshooting.md).

**Need to test with real mail servers?**  
MailCade is for development only. For staging/production testing, use real SMTP services like Mailtrap or your actual email provider.

**Want to test email delivery?**  
MailCade doesn't test delivery (SPF, DKIM, spam filters, etc.). It's for testing content and functionality. Use dedicated email testing services for delivery testing.

## Next Steps

You're now a MailCade pro! If you run into issues, check the [Troubleshooting guide](troubleshooting.md).

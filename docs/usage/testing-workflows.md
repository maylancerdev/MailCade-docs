# Testing Workflows

Test common email scenarios with MailCade.

## User Registration

**Test flow:**
1. Fill out registration form in your app
2. Submit the form
3. Check MailCade inbox for welcome email
4. Verify email content:
   - Correct recipient
   - Welcome message
   - Verification link (if applicable)
5. Click verification link
6. Confirm it redirects correctly

**What to check:**
- Email arrives within seconds
- Subject line is correct
- User's name appears (if personalized)
- Links work
- Images load
- Branding looks good

## Password Reset

**Test flow:**
1. Request password reset
2. Find reset email in MailCade
3. Copy reset link
4. Paste in browser
5. Reset password
6. Verify success

**What to check:**
- Reset link is unique
- Link expires correctly (test after timeout)
- Email warns about security
- Sender address is correct

## Order Confirmations

**Test flow:**
1. Complete a test order
2. Check MailCade for confirmation
3. Verify order details:
   - Order number
   - Items purchased
   - Total price
   - Shipping address
4. Check formatting and layout

**What to check:**
- Dynamic data is accurate
- Prices format correctly
- Tables display properly
- Receipt looks professional

## Email Templates

**Test flow:**
1. Send email with your template
2. View in MailCade
3. Check HTML rendering
4. Verify responsive design
5. Test in different window sizes

**What to check:**
- Colors match design
- Fonts load correctly
- Images appear
- Buttons are clickable
- Layout doesn't break
- Mobile preview looks good

## Transactional Emails

Common emails to test:

### Account Notifications
- Email address changed
- Password changed
- Two-factor authentication codes
- Login from new device

### Billing
- Payment received
- Payment failed
- Subscription renewal
- Refund processed

### Activity
- New follower
- New comment
- Message received
- Reminder notifications

## Multi-Recipient Emails

**Test with:**
- Multiple To addresses
- CC recipients
- BCC recipients (won't show in headers)

Verify:
- All recipients receive email
- BCC addresses stay hidden
- Reply-to works correctly

## Automated Testing

### API Testing

Access MailCade's API on `http://localhost:8025`:

```bash
# Get all messages
curl http://localhost:8025/api/v1/messages

# Get specific message
curl http://localhost:8025/api/v1/message/{id}

# Delete all messages
curl -X DELETE http://localhost:8025/api/v1/messages
```

### E2E Testing

**Playwright example:**
```javascript
test('user receives welcome email', async ({ page }) => {
  // Register user
  await page.goto('http://localhost:3000/register');
  await page.fill('[name="email"]', 'test@example.com');
  await page.click('button[type="submit"]');
  
  // Check MailCade API
  const response = await fetch('http://localhost:8025/api/v1/messages');
  const data = await response.json();
  
  const email = data.messages.find(
    m => m.To[0].Address === 'test@example.com'
  );
  
  expect(email).toBeDefined();
  expect(email.Subject).toContain('Welcome');
});
```

## Testing Best Practices

### Use Realistic Data

```
✅ john.smith@example.com
❌ test@test.com

✅ "Welcome to MailCade, John!"
❌ "Welcome to [APP], [USER]!"
```

### Test Edge Cases

- Very long subject lines
- Special characters in names
- International email addresses
- Multiple attachments
- Large email sizes

### Test Timing

- Immediate emails (welcome, confirmation)
- Delayed emails (reminder, follow-up)
- Scheduled emails (newsletter, digest)

### Test Failure Scenarios

- Invalid recipient
- Missing required fields
- Template render errors
- Link generation failures

## Regression Testing

Create a test checklist:

- [ ] User registration email
- [ ] Password reset email
- [ ] Order confirmation
- [ ] Shipping notification
- [ ] Newsletter signup
- [ ] Account deletion confirmation

Run through the checklist before each release.

## Performance Testing

Test with high volume:

```bash
# Send 1000 test emails
for i in {1..1000}; do
  curl smtp://localhost:1025 \
    --mail-from test@example.com \
    --mail-rcpt user$i@example.com \
    --upload-file email.txt
done
```

Check:
- MailCade remains responsive
- All emails appear
- Search/filter still works
- Memory usage is reasonable

## What's Next?

- [Settings](../advanced/settings.md) - Customize MailCade
- [Troubleshooting](../advanced/troubleshooting.md) - Fix issues

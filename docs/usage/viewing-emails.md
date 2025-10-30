# Viewing Emails

Read and inspect emails in MailCade.

## Email Inbox

The inbox shows all captured emails with:

- **Sender** address
- **Subject** line
- **Recipients** (To, CC, BCC)
- **Timestamp** when received
- **Preview** of email content

Click any email to view full details.

## Email Detail View

### Content Tab

View the email body:

- **HTML version** (if available)
- **Plain text version**
- Images and styling (rendered)

Switch between HTML and text using the tabs.

### Headers Tab

View technical email headers:

- **From/To/CC/BCC** - All recipients
- **Message-ID** - Unique identifier
- **Date** - Send timestamp
- **Content-Type** - MIME type
- **Custom headers** - X-headers, tracking, etc.

Useful for debugging delivery issues or testing email metadata.

### Raw Tab

See the complete raw email source including:

- All MIME parts
- Encoded content
- Full headers
- Boundaries

Perfect for debugging complex email formats.

## Email Actions

### Delete

Remove a single email:
1. Click the email
2. Click **Delete** button
3. Confirm deletion

### Forward

Send to your real inbox for testing:
1. Click the email
2. Click **Forward**
3. Your email client opens
4. Send to yourself

Great for testing on actual devices or email clients.

## Managing Emails

### Search

Coming soon! For now:
- Use descriptive subjects during testing
- Delete old emails regularly
- Keep inbox manageable

### Bulk Delete

Delete all emails:
1. **Settings → Server Configuration**
2. Set **Email Retention** to `10`
3. Wait a few seconds
4. Old emails auto-delete
5. Set retention back to preferred limit

Or restart the server to clear all emails.

### Filter by Sender/Recipient

Click email addresses in the inbox to filter (coming soon).

## Reading Tips

### Test Email Rendering

Resize the MailCade window to preview responsive email designs at different widths.

### Check Links

Links in emails are clickable. Test:
- Password reset links
- Verification links
- Unsubscribe links
- Call-to-action buttons

### Verify Attachments

Attachments are displayed. Check:
- File names appear correctly
- File sizes are reasonable
- Download links work

### Test Dynamic Content

Verify personalization:
- User names
- Order numbers
- Timestamps
- Custom data

Use real-looking test data to catch formatting issues.

## Email Metadata

Each email shows:

- **Size** - Total email size in bytes
- **Parts** - Number of MIME parts
- **Recipients** - All To/CC/BCC addresses
- **Thread** - Related emails (if applicable)

## Accessibility

MailCade supports:

- Keyboard navigation
- Screen reader compatibility
- High contrast mode
- Zoom support

## What's Next?

- [Testing Workflows](testing-workflows.md) - Test real email scenarios
- [Troubleshooting](../advanced/troubleshooting.md) - Fix common issues

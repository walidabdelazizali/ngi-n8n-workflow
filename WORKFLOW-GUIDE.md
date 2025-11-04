# n8n Workflow Guide - NGI Email Campaign

## Workflow Visualization

### Main Workflow (Scheduled)
```
┌─────────────────────┐
│  Schedule Trigger   │
│  (Daily at 9:00 AM) │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────────────────┐
│ Read Client Data from Google    │
│ Sheets                          │
│ - Reads: Name, Email, Message   │
└──────────┬──────────────────────┘
           │
           ▼
┌─────────────────────┐
│  Send Email via     │
│  Gmail              │
│  - Personalized     │
│  - Automated        │
└─────────────────────┘
```

## Workflow Files Overview

### 1. `ngi-email-workflow.json` (Recommended)
**Best for**: Automated daily email campaigns

**Features**:
- Scheduled trigger (runs daily at 9:00 AM)
- Google Sheets integration
- Automated execution

**Use Case**: Set it up once and forget it. Perfect for ongoing daily outreach campaigns.

### 2. `ngi-email-workflow-manual.json`
**Best for**: On-demand email campaigns

**Features**:
- Manual trigger (click to execute)
- Google Sheets integration
- User-controlled execution

**Use Case**: When you want to send emails on your own schedule or need to review data before sending.

### 3. `ngi-email-workflow-csv.json`
**Best for**: Working with local CSV files

**Features**:
- Scheduled trigger (daily at 9:00 AM)
- CSV file input
- No cloud storage required

**Use Case**: When you prefer to work with local CSV files instead of Google Sheets.

## Data Flow

### Input Data (Google Sheets / CSV)
```
┌──────────┬──────────────────────┬─────────────────────────┐
│   Name   │       Email          │        Message          │
├──────────┼──────────────────────┼─────────────────────────┤
│ John Doe │ john@example.com     │ Custom message here...  │
│ Jane S.  │ jane@example.com     │ Another message...      │
└──────────┴──────────────────────┴─────────────────────────┘
```

### Email Output
Each row is processed and generates a personalized email:

**To**: john@example.com  
**Subject**: Your Dubai Hills Mall Insurance – NGI  
**Body**:
```
Hello John Doe,

This is Waleed Abdelaziz from National General Insurance (NGI).
We help Dubai Hills Mall retailers get their required insurance coverage quickly and affordably.

Custom message here...

Please share your Trade License, VAT Certificate, and Employee Excel Sheet here:
[Google Form link]

Best regards,
Waleed Abdelaziz
Corporate Insurance Consultant
NGI – National General Insurance
```

## Step-by-Step Setup Checklist

### Phase 1: Preparation
- [ ] Install/Access n8n instance
- [ ] Create Google Sheet with columns: Name, Email, Message
- [ ] Populate sheet with client data
- [ ] Note down your Google Sheet ID (from URL)

### Phase 2: n8n Credentials Setup
- [ ] Configure Google Sheets OAuth2 credentials in n8n
- [ ] Configure Gmail OAuth2 credentials in n8n
- [ ] Test both credentials to ensure they work

### Phase 3: Import & Configure Workflow
- [ ] Import the workflow JSON file into n8n
- [ ] Update "Read Client Data from Google Sheets" node:
  - [ ] Set correct Google Sheet ID
  - [ ] Set correct Sheet name
  - [ ] Select Google Sheets credential
- [ ] Update "Send Email via Gmail" node:
  - [ ] Select Gmail credential
  - [ ] Update Google Form link (if applicable)

### Phase 4: Testing
- [ ] Click "Execute Workflow" to test
- [ ] Verify email sent to first contact
- [ ] Check for any errors in execution log
- [ ] Verify email content is correctly personalized

### Phase 5: Activation
- [ ] Toggle workflow to "Active"
- [ ] Verify schedule is correct (9:00 AM daily)
- [ ] Monitor first automated run

## Common Configuration Changes

### Change Schedule Time
Edit the cron expression in "Schedule Trigger" node:
- `0 9 * * *` → Daily at 9:00 AM
- `0 14 * * *` → Daily at 2:00 PM
- `0 9 * * 1-5` → Weekdays at 9:00 AM
- `0 9,17 * * *` → Daily at 9:00 AM and 5:00 PM

### Add BCC Recipients
In "Send Email via Gmail" node, add:
```
BCC: supervisor@ngi.ae
```

### Add Email Attachments
In "Send Email via Gmail" node:
1. Change `emailType` from "text" to "html"
2. Add attachments section
3. Configure file sources

## Troubleshooting Guide

### Problem: "Invalid credentials"
**Solution**: 
1. Go to n8n Credentials page
2. Re-authenticate Google Sheets/Gmail
3. Ensure tokens haven't expired

### Problem: "Sheet not found"
**Solution**:
1. Verify Google Sheet ID is correct
2. Ensure the sheet is shared with the authenticated Google account
3. Check sheet name matches exactly (case-sensitive)

### Problem: "Emails not sending"
**Solution**:
1. Check Gmail API is enabled in Google Cloud Console
2. Verify Gmail OAuth2 scopes include sending permissions
3. Check if sender email is correct
4. Review daily sending limits for Gmail

### Problem: "Workflow not running on schedule"
**Solution**:
1. Ensure workflow is set to "Active" (toggle switch)
2. Verify cron expression is correct
3. Check n8n instance is running continuously
4. Review execution logs for errors

## Best Practices

### Data Management
1. **Regular Backups**: Export your Google Sheet regularly
2. **Data Validation**: Ensure all emails are valid before running
3. **Test Data**: Create a test sheet with your own emails first

### Email Sending
1. **Start Small**: Test with 1-2 contacts before sending to all
2. **Monitor**: Check execution logs after first few runs
3. **Timing**: Avoid sending emails late at night or on weekends
4. **Personalization**: Keep the Message column updated with relevant info

### Performance
1. **Batch Size**: For large lists (100+ contacts), consider splitting into smaller batches
2. **Rate Limiting**: Be aware of Gmail API rate limits
3. **Error Handling**: Add error notifications to alert you of failures

## Security Notes

### Credentials
- Never share your n8n credential IDs publicly
- Use OAuth2 for Google services (more secure than API keys)
- Rotate credentials periodically

### Data Privacy
- Ensure client data is handled according to GDPR/privacy laws
- Don't store sensitive data in workflow variables
- Use secure connections (HTTPS) for n8n instance

### Access Control
- Limit access to n8n instance to authorized users only
- Use strong passwords for n8n login
- Enable 2FA if available

## Advanced Customization

### Add Conditional Logic
Insert an "IF" node to send different emails based on conditions:
```
IF: Message contains "VIP"
  → Send premium template
ELSE:
  → Send standard template
```

### Add Delay Between Emails
Insert a "Wait" node between reading data and sending:
- Prevents rapid-fire emails
- Appears more natural
- Reduces risk of rate limiting

### Add Tracking
Insert a Google Sheets "Append" node after email sending:
- Log sent emails with timestamp
- Track success/failure
- Create audit trail

## Support Resources

- **n8n Documentation**: https://docs.n8n.io
- **Community Forum**: https://community.n8n.io
- **Node Documentation**: Available in n8n UI for each node
- **Video Tutorials**: n8n YouTube channel

## Version History

- **v1.0** (2025-11-04): Initial workflow creation
  - Schedule trigger (daily 9 AM)
  - Google Sheets integration
  - Gmail sending
  - Manual and CSV variants

---

**Maintained by**: National General Insurance (NGI)  
**Contact**: Waleed Abdelaziz  
**Last Updated**: November 4, 2025

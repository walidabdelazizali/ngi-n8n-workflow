# Quick Start Guide - NGI Email Campaign

Get your automated email campaign running in under 10 minutes!

## Prerequisites
- [ ] n8n instance (cloud or self-hosted)
- [ ] Google account with Gmail
- [ ] Google Sheet with client data

## 5-Minute Setup

### Step 1: Prepare Your Google Sheet (1 minute)

1. Create a new Google Sheet
2. Add these column headers in row 1:
   ```
   Name | Email | Message
   ```
3. Add your client data:
   ```
   John Doe | john@example.com | We noticed your new store at the mall.
   Jane Smith | jane@example.com | Your business has been growing well.
   ```
4. Copy the Sheet ID from the URL:
   ```
   https://docs.google.com/spreadsheets/d/[THIS_IS_YOUR_SHEET_ID]/edit
   ```

### Step 2: Setup n8n Credentials (2 minutes)

#### Google Sheets:
1. In n8n, go to **Credentials** → **New**
2. Search for "Google Sheets"
3. Click **Connect My Account**
4. Authorize with your Google account
5. Copy the credential ID

#### Gmail:
1. In n8n, go to **Credentials** → **New**
2. Search for "Gmail"
3. Click **Connect My Account**
4. Authorize with your Google account
5. Copy the credential ID

### Step 3: Import Workflow (1 minute)

1. Download `ngi-email-workflow.json` from this repository
2. In n8n, click **Workflows** → **Import from File**
3. Select the downloaded JSON file
4. Click **Import**

### Step 4: Configure Workflow (2 minutes)

1. Open the imported workflow
2. Click on **"Read Client Data from Google Sheets"** node
3. Update:
   - **Document ID**: Paste your Google Sheet ID
   - **Sheet Name**: Enter "Sheet1" (or your sheet name)
   - **Credentials**: Select your Google Sheets credential
4. Click on **"Send Email via Gmail"** node
5. Update:
   - **Credentials**: Select your Gmail credential

### Step 5: Test & Activate (1 minute)

1. Click **"Execute Workflow"** (the play button)
2. Check if emails were sent successfully
3. If successful, toggle the workflow to **Active**
4. Done! 🎉

## What Happens Next?

✅ Your workflow will automatically run every day at 9:00 AM  
✅ It will read all rows from your Google Sheet  
✅ It will send a personalized email to each contact  
✅ You'll see execution logs in the n8n dashboard  

## First Test Run

**Important**: Before activating for real clients:

1. Create a test sheet with only YOUR email addresses
2. Run the workflow manually
3. Verify you receive the emails correctly
4. Check the email formatting and personalization
5. Then switch to your real client sheet

## Customization Options

### Change Send Time
Want to send at a different time?

1. Click on **"Schedule Trigger"** node
2. Change the cron expression:
   - `0 9 * * *` = 9:00 AM daily (default)
   - `0 14 * * *` = 2:00 PM daily
   - `0 9 * * 1-5` = 9:00 AM weekdays only

### Update Email Content
1. Click on **"Send Email via Gmail"** node
2. Edit the **"message"** field
3. Keep the `{{ $json.Name }}` and `{{ $json.Message }}` placeholders for personalization

### Use Manual Trigger Instead
Want to run it on-demand instead of scheduled?

1. Import `ngi-email-workflow-manual.json` instead
2. Click "Execute Workflow" whenever you want to send emails

## Common Issues & Quick Fixes

### "Permission denied" error
**Fix**: Re-authenticate your Google Sheets/Gmail credentials

### "Sheet not found" error
**Fix**: Double-check your Sheet ID and ensure the sheet is shared with your Google account

### Emails not sending
**Fix**: 
1. Verify Gmail API is enabled in Google Cloud Console
2. Check your Gmail daily sending limit (500/day for free accounts)

### Wrong email content
**Fix**: Check your Google Sheet columns are exactly: Name, Email, Message

## Need More Help?

- 📖 Read the full [README.md](README.md) for detailed instructions
- 🔧 Check [WORKFLOW-GUIDE.md](WORKFLOW-GUIDE.md) for advanced configuration
- 💬 Visit [n8n community forum](https://community.n8n.io) for support

## Pro Tips

💡 **Tip 1**: Add your own email to BCC to monitor all sent emails  
💡 **Tip 2**: Keep a backup copy of your Google Sheet  
💡 **Tip 3**: Start with a small batch (5-10 contacts) before scaling up  
💡 **Tip 4**: Use the manual trigger version for testing  
💡 **Tip 5**: Check execution logs daily for the first week  

---

**Ready to launch your email campaign? Let's go!** 🚀

Questions? Contact: Waleed Abdelaziz - National General Insurance (NGI)

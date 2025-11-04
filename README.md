# NGI n8n Workflow - Dubai Hills Mall Email Campaign

Automated Email Workflow for National General Insurance (NGI) – Dubai Hills Mall Campaign

## Overview

This n8n workflow automates sending personalized insurance outreach emails to Dubai Hills Mall retailers. The workflow reads client data from a Google Sheet and sends customized emails via Gmail.

## Features

- **Scheduled Trigger**: Runs daily at 9:00 AM automatically
- **Google Sheets Integration**: Reads client data (Name, Email, Message) from a Google Sheet
- **Personalized Emails**: Sends customized emails to each client
- **Professional Template**: Pre-configured email template for insurance outreach

## Workflow Structure

The workflow consists of 3 nodes:

1. **Schedule Trigger**: Executes the workflow daily at 9:00 AM (configurable)
2. **Read Client Data from Google Sheets**: Retrieves client information from your Google Sheet
3. **Send Email via Gmail**: Sends personalized emails to each client

## Prerequisites

Before importing this workflow into n8n, ensure you have:

1. **n8n instance** (self-hosted or cloud)
2. **Google Sheets API credentials** configured in n8n
3. **Gmail OAuth2 credentials** configured in n8n
4. **Google Sheet** with the following columns:
   - Name
   - Email
   - Message

## Google Sheet Setup

Create a Google Sheet with the following structure:

| Name | Email | Message |
|------|-------|---------|
| John Doe | john@example.com | Custom message for John |
| Jane Smith | jane@example.com | Custom message for Jane |

**Note**: The "Message" column can contain client-specific notes or additional information to be included in the email.

## Installation & Setup

### Step 1: Import the Workflow

1. Open your n8n instance
2. Click on **"Workflows"** → **"Import from File"**
3. Select the `ngi-email-workflow.json` file
4. The workflow will be imported with all nodes pre-configured

### Step 2: Configure Google Sheets Credentials

1. In n8n, go to **"Credentials"** → **"New"**
2. Select **"Google Sheets API"**
3. Follow the authentication process to connect your Google account
4. Copy the credential ID

### Step 3: Configure Gmail Credentials

1. In n8n, go to **"Credentials"** → **"New"**
2. Select **"Gmail"**
3. Follow the OAuth2 authentication process
4. Copy the credential ID

### Step 4: Update the Workflow

1. Open the imported workflow
2. Click on the **"Read Client Data from Google Sheets"** node
3. Update the following:
   - **Document ID**: Enter your Google Sheet ID (from the Sheet URL)
   - **Sheet Name**: Enter the name of your sheet (default: "Sheet1")
   - **Credentials**: Select your Google Sheets credential
4. Click on the **"Send Email via Gmail"** node
5. Update:
   - **Credentials**: Select your Gmail credential
   - Update the Google Form link in the email template if needed

### Step 5: Test the Workflow

1. Click **"Execute Workflow"** to test manually
2. Verify emails are sent correctly
3. Check for any errors in the execution log

### Step 6: Activate the Workflow

1. Toggle the workflow to **"Active"**
2. The workflow will now run automatically every day at 9:00 AM

## Email Template

The workflow sends the following email:

**Subject**: Your Dubai Hills Mall Insurance – NGI

**Body**:
```
Hello {{Name}},

This is Waleed Abdelaziz from National General Insurance (NGI).
We help Dubai Hills Mall retailers get their required insurance coverage quickly and affordably.

{{Message}}

Please share your Trade License, VAT Certificate, and Employee Excel Sheet here:
[Google Form link]

Best regards,
Waleed Abdelaziz
Corporate Insurance Consultant
NGI – National General Insurance
```

## Customization

### Modify Schedule

To change the schedule from daily at 9:00 AM:

1. Click on the **"Schedule Trigger"** node
2. Modify the **cron expression**: `0 9 * * *`
   - `0 9 * * *` = Daily at 9:00 AM
   - `0 9 * * 1-5` = Weekdays at 9:00 AM
   - `0 9,14 * * *` = Daily at 9:00 AM and 2:00 PM

### Customize Email Content

Edit the **"Send Email via Gmail"** node to modify:
- Subject line
- Email body text
- Add attachments (if needed)
- Change sender name/email

## Alternative: CSV File Input

If you prefer to use a CSV file instead of Google Sheets:

1. Replace the **"Read Client Data from Google Sheets"** node with a **"Read Binary File"** node
2. Add a **"CSV to JSON"** node to convert the CSV data
3. Ensure your CSV has columns: Name, Email, Message

## Troubleshooting

### Emails Not Sending

- Verify Gmail credentials are properly configured
- Check if Gmail API is enabled in your Google Cloud Console
- Ensure the sender email has permission to send emails

### Google Sheets Not Reading

- Verify the Sheet ID is correct
- Ensure the Google Sheets API is enabled
- Check that your Google account has access to the sheet

### Schedule Not Triggering

- Ensure the workflow is set to **"Active"**
- Verify the cron expression is correct
- Check n8n logs for any execution errors

## Support

For issues or questions:
- Check the n8n documentation: https://docs.n8n.io
- Review node-specific documentation in n8n UI

## License

This workflow is provided as-is for use by National General Insurance (NGI).

---

**Created for**: National General Insurance (NGI)  
**Campaign**: Dubai Hills Mall Retailer Outreach  
**Contact**: Waleed Abdelaziz - Corporate Insurance Consultant

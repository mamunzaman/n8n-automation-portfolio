# Candidate Application Automation

A two-stage multilingual recruiting workflow built with n8n. It captures candidate interest, prevents duplicate registrations, collects detailed application data, generates a structured candidate profile, exports it as PDF, stores the files in Google Drive, and sends confirmation and HR notification emails.

## Business Problem

Recruiting teams often receive incomplete candidate information across multiple forms and email threads. Manual duplicate checks, document generation, multilingual communication, and file organisation create delays and inconsistencies.

This automation standardises the process from first registration through candidate-profile generation and HR delivery.

## Included Workflows

### 1. Candidate Registration

- Receives an initial candidate-interest form through a webhook
- Normalises submitted data
- Checks Google Sheets for an existing email address
- Prevents duplicate registrations
- Generates a unique candidate ID
- Builds a personalised second-form URL
- Saves the candidate record to Google Sheets
- Sends success or duplicate notifications in German, English, or Spanish
- Returns a webhook response to the form frontend

### 2. Candidate Profile Generation

- Receives the detailed candidate form through a webhook
- Finds the original candidate record in Google Sheets
- Validates the submission and completion status
- Combines first-stage and second-stage data
- Copies a Google Docs candidate-profile template
- Replaces template placeholders with candidate data
- Exports the completed profile as PDF
- Stores the PDF in Google Drive
- Downloads the uploaded CV
- Updates the candidate record in Google Sheets
- Sends the candidate package to HR
- Sends confirmation emails in German, English, or Spanish
- Prevents repeated completion of the same application

## Technologies

- n8n
- Webhooks
- JavaScript Code nodes
- Google Sheets
- Google Docs API
- Google Drive
- Gmail
- Tally Forms
- PDF generation
- Multilingual email routing

## Repository Structure

```text
candidate-application-automation/
├── README.md
├── Candidate Registration.json
├── Candidate Profile Generation.json
├── Candidate_Profile_Google_Doc_Template.docx
└── Google Sheet Template.xlsx
```

## Required Configuration

Before importing the workflows, configure:

- Google Sheets OAuth2 credential
- Google Docs OAuth2 credential
- Google Drive OAuth2 credential
- Gmail OAuth2 credential
- Google Sheet ID
- Google Docs template ID
- Google Drive destination folder ID
- HR recipient email address
- Tally form URL or equivalent form frontend
- Production webhook URLs

The public workflow files use placeholders such as:

```text
YOUR_GOOGLE_SHEET_ID
YOUR_GOOGLE_DOC_TEMPLATE_ID
YOUR_GOOGLE_DRIVE_FOLDER_ID
REPLACE_WITH_GOOGLE_SHEETS_CREDENTIAL_ID
REPLACE_WITH_GOOGLE_DOCS_CREDENTIAL_ID
REPLACE_WITH_GOOGLE_DRIVE_CREDENTIAL_ID
REPLACE_WITH_GMAIL_CREDENTIAL_ID
hr@example.com
```

## Google Sheets Setup

Use `Google Sheet Template.xlsx` as the column-reference template. Upload or recreate it in Google Sheets, then place its spreadsheet ID in both workflows.

The sheet acts as the central candidate record and stores registration data, candidate IDs, completion status, document links, and processing timestamps.

## Google Docs Template

Upload `Candidate_Profile_Google_Doc_Template.docx` to Google Drive and convert it to Google Docs format. Use the resulting document ID as `YOUR_GOOGLE_DOC_TEMPLATE_ID`.

The profile-generation workflow copies this template and replaces its placeholders with candidate information before PDF export.

## Import and Setup

1. Import `Candidate Registration.json` into n8n.
2. Import `Candidate Profile Generation.json` into n8n.
3. Assign the required Google Sheets, Google Docs, Google Drive, and Gmail credentials.
4. Replace all placeholder IDs and email addresses.
5. Create or import the Google Sheets structure.
6. Upload and convert the candidate-profile template to Google Docs.
7. Configure the first form to call the registration webhook.
8. Configure the second form to call the profile-generation webhook.
9. Test a new candidate registration.
10. Test duplicate-email handling.
11. Test all three language routes.
12. Test document generation, PDF export, Drive storage, and HR delivery.
13. Activate both workflows only after successful testing.

## Security and Privacy

The repository does not include API keys, OAuth tokens, real credential IDs, private Google resource IDs, production webhook IDs, or real candidate records.

Because this workflow processes personal application data, production deployments should also use:

- restricted Google Drive and Google Sheets permissions
- a documented data-retention policy
- GDPR-compliant privacy information and consent
- secure webhook endpoints
- minimal data collection
- deletion and access-request procedures
- n8n execution-data retention limits

## Workflow Design Highlights

- Two-stage candidate intake
- Duplicate-email prevention
- Unique candidate identifiers
- Multilingual routing in German, English, and Spanish
- Central Google Sheets record
- Reusable Google Docs template
- Automated PDF generation
- Candidate and HR notifications
- Completion-state validation
- Separation of candidate registration and profile processing

## Possible Improvements

- Add automatic CV text extraction and AI-assisted candidate summaries
- Add recruiter approval stages
- Add interview scheduling through Google Calendar
- Add application-status notifications
- Add workflow-level error alerts
- Add data-retention and deletion automation
- Add dashboard reporting for candidate pipeline metrics

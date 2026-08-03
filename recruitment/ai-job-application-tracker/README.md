# AI Job Application Tracker

An n8n workflow that monitors a Dropbox folder for job-application documents, extracts application information from PDF files with OpenAI, checks for previous applications in Google Sheets, and sends a Telegram notification for new or duplicate applications.

## Business Problem

Job seekers often save cover letters and application documents in folders but still need to manually maintain a separate application tracker. This workflow turns the Dropbox folder into an automated application log and helps prevent duplicate applications to the same company and position.

## Workflow Summary

1. Checks the Dropbox `Incoming` folder on a schedule.
2. Filters for PDF and DOCX files.
3. Processes files sequentially with `Loop Over Items`.
4. Downloads each file from Dropbox.
5. Routes files by extension.
6. Extracts text from PDF documents.
7. Cleans and validates the extracted text.
8. Uses OpenAI structured extraction to identify:
   - Company
   - Position
9. Creates a normalized application key.
10. Checks Google Sheets for an existing company-position combination.
11. Adds new applications to Google Sheets.
12. Sends Telegram notifications for:
   - New applications
   - Already-applied duplicates
13. Continues until every file in the batch has been processed.

## Architecture

```text
Schedule Trigger
  → Dropbox: List Incoming Files
  → Filter: PDF/DOCX
  → Loop Over Items (batch size 1)
  → Dropbox: Download File
  → Switch: Detect File Type
      ├─ PDF
      │   → Extract PDF Text
      │   → Normalize and Validate
      │   → OpenAI Information Extractor
      │   → Prepare Application Record
      │   → Validate Company and Position
      │   → Google Sheets Lookup
      │   → Already Applied?
      │       ├─ Yes → Telegram Duplicate Warning
      │       └─ No  → Append Google Sheets Row
      │                → Telegram Success
      │   → Return to Loop
      └─ DOCX
          → Return to Loop (DOCX extraction planned)
```

## Google Sheets Structure

Create a sheet named `Applications` with these columns:

```text
ApplicationKey
AppliedDate
Company
Position
Location
JobURL
ApplicationStatus
SourceFileName
DropboxFileId
DropboxPath
FileType
Confidence
ProcessedAt
```

## Dropbox Structure

```text
Job Applications/
├── Incoming/
├── Processed/
├── Manual Review/
└── Failed/
```

The current workflow reads from `Incoming`. Moving files into the other folders is a planned improvement.

## Required Credentials

Configure these credentials directly in n8n after importing:

- Dropbox OAuth2
- Google Sheets OAuth2
- OpenAI API
- Telegram Bot API

## Required Configuration

After importing the workflow:

1. Select the Dropbox credential.
2. Set the Dropbox folder path.
3. Select the Google Sheets credential.
4. Replace `REPLACE_WITH_GOOGLE_SHEET_ID`.
5. Confirm the sheet name is `Applications`.
6. Select the OpenAI credential and model.
7. Replace `REPLACE_WITH_TELEGRAM_CHAT_ID`.
8. Test with one PDF before activating the schedule.

## Duplicate Detection

The workflow checks Google Sheets using both:

```text
Company AND Position
```

It also generates a normalized key:

```text
normalized-company__normalized-position
```

This supports consistent application tracking while allowing the same company to have multiple job applications for different positions.

## Reliability Design

- Numbered and descriptive node names
- One-file-at-a-time processing
- Explicit PDF/DOCX routing
- Extracted-text validation
- Structured AI output
- Deterministic key generation
- Duplicate prevention
- Telegram result notifications
- Loop return paths for success, duplicate, invalid, and unsupported-document branches
- Credentials and private resource identifiers removed from the public workflow JSON

## Current Limitation

The built-in `Extract From File` node in the tested n8n version supports PDF extraction but not DOCX extraction. The DOCX branch currently skips the file and continues processing the remaining batch.

A production extension can add DOCX extraction using one of these approaches:

- LibreOffice conversion in the self-hosted n8n container
- A dedicated document-conversion API
- A custom Code/Execute Command integration
- Microsoft Graph or Google Drive conversion

## Planned Improvements

- DOCX extraction
- Move successful files to `Processed`
- Move incomplete documents to `Manual Review`
- Move failed files to `Failed`
- Extract application date, location, job URL, contact details, and salary expectation
- Add execution logging
- Add a separate n8n Error Trigger workflow
- Send a single batch summary after all files finish
- Check Dropbox file ID and revision before downloading to avoid repeated scheduled processing

## Import

Import:

```text
workflow/ai-job-application-tracker.json
```

Then configure all credentials and placeholders before executing.

## Security

The public workflow contains no API keys, OAuth tokens, Telegram chat IDs, Google Sheet IDs, webhook IDs, or n8n instance identifiers.

Do not commit exported workflow JSON without sanitizing credentials and private resource identifiers.

## Author

**Md Mamunuzzaman**  
AI Automation & Full-Stack Developer  
Bremen, Germany

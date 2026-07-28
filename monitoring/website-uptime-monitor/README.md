# Website Uptime Monitor

An automated website monitoring workflow built with n8n.

The workflow checks a website at a configured interval, records every check in Google Sheets, maintains the latest website status, detects status changes, and sends a Telegram alert when the website changes from UP to DOWN.

## Business Problem

Businesses need to know quickly when an important website or API becomes unavailable. Manual checking is unreliable and does not provide historical monitoring data.

## Workflow Features

- Scheduled website availability checks
- Configurable HTTP timeout
- Automatic retries
- UP and DOWN result normalisation
- Response-time measurement
- Google Sheets logging
- Latest-status tracking
- Status-change detection
- Telegram downtime notification
- Prevention of repeated alerts while the website remains down

## Technologies

- n8n
- HTTP Request
- Google Sheets
- Telegram Bot API
- JavaScript Code nodes

## Workflow Process

1. The Schedule Trigger runs the workflow.
2. Website configuration and timestamps are prepared.
3. An HTTP request checks the website.
4. Successful and failed responses are normalised.
5. Every result is appended to the Checks sheet.
6. The previous status is read from the Latest Status sheet.
7. The current and previous statuses are compared.
8. The Latest Status record is updated.
9. A Telegram alert is sent only when the status changes to DOWN.

## Required Configuration

Replace the following placeholders:

- `YOUR_GOOGLE_SHEET_ID`
- `YOUR_TELEGRAM_CHAT_ID`
- Website URL
- Google Sheets credential
- Telegram credential

## Google Sheets Structure

### Checks sheet

| Column | Description |
|---|---|
| checkedAt | Monitoring timestamp |
| websiteUrl | Monitored website |
| status | UP or DOWN |
| statusCode | HTTP response code |
| responseTimeMs | Response time |
| errorMessage | Normalised response or error |

### Latest Status sheet

| Column | Description |
|---|---|
| websiteUrl | Unique website identifier |
| currentStatus | Latest status |
| lastCheckedAt | Latest check time |
| statusCode | Latest HTTP status code |

## Error Handling

- HTTP timeout
- Automatic retry
- Continue through the error output
- Normalised HTTP and connection errors
- Alerts only on state transition
- Historical logging for troubleshooting

## Import

1. Download `workflow.json`.
2. Import it into n8n.
3. Configure Google Sheets credentials.
4. Configure Telegram credentials.
5. Set the Google Sheet ID and Chat ID.
6. Test with an invalid URL.
7. Activate the workflow.

## Possible Improvements

- Recovery notification when the website returns online
- Multiple website configuration
- Alert throttling
- Email and Slack notifications
- Daily uptime reporting
- Monthly archive workflow
- Response-time dashboard

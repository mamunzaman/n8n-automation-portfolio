# n8n Automation Portfolio

A collection of production-oriented business automation workflows built with n8n.

These projects demonstrate workflow architecture, API integration, data validation, error handling, logging, AI-assisted processing, document generation, notification systems, and Google Workspace automation.

## Featured Automations

### AI Job Search & Candidate Matching Automation

A scheduled recruitment workflow that collects job listings from LinkedIn and StepStone through Apify, normalises and deduplicates the data, removes previously processed jobs, and evaluates relevant positions against a structured candidate profile using OpenAI.

Deterministic JavaScript logic handles filtering, validation, scoring adjustments, ranking, and Top-15 selection. The final results are stored in Google Sheets and delivered as a Telegram summary.

[View the AI Job Search & Candidate Matching Automation](recruitment/ai-job-search-matching/)

### Website Uptime Monitor

A monitoring workflow that checks website availability on a schedule, records response status and response time in Google Sheets, tracks the latest state, and sends a Telegram alert when a website changes from UP to DOWN.

[View the Website Uptime Monitor](monitoring/website-uptime-monitor/)

## Workflow Categories

### Recruitment & AI Matching

- [AI Job Search & Candidate Matching Automation](recruitment/ai-job-search-matching/)
- Multi-source job collection with Apify
- AI-based candidate-to-job evaluation
- Deterministic validation, ranking, and Top-N selection
- Google Sheets result storage and Telegram reporting

### Monitoring

- [Website Uptime Monitor](monitoring/website-uptime-monitor/)
- Scheduled HTTP checks
- Status-change detection
- Historical logging and Telegram alerts

### Document Automation

- Candidate PDF generation
- Google Docs template generation
- Google Drive file storage

### Image Processing

- Coin image upload and file organisation
- Duplicate file replacement
- Google Drive storage

### Email Automation

- Multilingual email routing
- Candidate confirmation emails
- Status-based email notifications

## Technologies

- n8n
- JavaScript
- OpenAI API
- Apify
- REST APIs
- Webhooks
- JSON
- Google Sheets
- Google Docs
- Google Drive
- Gmail
- Telegram Bot API
- Tally Forms

## Engineering Approach

The workflows are designed with:

- Clear and numbered node naming
- Modular workflow architecture
- Separation of deterministic logic from AI processing
- Input validation and output normalisation
- Duplicate prevention
- Structured LLM outputs
- Score validation and rule-based adjustments
- Error handling and logging
- Reusable configuration values
- Minimal duplicated logic
- Secure credential handling
- Documented setup requirements

## Security

Credentials, API keys, access tokens, private Google Sheet IDs, Telegram chat IDs, and other secrets are not included in this repository.

Before importing a workflow, configure the required credentials directly inside n8n and replace all documented placeholder values.

## Importing a Workflow

1. Open the required project folder.
2. Download the workflow JSON file.
3. Import it into n8n.
4. Configure the required credentials.
5. Replace placeholder configuration values.
6. Review the project README for setup instructions.
7. Test the workflow manually before activation.

## Author

**Md Mamunuzzaman**  
AI Automation & Full-Stack Developer  
Bremen, Germany

# n8n Automation Portfolio

A collection of production-oriented business automation workflows built with n8n.

These projects demonstrate workflow architecture, API integration, data validation, error handling, logging, AI-assisted processing, document generation, notification systems, multilingual routing, and Google Workspace automation.

## Featured Automations

### Candidate Application Automation

A two-stage multilingual recruiting workflow that captures candidate interest, prevents duplicate registrations, creates unique candidate IDs, collects detailed application data, generates structured candidate profiles, exports them as PDFs, stores files in Google Drive, and sends candidate and HR notifications in German, English, or Spanish.

[View the Candidate Application Automation](recruitment/candidate-application-automation/)

### AI Job Search & Candidate Matching Automation

A scheduled recruitment workflow that collects job listings from LinkedIn and StepStone through Apify, normalises and deduplicates the data, removes previously processed jobs, and evaluates relevant positions against a structured candidate profile using OpenAI.

Deterministic JavaScript logic handles filtering, validation, scoring adjustments, ranking, and Top-15 selection. The final results are stored in Google Sheets and delivered as a Telegram summary.

[View the AI Job Search & Candidate Matching Automation](recruitment/ai-job-search-matching/)

### Website Uptime Monitor

A monitoring workflow that checks website availability on a schedule, records response status and response time in Google Sheets, tracks the latest state, and sends a Telegram alert when a website changes from UP to DOWN.

[View the Website Uptime Monitor](monitoring/website-uptime-monitor/)

## Workflow Categories

### Recruitment & Candidate Processing

- [Candidate Application Automation](recruitment/candidate-application-automation/)
- Two-stage candidate registration and profile completion
- Duplicate-email prevention and unique candidate IDs
- Multilingual candidate communication in German, English, and Spanish
- Google Docs profile generation and PDF export
- Google Drive storage and HR delivery
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

- Candidate profile generation
- Google Docs template processing
- Automated PDF export
- Google Drive file storage

### Email Automation

- Multilingual email routing
- Candidate confirmation emails
- Duplicate-registration notifications
- HR candidate-package delivery
- Status-based notifications

## Technologies

- n8n
- JavaScript
- OpenAI API
- Apify
- REST APIs
- Webhooks
- JSON
- Google Sheets
- Google Docs API
- Google Drive
- Gmail
- Telegram Bot API
- Tally Forms
- PDF generation

## Engineering Approach

The workflows are designed with:

- Clear and numbered node naming
- Modular workflow architecture
- Separation of deterministic logic from AI processing
- Input validation and output normalisation
- Duplicate prevention
- Structured LLM outputs
- Score validation and rule-based adjustments
- Multilingual routing
- Completion-state validation
- Error handling and logging
- Reusable configuration values
- Minimal duplicated logic
- Secure credential handling
- Documented setup requirements

## Security

Credentials, API keys, access tokens, private Google resource IDs, Telegram chat IDs, production webhook IDs, real candidate records, and other secrets are not included in this repository.

Before importing a workflow, configure the required credentials directly inside n8n and replace all documented placeholder values.

Workflows that process candidate data should also use restricted access permissions, GDPR-compliant privacy information, secure webhook endpoints, minimal data collection, and appropriate execution-data retention limits.

## Importing a Workflow

1. Open the required project folder.
2. Download the workflow JSON file or files.
3. Import them into n8n.
4. Configure the required credentials.
5. Replace placeholder configuration values.
6. Review the project README and included templates.
7. Test the workflow manually before activation.

## Author

**Md Mamunuzzaman**  
AI Automation & Full-Stack Developer  
Bremen, Germany

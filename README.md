AI Lead-to-Appointment Automation
I built this project to automate the journey from a new business enquiry to a booked consultation.
The system uses two n8n workflows. The first captures and qualifies incoming leads, stores them in a simple CRM and sends the right follow-up. The second takes over when a Calendly event is created or cancelled and manages the appointment lifecycle.
I wanted the project to solve a realistic sales/admin problem rather than just demonstrate individual n8n nodes.
What it does
Receives new leads through a webhook
Validates and normalises lead data
Uses OpenAI to classify leads as HIGH, NORMAL or LOW priority
Stores leads in Google Sheets as a lightweight CRM
Generates personalised email replies
Sends faster follow-up for high-value leads
Alerts the business owner about high-value leads
Sends qualified leads a Calendly booking link
Detects new bookings and cancellations
Updates CRM appointment status automatically
Notifies the business owner when an appointment is booked
Sends a reminder 24 hours before the consultation
Prevents reminders when an appointment has been cancelled
Sends a post-consultation thank-you email
Updates the CRM after the post-consultation follow-up
Workflow structure
1. Lead to Appointment Automation
`Webhook → Validation → AI Qualification → Lead Routing → CRM → Email / Follow-up`
The AI qualification step routes leads into HIGH, NORMAL and LOW branches. High and normal leads receive different follow-up timing, while low-priority leads are stored without starting the full sales sequence.
2. Appointment Booking Automation
`Calendly Trigger → Booking Router → CRM Update → Owner Alert / Reminder / Post-Consultation Follow-up`
Calendly acts as the bridge between the two workflows. Google Sheets is the shared CRM, and the lead's email address is used to match the appointment back to the correct CRM record.
Tech stack
n8n
OpenAI
Google Sheets
Gmail
Calendly
Webhooks
OAuth
Repository structure
```text
ai-lead-to-appointment-automation/
├── README.md
├── workflows/
│   ├── lead-to-appointment.json
│   └── appointment-booking.json
├── screenshots/
└── docs/
    └── workflow-overview.md
```
Import and setup
The workflow files in this repository are public-safe templates. Credentials and personal account details have intentionally been removed.
After importing the JSON files into n8n:
Connect your own OpenAI, Gmail, Google Sheets and Calendly credentials.
Select your Google Sheets CRM in each Google Sheets node.
Replace `owner@example.com` with the email address that should receive business-owner alerts.
Replace `https://calendly.com/YOUR_USERNAME/YOUR_EVENT` with your own Calendly event link.
Confirm the CRM columns match the fields expected by the workflow.
Test the workflows before activating them.
CRM columns
The example CRM uses:
`Date | Name | Email | Phone | Company | Service | Budget | Message | Source | Lead Quality | Status | Appointment Time`
Notes
This is a portfolio/demo project. The public workflow files do not contain API keys, OAuth tokens, personal email addresses or live credential connections.
For a production deployment I would also add stronger error handling, logging, retry behaviour and a more scalable CRM/database depending on the client's requirements.

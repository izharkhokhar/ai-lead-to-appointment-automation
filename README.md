# AI Lead-to-Appointment Automation

I built this project to automate the journey from a new business enquiry to a booked consultation.

The system uses two n8n workflows. The first captures and qualifies incoming leads, stores them in a simple CRM and sends the right follow-up. The second takes over when a Calendly event is created or cancelled and manages the appointment lifecycle.

I wanted the project to solve a realistic sales and admin problem rather than just demonstrate individual n8n nodes.

## What It Does

- Receives new leads through a webhook
- Validates and normalises lead data
- Uses OpenAI to classify leads as HIGH, NORMAL or LOW priority
- Stores leads in Google Sheets as a lightweight CRM
- Generates personalised email replies
- Sends faster follow-up for high-value leads
- Alerts the business owner about high-value leads
- Sends qualified leads a Calendly booking link
- Detects new bookings and cancellations
- Updates CRM appointment status automatically
- Notifies the business owner when an appointment is booked
- Sends a reminder 24 hours before the consultation
- Prevents reminders when an appointment has been cancelled
- Sends a post-consultation thank-you email
- Updates the CRM after follow-up

## Workflow 1 — Lead to Appointment

`Webhook → Validation → AI Qualification → Lead Routing → CRM → Email / Follow-up`

The AI qualification step routes leads into **HIGH**, **NORMAL** and **LOW** branches.

High and normal leads receive different follow-up timing, while low-priority leads are stored without starting the full sales sequence.

## Workflow 2 — Appointment Booking

`Calendly Trigger → Booking Router → CRM Update → Owner Alert / Reminder / Post-Consultation Follow-up`

Calendly connects the two workflows. Google Sheets acts as the shared CRM, and the customer's email address is used to match the appointment with the correct lead.

## Tech Stack

- n8n
- OpenAI
- Google Sheets
- Gmail
- Calendly
- Webhooks
- OAuth

## Repository Structure

```text
ai-lead-to-appointment-automation/
├── README.md
├── workflows/
│   ├── lead-to-appointment.json
│   └── appointment-booking.json
├── screenshots/
│   ├── lead-workflow.png
│   └── appointment-workflow.png
└── docs/
    └── workflow-overview.md

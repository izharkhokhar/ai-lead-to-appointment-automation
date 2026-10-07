# Workflow Overview

## How the two workflows connect

The workflows are separate by design.

The **Lead to Appointment Automation** receives the original enquiry, qualifies it, stores the lead in Google Sheets and sends the Calendly booking link.

When the lead books, **Calendly** triggers the **Appointment Booking Automation**. That workflow searches the same Google Sheets CRM using the lead's email address and updates the correct record.

So the connection is:

```text
Lead Workflow
   ↓
Google Sheets CRM
   ↓
Calendly booking link
   ↓
Calendly event
   ↓
Appointment Workflow
   ↓
Same Google Sheets CRM
```

## Lead workflow

### HIGH
- Save lead to CRM
- Generate a personalised reply
- Send consultation link
- Alert the business owner
- Wait 6 hours
- Check CRM status
- If still unbooked, send another follow-up and alert the owner

### NORMAL
- Save lead to CRM
- Generate a personalised reply
- Send consultation link
- Wait 24 hours
- Check CRM status
- If still unbooked, send a follow-up

### LOW
- Save the lead as low priority
- Do not start the full booking follow-up sequence

## Appointment workflow

### Appointment created
- Find the lead in the CRM
- Set status to `Appointment Booked`
- Save the appointment time
- Notify the business owner
- Start a reminder branch for 24 hours before the appointment
- Start a post-consultation branch for 1 hour after the scheduled end time

### Appointment cancelled
- Match the lead by email
- Set status to `Appointment Cancelled`

### Reminder protection
Before sending the reminder, the workflow checks the CRM again. If the appointment is no longer marked `Appointment Booked`, the reminder does not send.

### Post-consultation follow-up
One hour after the scheduled appointment end time, the workflow checks that the booking is still active, sends a thank-you email and updates the CRM status to `Consultation Follow-Up Sent`.

## Public template placeholders

The GitHub version intentionally uses placeholders for account-specific values:

- `owner@example.com`
- `YOUR_GOOGLE_SHEET_ID`
- `https://calendly.com/YOUR_USERNAME/YOUR_EVENT`

n8n credentials are also removed from the exported public templates.

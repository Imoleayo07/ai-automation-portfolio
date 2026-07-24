# Email & Lead Triage Workflows

A lightweight inbox automation that turns incoming inquiries into routed, actionable alerts instead of a pile of unread email.

## Tools

n8n, Gmail, Tally, Groq, Slack, Google Sheets

## How it works

1. Inquiries arrive through Gmail or a Tally webhook form.
2. Groq extracts the key details from each inquiry: service needed, urgency, and contact info.
3. The result is routed to Slack for immediate visibility, a confirmation email is sent back to the sender, and the inquiry is logged in Google Sheets.
4. Each inquiry gets a unique ID (generated from a timestamp plus a random suffix) so nothing gets double-booked or lost, even under high volume.

A related, simpler version of this workflow was also built for Light Consultancy directly: Gmail → AI classification → Google Drive → Telegram alert.

## Problems solved

- **Broken JSON from apostrophes:** customer messages containing apostrophes broke the JSON body until `JSON.stringify()` was applied consistently across nodes.
- **Cross-branch data references:** nodes referencing data across different branches of the workflow failed until references were standardized using `$json`.
- **Duplicate or colliding IDs:** inquiry IDs needed a genuinely unique format, solved with `$now.toMillis()` plus a random suffix.

## Status

Live and in use for lead intake.

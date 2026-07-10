# Squire Automation

This folder contains the **n8n** automation workflows used in the Squire project. These workflows automate task scheduling, calendar integration, and reminder notifications.

## Why does this automation exist?
The n8n automation exists to bridge the gap between the task management system and user notifications. Instead of manually creating calendar events and sending reminder emails, the system triggers webhooks that automatically handle these processes. This ensures reliability, saves time, and provides users with timely reminders before their deadlines.

## Workflows

### 1. Calendar Tasks & Reminders
**Files:** `Calendar Tasks.json`, `calendar-reminder-workflow.json`

This is the primary workflow for handling new tasks. It performs the following actions:
- **Webhook Trigger**: Listens for a POST request (`/add-task`) containing task details such as `taskName`, `deadline`, `email`, and `description`.
- **Validation & Parsing**: A custom code node validates the incoming data and calculates the exact time to send a reminder (e.g., 6 hours before the deadline).
- **Google Calendar Integration**: Automatically creates an event in the primary Google Calendar for the task.
- **Immediate Response**: Sends a JSON response back to the caller confirming that the task was scheduled successfully.
- **Wait Node**: Pauses the workflow execution until the scheduled reminder time.
- **Gmail Notification**: Sends an automated email reminder to the provided email address, alerting the user that their task is due soon.

### 2. Google Calendar (DEPI PROJECT)
**File:** `Google calendar workflow.json`

A streamlined workflow specifically designed for the DEPI project.
- **Webhook Trigger**: Listens for a payload containing `deadline_date`, `deadline_time`, and `topic`.
- **Google Calendar Integration**: Instantly creates a calendar event for a specific user based on the provided topic and deadline.

## Usage
To use these workflows in your own n8n instance:
1. Open your n8n dashboard.
2. Create a new workflow.
3. Click on the options menu (top right) and select **Import from File**.
4. Select the desired JSON file from this folder.
5. Reconfigure the **Credentials** for Google Calendar and Gmail to match your own accounts.
6. Activate the workflow.

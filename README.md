# Job Kanban

A personal job-search board: one `index.html`, no framework, no build step.

The repository holds only code. The data stays in my private Google Sheet, Drive and Gmail. The browser reads it directly after a Google sign-in. Without a sign-in the page shows nothing but a sign-in button.

- **Board / List:** jobs from the `jobs` sheet. Drag a card or use the status dropdown to change its status.
  - Statuses: new, applied, screen, interview, offer, rejected (email), rejected, no reply.
  - `rejected (email)` is a rejection without any conversation. `rejected` is a rejection after a screen or interview.
  - The **Hide closed** chip hides rejected (email), rejected and no reply.
- **Activity:** comments, cover letters and company replies with attachments, plus status history. These live in the `comments` and `activity` sheets. Attachments go to the Drive folder "Job kanban — attachments".
- **Mail (read-only):**
  - Each job has a Mail tab that finds Gmail messages by company name, or by the job's `mail_query` column, starting from the apply date.
  - The Inbox screen lists recent job mail, links each message to a job, and suggests a status change for rejections and invitations.
  - Accepting a suggestion changes the status and saves the email as a company reply.
  - Saved and dismissed messages are recorded in the `mail` sheet.

## Access

- The OAuth client lives in a Google Cloud project in Testing mode, so only its listed test users can sign in.
- Scopes:
  - `spreadsheets`
  - `drive.file` (only files this site created)
  - `gmail.readonly`
- The access token stays in this browser's localStorage and expires after an hour. The sheet link is also stored there and is never put in the repository.

## Deploy

`git push` to `main`. GitHub Pages serves the repository root.

For local testing, run `python3 -m http.server 8000` and open http://localhost:8000. That origin is also allowed in the OAuth client.

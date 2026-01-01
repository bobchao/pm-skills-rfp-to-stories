# User Story Template Library

This document provides User Story templates for various common features as writing references.

## Usage Instructions

1. These templates are **starting points**, not endpoints
2. Adjust wording and details based on actual RFP
3. Not all templates apply to every project
4. `[placeholders]` in templates need to be replaced with actual content

---

## Authentication and Authorization

### Login Related

```markdown
As a user, I want to log into the system via [authentication method] so that I can access my personalized content and settings.

As a user, I want the system to remember my login state for [time period] so that I don't need to log in frequently.

As a user, I want to securely log out of the system so that I can protect my account on shared computers.

As a security manager, I want the system to automatically log out users after [time] of inactivity to reduce the risk of account hijacking.
```

### Permission Related

```markdown
As a system administrator, I want to set user roles and permissions so that I can control different personnel's system access scope.

As a user, I want to receive notifications when my permissions change so that I know which features I can use.

As a manager, I want to view the permission list of my team members so that I can ensure permission configuration matches responsibilities.
```

---

## Content Management

### Creating Content

```markdown
As a [editor role], I want to create new [content type] so that I can provide users with the latest information.

As a [editor role], I want to upload images/attachments when creating [content type] so that I can enrich content presentation.

As a [editor role], I want to save [content type] as draft so that I can continue editing later without finishing at once.

As a [editor role], I want to preview how [content type] will look when published so that I can confirm layout is correct.
```

### Editing Content

```markdown
As a [editor role], I want to edit published [content type] so that I can correct errors or update information.

As a [editor role], I want to view edit history of [content type] so that I can track changes.

As a [editor role], I want to revert [content type] to a previous version so that I can quickly recover from mistakes.
```

### Approval Workflow

```markdown
As a [reviewer role], I want to view the list of pending [content type] so that I can focus on review work.

As a [reviewer role], I want to approve [content type] so that content can be officially published.

As a [reviewer role], I want to return [content type] with revision comments so that editors can adjust and resubmit.

As a [reviewer role], I want to reject [content type] with reasons so that editors understand why it wasn't approved.

As a [editor role], I want to receive notifications when my submitted [content type] status changes so that I can know review progress in time.
```

### Scheduled Publishing

```markdown
As a [editor role], I want to set scheduled publish time for [content type] so that I can prepare content to go live at specified times.

As a [editor role], I want to set takedown time for [content type] so that time-sensitive content is automatically removed.
```

---

## Search and Filtering

```markdown
As a user, I want to search [content type] by keywords so that I can quickly find relevant information.

As a user, I want to filter [content type] by [filter criteria] so that I can narrow down search scope.

As a user, I want search results sorted by [sort method] so that I can see the most relevant results first.

As a user, I want the system to remember my recent search criteria so that I can quickly repeat similar searches.
```

---

## Bookmarks and Following

```markdown
As a user, I want to bookmark [item type] so that I can quickly access it later.

As a user, I want to view all [item type] I've bookmarked so that I can manage content I'm following in one place.

As a user, I want to remove bookmarks from [item type] so that I can keep my bookmark list tidy.

As a user, I want the system to confirm my intention when removing bookmarks so that I can avoid accidental deletion.

As a user, I want to receive notifications when bookmarked [item type] is updated so that I can get the latest information in time.
```

---

## Notifications and Reminders

```markdown
As a user, I want to set which notification types I want to receive so that I only get messages I care about.

As a user, I want to choose how to receive notifications (in-app/email/push) so that I can receive them in the most convenient way.

As a user, I want to view all notification history so that I can review messages I might have missed.

As a user, I want to mark all notifications as read in one click so that I can quickly clear the notification list.
```

---

## Data Export and Reports

```markdown
As a [role], I want to export [data type] as [format] so that I can analyze or archive in other tools.

As a [role], I want to view [report type] reports so that I can understand [business metric].

As a [role], I want to set time range for reports so that I can analyze data for specific periods.

As a [role], I want to automatically receive [report type] reports periodically so that I don't need to query manually.
```

---

## User Experience

### Responsive Design

```markdown
As a user, I want to use the system normally on different devices (desktop/tablet/mobile) so that I can access anytime, anywhere.

As a user, I want to use main features on mobile so that I can handle urgent matters on the go.
```

### Navigation and Interface

```markdown
As a user, I want to find needed features through clear menu structure so that I can complete work quickly.

As a user, I want to return to top in one click when browsing long pages so that I can save scrolling time.

As a user, I want to see my current location (breadcrumb navigation) so that I know where I am in the system.

As a user, I want to quickly switch between different functional areas so that I can improve operational efficiency.
```

### Feedback Mechanism

```markdown
As a user, I want to see clear success/failure prompts after operations so that I can confirm operation results.

As a user, I want to see progress indicators when waiting for longer operations so that I know the system is processing.

As a user, I want error messages to explain the cause and solution so that I can troubleshoot on my own.
```

---

## System Administration

```markdown
As a system administrator, I want to view system operation status so that I can detect anomalies in time.

As a system administrator, I want to view user operation logs so that I can track issues or conduct audits.

As a system administrator, I want to configure system parameters (like idle logout time) so that I can adjust behavior according to policies.

As a system administrator, I want to temporarily disable specific features so that I can control the system during maintenance or emergencies.
```

---

## Integration and API

```markdown
As a user, I want to log into the system via company SSO so that I don't need to remember additional account passwords.

As a user, I want to not need to log in again when clicking links to other internal platforms from the system so that I can have a seamless experience.

As a [role], I want the system to sync data with [third-party system] so that I can maintain information consistency.

As a developer, I want to access [data type] via API so that I can integrate into other systems.
```

---

## Performance Related (Non-functional Requirements as Stories)

```markdown
As a user, I want pages to load within [X] seconds so that I can have a smooth user experience.

As a user, I want the system to operate normally during peak hours so that my work is not affected.

As a user, I want to see progress when uploading large files so that I know how much longer to wait.
```

---

## Template Usage Notes

### 1. Avoid Mechanical Application

Templates are references, not fill-in-the-blank exercises. Each project has its unique context, requiring wording adjustments.

### 2. Remove Inapplicable Items

Not all features need all related Stories. For example:
- Pure browsing websites don't need "bookmark" feature
- Internal systems may not need "responsive design"

### 3. Merge Too-Small Stories

If multiple template Stories are all very small and highly related, consider merging.

### 4. Add Project-Specific Items

Templates cannot cover all business scenarios, need to add project-specific Stories based on RFP.

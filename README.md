# 🏃 AgileLedger

[![inGitDB](https://github.com/ingitdb/demo-agile-ingitdb/actions/workflows/ingitdb.yml/badge.svg)](https://github.com/ingitdb/demo-agile-ingitdb/actions/workflows/ingitdb.yml)

> **Note**: This schema describes and relies on features of **inGitDB** that may not be fully implemented
> yet. Its primary purpose is to drive development of inGitDB by serving as a comprehensive real-world use
> case and to demonstrate its capabilities for agile team workflows.

AgileLedger is an open-source, **free to use** template app for agile teams that uses **inGitDB** as its
main database, hosted directly in a Git repository. It is designed to facilitate agile rituals,
specifically **Daily Standups** and **Retrospectives**, through a statically hosted GitHub Pages web UI
without needing a traditional backend.

With AgileLedger, **users and teams completely own and control their data**. Storage and privacy are
managed entirely through standard GitHub permissions.

## Overview

AgileLedger provides a completely serverless structure leveraging GitHub and inGitDB. By forking the
AgileLedger template repo, a team immediately gets a pre-configured inGitDB setup.

- **Frontend**: A statically hosted Single Page Application (SPA), implemented in **Ionic / Angular**.
- **Backend/Data Layer**: GitHub API + inGitDB CLI (run via GitHub Actions). Data is stored as JSON/YAML files in the repo.
- **Data Flow**: When a user submits an update, the web UI uses the GitHub API to create a personal branch, add/modify the relevant files, and open a Pull Request (PR).
- **Automation**: inGitDB CLI runs via GitHub Actions to automatically validate both the schema and the data via incremental checks. Once validated, the PR is automatically merged into the main branch, triggering a process to update the materialized views that power summary pages.

## ⚙️ GitHub Actions Workflow

A [GitHub Actions workflow](.github/workflows/ingitdb.yml) runs automatically on every push and pull request to `main`. It uses the [ingitdb-action](https://github.com/ingitdb/ingitdb-action) to:

1. **Validate** — checks all collection schema definitions and verifies every record conforms to its collection's constraints (types, required fields, foreign keys, enums, regex patterns).
2. **Materialize** — builds any defined views, resolving cross-collection references and producing materialized output.

## 📋 Collections Overview

| Collection | Description |
|------------|-------------|
| [teams](collections/teams/) | Agile teams — the root of all data |
| [teams/mates](collections/teams/) | Team members and their roles |
| [teams/daily-questions](collections/teams/) | Customizable daily standup questions per team |
| [teams/dates](collections/teams/) | Standup dates for each team |
| [teams/dates/mates](collections/teams/) | Team member participation per date |
| [teams/dates/mates/questions](collections/teams/) | Question entries per mate per date |
| [teams/dates/mates/questions/answers](collections/teams/) | Answers per question per mate per date |

For full details on each collection see [collections/](collections/).

## Architecture & Permissions

1. **GitHub Repository Store**: Branches hold pending changes; `main` holds the source of truth.
2. **inGitDB Engine**: Validates data schemas and data integrity using incremental checks on PR validation. It then generates materialized views for quick reads.
3. **AgileLedger Web UI**: Statically deployed SPA using Ionic/Angular. It authenticates users via GitHub OAuth.
4. **Teams & Roles**:
   - A single repository can host **multiple teams**.
   - You can specifically define team members and their roles.
   - **Only team members** are authorized to submit data to a team's ledger.
5. **Privacy & Granular Permissions**:
   - Base privacy is managed through standard GitHub repository permissions.

## Core Features

### ⚡️ Triggers & Automation

- **Proactive Reminders**: `inGitDB` triggers can be set up to automatically remind team members to submit their answers prior to a scheduled standup or retrospective.
- **Real-Time Notifications**: Triggers can be utilized to send webhook notifications (e.g., via a Telegram bot, Slack, etc.) for various events.

### 📅 Daily Standups (Scrum)

Daily standups allow team members to submit updates on their progress for a specific date, configured via customized mandatory and optional questions. It stores answers in collections powered by inGitDB validations, and automatically merges changes through personal PRs.

### 🔄 Retrospectives

Retrospectives help agile teams reflect on past sprints by enabling custom review workflows. Users can pull data directly from their daily standups and convert them into top achievements, tracking team performance metrics aggregated by inGitDB.

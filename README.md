# Good Morning Breach

A morning cybersecurity news feed. Good Morning Breach gathers security news from open sources, sorts and scores each story, and sends subscribers a daily briefing. Logged-in users can also browse everything on a dashboard.

> **Status:** Early planning. The scope below comes from the initial requirements interview.

## Goals

- Give a short, useful picture of the overnight threat landscape every morning.
- Use only ethical data sources, and honor each source's licensing and terms of use.
- Link stories to MITRE ATT&CK so readers can see the tactics and techniques involved.

## Data Sources

| Source | Notes |
| --- | --- |
| Reddit | Security subreddits (e.g. r/netsec, r/cybersecurity), via the official API and within its terms |
| [Cloudflare Radar](https://radar.cloudflare.com/zero-wire) | Internet traffic, attack, and outage signals |
| Open-source cyber news | RSS feeds and advisories (e.g. CISA KEV, vendor advisories, security news outlets) |
| MITRE ATT&CK | Maps stories to tactics and techniques |

### Ethical sourcing

- Before adding a source, check its license, terms of service, and robots.txt.
- Use official APIs and feeds instead of scraping wherever possible.
- Store summaries and links, not full copies of copyrighted articles, and always credit the source.
- Keep a record of each source's license or terms.

## Features

### Morning Alert
The daily briefing goes out on each subscriber's chosen channels:
- **Email**
- **Text (SMS)**
- **Slack**

### Dashboard
A web view of the current feed, with filters by category, risk level, source, and date.

### Story Categorization
Each story is sorted into categories such as vulnerability, ransomware, data breach, nation-state activity, malware, and policy/regulation.

### Sentiment / Risk Analysis
Each story is scored for risk and severity, so the briefing and dashboard can list the most important items first.

### MITRE ATT&CK Analysis
Where possible, each story is tagged with the ATT&CK tactics and techniques it describes.

## Access Control

This is a closed service, and every page needs a login.

| Role | Capabilities |
| --- | --- |
| **admin** | Manage users, data sources, categories, and alert settings |
| **user** | View the dashboard and manage their own alert subscriptions |

## Roadmap

- [ ] Choose the tech stack and architecture
- [ ] Build source ingestion, including license tracking
- [ ] Add categorization and risk scoring
- [ ] Add MITRE ATT&CK mapping
- [ ] Build authentication and roles (admin/user)
- [ ] Build the dashboard
- [ ] Add alert delivery (email, SMS, Slack)

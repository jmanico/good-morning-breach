<p align="center"><img src="logo.svg" width="96" height="96" alt="Good Morning Breach logo: a dawn sun over a broken horizon"></p>

# Good Morning Breach

A private, non-commercial morning cybersecurity news feed. Good Morning Breach collects security news from licensed open sources, categorizes and scores each story, tags it with MITRE ATT&CK techniques, and sends each user a morning alert. Logged-in users can also browse all stories on a dashboard.

> **Status:** Requirements and design complete. See [REQUIREMENTS.md](REQUIREMENTS.md) for the full, numbered requirements and [DESIGN.md](DESIGN.md) for the design system. This README is a summary; if the two disagree, REQUIREMENTS.md wins.

## Goals

- Give a short, useful picture of the overnight threat landscape every morning.
- Use only ethical data sources, and honor each source's license and terms of use.
- Link stories to MITRE ATT&CK so readers can see the tactics and techniques involved.
- Stay private and non-commercial, for personal use only.

## Data Sources

Source licenses were researched for this use case. See [reports/Licensed cyber news sources.md](reports/Licensed%20cyber%20news%20sources.md).

| Group | Sources at launch |
| --- | --- |
| Government and CERT | CISA KEV and advisories, NVD API, FBI IC3, UK NCSC, CERT-EU, CERT-FR, Australia ASD's ACSC, Canadian Centre for Cyber Security |
| Vulnerability and threat data | FIRST EPSS, GitHub Advisory Database, CISA Vulnrichment, abuse.ch (Feodo Tracker, SSL Blacklist, URLhaus, ThreatFox, MalwareBazaar), Have I Been Pwned breach catalog |
| News and research | SANS Internet Storm Center, EFF Deeplinks, Kaspersky Securelist, Hacker News (titles and links only) |
| Internet signals | Cloudflare Radar (outages, attack trends, BGP events), Cloudflare Zero Wire (headline, link, CVE IDs, action label only) |
| Frameworks | MITRE ATT&CK |
| Reddit | r/netsec and r/cybersecurity, **only after Reddit approves API access**; titles and links shown without change, never summarized or scored |

**Not used:** LevelBlue/AlienVault OTX, GreyNoise free tier, OpenPhish free feed, Spamhaus DROP, Shadowserver. Their terms forbid display to other persons.

### Ethical sourcing

- An admin records each source's license, terms link, and permitted use before the source can be enabled.
- Each source has a content rule: full text, verbatim excerpt, summary, or headline and link only. "All rights reserved" news sources get headline and link only.
- Every story shows its source name and a link to the original.
- Required notices (NVD, MITRE ATT&CK, Have I Been Pwned, SANS ISC) are shown. No government logos or seals, and no claim of endorsement.
- If the service ever becomes commercial, non-commercial-only sources must be disabled or licensed.

## Features

### Morning Alert
- Default: 07:00 in each user's time zone, every day. Each user can change the time, time zone, and days, or stop the alert.
- Channels, chosen per user: **Email**, **Text (SMS)**, **Slack** (user-supplied incoming webhook).
- Contains stories collected since the last alert at or above the user's minimum risk level (default Medium), highest risk first.
- Email and Slack: up to 10 stories. SMS: up to 3 titles and a dashboard link.
- Phone numbers are verified by code. Slack webhooks get a test message. Failed deliveries are retried up to 3 times.

### Dashboard
- Shows the last 24 hours by default, sorted by risk.
- Filters by category, risk, source, date range, and ATT&CK tactic or technique; keyword search.
- Shows current Cloudflare Radar data.
- Admins see the status of each source and a warning when a source fails for 24 hours.

### Story Categorization
One or more categories per story. Starting list: Vulnerability, Exploited Vulnerability, Ransomware, Malware, Data Breach, Phishing and Social Engineering, Nation-State Activity, Supply Chain, Cloud and Infrastructure, Internet Outage and DDoS, Policy and Regulation, Other. Admins can add, rename, and disable categories.

### Sentiment and Risk Analysis
- Risk: Critical, High, Medium, Low, Informational.
- Sentiment (tone of the story): Negative, Neutral, Positive.

### MITRE ATT&CK Analysis
Each story is tagged with zero or more ATT&CK techniques (ID, name, tactic), each linked to its page on the ATT&CK website.

### Data Retention
Stories are kept for 365 days. Alert delivery records are kept for 90 days.

## Design

The full design system is in [DESIGN.md](DESIGN.md). A static preview of the palette, type scale, components, and dashboard is in [design/preview.html](design/preview.html). Open the preview file locally in a browser.

- **Look:** a pre-dawn palette, with night-indigo ink on a pale first-light background. The dawn amber appears only in the logo.
- **Risk at a glance:** each story has a left risk spine. It gets thicker and darker as risk rises, from 8 px for Critical to 2 px for Informational. Risk always shows as a word, a colour, and a spine width together.
- **Type:** Atkinson Hyperlegible Next, self-hosted. Atkinson Hyperlegible Mono is used only for CVE and ATT&CK IDs.
- **Accessibility:** every colour pair meets WCAG 2.2 AA. Controls show a visible focus ring and have touch targets of at least 44 px.
- **Security in the UI:**
  - Signed-in state is always visible.
  - Destructive actions need confirmation. Deleting an account means typing its email.
  - Sign-in has one generic error, including for a locked account.
  - Collected content is shown as plain text only.
- **Logo:** [logo.svg](logo.svg) is a dawn sun over a broken horizon, split by a breach crack.

## Access Control

This is a closed service. Every page needs a login, and there is no self sign-up.

- Login: email address, password (at least 12 characters, not on a breached-password list), and a TOTP one-time code, set up at first login.
- An account is blocked for 15 minutes after 5 failed logins in 15 minutes. Sessions end after 30 minutes of inactivity.

| Role | Capabilities |
| --- | --- |
| **admin** | Everything a user can do, plus manage users, roles, data sources, and categories, and view source status and the admin action log |
| **user** | View the dashboard and manage their own alert settings and profile |

## Roadmap

- [x] Write requirements ([REQUIREMENTS.md](REQUIREMENTS.md))
- [x] Research source licenses
- [x] Design system, logo, and preview ([DESIGN.md](DESIGN.md))
- [ ] Choose the tech stack and architecture
- [ ] Build source ingestion, including license records and content rules
- [ ] Add categorization and risk scoring
- [ ] Add MITRE ATT&CK mapping
- [ ] Build authentication and roles (admin/user)
- [ ] Build the dashboard
- [ ] Add alert delivery (email, SMS, Slack)
- [ ] Apply for Reddit API access

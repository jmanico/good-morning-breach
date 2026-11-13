# Requirements: Good Morning Breach

This file owns WHAT the system must do. It does not say HOW to build it.

Sources: the project notes and the requirements interview. In the interview, the owner told the author to answer all open questions. Decisions made on that instruction are marked *(delegated decision)*.

## Required Requirement Inputs

- **Project purpose:** A morning cybersecurity news feed for private, non-commercial, personal use.
- **Users and actors:** Admin; User. External actors: data sources (see FR-1.14); email, text message, and Slack delivery services.
- **Core workflows:** Collect news from data sources; categorize stories; analyze sentiment and risk; tag stories with MITRE ATT&CK techniques; send the morning alert; show stories on a dashboard; log in; manage users; manage data sources; manage alert settings.
- **Data entities:** Story; data source (with license record); category; risk level; sentiment value; ATT&CK technique tag; morning alert; alert delivery record; user account; role; alert settings.
- **External integrations:** Reddit (r/netsec, r/cybersecurity); Cloudflare Radar; other open-source cyber news sources; MITRE ATT&CK; email; text message (SMS); Slack.
- **Authentication and roles:** Closed service. Every function needs login. Email address, password, and multi-factor authentication. Roles: admin, user. No self sign-up.
- **Regulatory or privacy constraints:** Use only ethical data sources and honor their licensing. The service is private and non-commercial, for personal use only. Contact data (email, phone number, Slack webhook) is used only to send alerts.
- **Target surfaces (web UI, APIs, background jobs):** Web dashboard; background jobs for collection, analysis, and the morning alert. Public APIs: none.

## Functional Requirements

### 1. Data Collection

- **FR-1.1** The system MUST collect cybersecurity news from Reddit, under the limits in FR-1.16, FR-1.17, and FR-1.18.
- **FR-1.7** The system MUST collect posts from the Reddit communities r/netsec and r/cybersecurity, under the limits in FR-1.16, FR-1.17, and FR-1.18.
- **FR-1.2** The system MUST collect data from Cloudflare Radar, including the Zero Wire vulnerability feed at https://radar.cloudflare.com/zero-wire.
- **FR-1.3** The system MUST collect cybersecurity news from other open-source news sources.
- **FR-1.4** The system MUST use MITRE ATT&CK data to analyze stories.
- **FR-1.5** The system MUST honor the license and the terms of use of each data source.
- **FR-1.6** The system MUST NOT collect data from a source whose license or terms of use do not permit that use.
- **FR-1.8** The system MUST collect from each enabled source at least one time each hour. If the terms of a source set a lower rate, the system MUST obey the terms of that source. *(delegated decision)*
- **FR-1.9** The system MUST attempt a collection from all enabled sources before it sends the morning alert. *(delegated decision)*
- **FR-1.10** When a source is not available or returns data that is not valid, the system MUST continue to collect from the other sources. *(delegated decision)*
- **FR-1.11** When a collection from a source fails, the system MUST record the time and the cause of the failure. *(delegated decision)*
- **FR-1.12** When two collected items have the same link, the system MUST keep them as one story. The story MUST show all sources that reported it. *(delegated decision)*
- **FR-1.13** The system SHOULD show stories that name the same CVE identifier as related stories. *(delegated decision)*
- **FR-1.14** At launch, the system MUST collect from these sources (see `reports/Licensed cyber news sources.md` for feed addresses, licenses, and limits): CISA KEV catalog and CISA advisory feeds; NVD API; FBI IC3; UK NCSC; CERT-EU; CERT-FR; Australia ASD's ACSC; Canadian Centre for Cyber Security; FIRST EPSS; GitHub Advisory Database; CISA Vulnrichment; abuse.ch Feodo Tracker, SSL Blacklist, URLhaus, ThreatFox, and MalwareBazaar; Have I Been Pwned breach catalog; SANS Internet Storm Center; EFF Deeplinks; Kaspersky Securelist; Hacker News (titles and links only); Cloudflare Radar; Cloudflare Zero Wire. *(delegated decision, from research)*
- **FR-1.15** The system MUST NOT collect from sources whose terms prohibit display to other persons: LevelBlue/AlienVault OTX, GreyNoise free tier, OpenPhish free feed, Spamhaus DROP, and Shadowserver. *(delegated decision, from research)*
- **FR-1.16** The system MUST NOT collect from Reddit until Reddit approves API access for this service. *(delegated decision, from research)*
- **FR-1.17** For Reddit items, the system MUST show only the post title, the subreddit, and a link, without change. The system MUST NOT summarize, categorize, or score the text of a Reddit post. The system MAY analyze the item that the post links to, if the license of that item permits it. *(delegated decision, from research)*
- **FR-1.18** When Reddit removes a post, or the author deletes or edits it, the system MUST delete or update its copy within 48 hours. *(delegated decision, from research)*
- **FR-1.19** From Cloudflare Radar, the system MUST collect internet outages, attack trends, and BGP hijack and route leak events. *(delegated decision)*
- **FR-1.20** From Cloudflare Zero Wire, the system MUST show only the headline, the link, the CVE identifiers, and the Zero Wire action label (Patch, Review, or Assess). *(delegated decision, from research)*
- **FR-1.21** An admin MAY add an "all rights reserved" news source. For such a source, the system MUST show only the headline, the source name, and a link. It MUST NOT store or show the article text or a summary of it. *(delegated decision, from research)*

### 2. Story Categorization

- **FR-2.1** The system MUST assign a category to each story. Exception: Reddit items (FR-1.17).
- **FR-2.2** The system MUST assign one or more categories to each story. *(delegated decision)*
- **FR-2.3** The system MUST start with these categories: Vulnerability; Exploited Vulnerability; Ransomware; Malware; Data Breach; Phishing and Social Engineering; Nation-State Activity; Supply Chain; Cloud and Infrastructure; Internet Outage and DDoS; Policy and Regulation; Other. *(delegated decision)*
- **FR-2.4** When no other category applies, the system MUST assign the category "Other". *(delegated decision)*
- **FR-2.5** An admin MUST be able to add, rename, and disable a category. *(delegated decision)*
- **FR-2.6** The system MUST NOT assign a disabled category to a new story. *(delegated decision)*

### 3. Sentiment and Risk Analysis

- **FR-3.1** The system MUST assign a sentiment value to each story. Exception: Reddit items (FR-1.17).
- **FR-3.2** The system MUST assign a risk value to each story. Exception: Reddit items (FR-1.17).
- **FR-3.3** The risk value MUST be one of: Critical, High, Medium, Low, Informational. *(delegated decision)*
- **FR-3.4** The sentiment value MUST be one of: Negative, Neutral, Positive. The value tells the tone of the story. *(delegated decision)*
- **FR-3.5** The system MUST show the risk value and the sentiment value with each story on the dashboard and in the email alert. *(delegated decision)*

### 4. Morning Alert

- **FR-4.1** The system MUST send a morning alert to users.
- **FR-4.2** The system MUST be able to send the morning alert by email.
- **FR-4.3** The system MUST be able to send the morning alert by text message.
- **FR-4.4** The system MUST be able to send the morning alert by Slack.
- **FR-4.5** The system MUST send the morning alert at 07:00 in the time zone of the user, every day, by default. *(delegated decision)*
- **FR-4.6** A user MUST be able to change the alert time, the time zone, and the days of the week for their own alert. *(delegated decision)*
- **FR-4.7** A user MUST be able to select one or more alert channels (email, text message, Slack) for their own alert. *(delegated decision)*
- **FR-4.8** A user MUST be able to stop and start their own alert. *(delegated decision)*
- **FR-4.9** A user MUST be able to set a minimum risk level for their own alert. The default MUST be Medium. *(delegated decision)*
- **FR-4.10** The alert MUST contain only stories that the system collected after the previous alert to that user and that are at or above the minimum risk level of that user. *(delegated decision)*
- **FR-4.11** The system MUST sort alert stories by risk value, highest first, then by publication time, newest first. *(delegated decision)*
- **FR-4.12** The email and Slack alerts MUST contain a maximum of 10 stories. Each story MUST show the title, source name, risk value, categories, a short summary where FR-8.8 permits it, and a link to the original source. *(delegated decision)*
- **FR-4.13** The text message alert MUST contain a maximum of 3 story titles with risk values and a link to the dashboard. *(delegated decision)*
- **FR-4.14** When no story meets the criteria, the system MUST send a short alert that tells the user that there are no new stories at or above their risk level. *(delegated decision)*
- **FR-4.15** The system MUST NOT send a text message alert to a phone number until the user enters a verification code that the system sent to that number. *(delegated decision)*
- **FR-4.16** The system MUST send the alert to Slack through a Slack incoming webhook that the user supplies. The system MUST reject a webhook address that is not a Slack incoming webhook address. *(delegated decision)*
- **FR-4.17** When a user saves a Slack webhook, the system MUST send a test message to it and tell the user if the test failed. *(delegated decision)*
- **FR-4.18** When a delivery fails, the system MUST try again up to 3 times in 30 minutes. A failure on one channel MUST NOT stop delivery on the other channels. *(delegated decision)*
- **FR-4.19** The system MUST record the result of each delivery attempt (user, channel, time, success or failure, cause). *(delegated decision)*

### 5. Dashboard

- **FR-5.1** The system MUST show stories to a logged-in user on a dashboard.
- **FR-5.2** For each story, the dashboard MUST show: title, source names, publication time, categories, risk value, sentiment value, ATT&CK technique tags, short summary where FR-8.8 permits it, and a link to the original source. *(delegated decision)*
- **FR-5.3** By default, the dashboard MUST show stories from the last 24 hours, sorted by risk value, highest first. *(delegated decision)*
- **FR-5.4** A user MUST be able to filter stories by category, risk value, source, date range, and ATT&CK tactic or technique. *(delegated decision)*
- **FR-5.5** A user MUST be able to search stories by a keyword in the title or summary. *(delegated decision)*
- **FR-5.6** The dashboard MUST show the current Cloudflare Radar data. *(delegated decision)*

### 6. Authentication and Authorization

- **FR-6.1** The system MUST require a person to log in before it shows any content or function.
- **FR-6.2** The system MUST refuse access to a person who is not logged in.
- **FR-6.3** The system MUST refuse login when the credentials are not valid.
- **FR-6.4** The system MUST support two roles: admin and user.
- **FR-6.5** A person MUST log in with an email address, a password, and a time-based one-time code (TOTP). *(delegated decision)*
- **FR-6.6** The system MUST refuse a password that has fewer than 12 characters or that is on a list of known breached passwords. *(delegated decision)*
- **FR-6.7** After 5 failed login attempts for one account in 15 minutes, the system MUST block login for that account for 15 minutes. *(delegated decision)*
- **FR-6.8** The system MUST give the same error message for a wrong email address, a wrong password, and a wrong one-time code. *(delegated decision)*
- **FR-6.9** A user MUST be able to reset their password through a single-use link that the system sends to their email address. The link MUST expire after 30 minutes. *(delegated decision)*
- **FR-6.10** The system MUST end a session after 30 minutes without activity and when the user logs out. *(delegated decision)*
- **FR-6.11** Each account MUST have exactly one role. *(delegated decision)*
- **FR-6.12** A user MUST be able to view and change only their own alert settings and profile. The system MUST refuse access to the settings of other users. *(delegated decision)*
- **FR-6.13** The system MUST refuse access to admin functions for an account with the user role. *(delegated decision)*
- **FR-6.14** An admin MUST be able to do all that a user can do. *(delegated decision)*
- **FR-6.15** At first login, the system MUST make the person set up a time-based one-time code before it gives access to other functions. *(delegated decision)*

### 7. MITRE ATT&CK Analysis

- **FR-7.1** The system MUST tag each story with zero or more MITRE ATT&CK techniques that the story describes. Each tag MUST show the technique ID, the technique name, and its tactic. *(delegated decision)*
- **FR-7.2** Each ATT&CK tag MUST link to the page of that technique on the MITRE ATT&CK website. *(delegated decision)*
- **FR-7.3** The system MUST show ATT&CK tags on the dashboard and in the email alert. *(delegated decision)*

### 8. Source Management

- **FR-8.1** The system MUST permit only an admin to add, enable, disable, and remove a data source. *(delegated decision)*
- **FR-8.2** For each source, the admin MUST record: name, address, license or terms name, link to the license or terms, and permitted use. *(delegated decision)*
- **FR-8.3** The system MUST NOT enable a source that does not have a license record. *(delegated decision)*
- **FR-8.4** The system MUST show each source name and a link to the original item with each story. *(delegated decision)*
- **FR-8.5** The system MUST show the attribution text that the license of a source requires. *(delegated decision)*
- **FR-8.6** The system MUST show the status of each source to an admin: last successful collection, last failure, and cause. *(delegated decision)*
- **FR-8.7** When a source fails all collections for 24 hours, the system MUST show a warning to admins on the dashboard. *(delegated decision)*
- **FR-8.8** For each source, the admin MUST record which content the system may store and show: full text, verbatim excerpt, system summary, or headline and link only. The system MUST obey that record on the dashboard and in every alert. *(delegated decision, from research)*
- **FR-8.9** The system MUST NOT generate a summary for a source whose license does not permit changes to the content (for example, Kaspersky Securelist permits only verbatim excerpts). *(delegated decision, from research)*
- **FR-8.10** The system MUST show these notices on the dashboard: "This product uses the NVD API but is not endorsed or certified by the NVD."; "© 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation." with a link to the ATT&CK terms of use. *(delegated decision, from research)*
- **FR-8.11** The system MUST show a credit and link to haveibeenpwned.com on every surface (dashboard, email, Slack, text message) that shows Have I Been Pwned data. *(delegated decision, from research)*
- **FR-8.12** The system MUST mark a summary of SANS Internet Storm Center content with the CC BY-NC-SA 4.0 license. *(delegated decision, from research)*
- **FR-8.13** The system MUST NOT show the logo or seal of a government source, and MUST NOT state that a source endorses the service. *(delegated decision, from research)*

### 9. User Management

- **FR-9.1** The system MUST permit only an admin to create, disable, and delete an account and change its role. *(delegated decision)*
- **FR-9.2** The system MUST NOT permit self sign-up. *(delegated decision)*
- **FR-9.3** The system MUST NOT permit an admin to remove the admin role from the last active admin account. *(delegated decision)*
- **FR-9.4** The system MUST refuse login for a disabled account. *(delegated decision)*
- **FR-9.5** When an admin deletes an account, the system MUST delete the email address, phone number, and Slack webhook of that account. *(delegated decision)*
- **FR-9.6** The system MUST record each admin action (admin, action, target, time). An admin MUST be able to view this record. *(delegated decision)*
- **FR-9.7** The system MUST create the first admin account during installation. *(delegated decision)*

### 10. Data Retention

- **FR-10.1** The system MUST keep each story for 365 days after it was collected. After that time, the system MUST delete it. *(delegated decision)*
- **FR-10.2** The system MUST delete alert delivery records after 90 days. *(delegated decision)*

## Non-Functional Requirements

### 1. Use Constraints

- **NFR-1.1** The system MUST be private, non-commercial, and for personal use only.
- **NFR-1.2** The system MUST NOT sell, publish, or give collected content to persons outside the service.
- **NFR-1.3** If the service becomes commercial, an admin MUST disable or license each source that permits only non-commercial use (Cloudflare Radar, SANS Internet Storm Center, Canadian Centre for Cyber Security, abuse.ch URLhaus, ThreatFox, MalwareBazaar). *(delegated decision, from research)*

### 2. Capacity and Timeliness

- **NFR-2.1** The system MUST support a minimum of 10 user accounts. *(delegated decision)*
- **NFR-2.2** The system MUST start each morning alert delivery no later than 5 minutes after the scheduled time, and complete the first attempt within 15 minutes. *(delegated decision)*
- **NFR-2.3** The dashboard MUST show the first page of stories within 3 seconds for 1 year of stored stories. *(delegated decision)*

### 3. Security and Privacy

- **NFR-3.1** The system MUST use only HTTPS for all user access. *(delegated decision)*
- **NFR-3.2** The system MUST use contact data (email address, phone number, Slack webhook) only to send alerts and password reset messages. *(delegated decision)*
- **NFR-3.3** The system MUST NOT show passwords, one-time code secrets, or Slack webhook addresses after they are saved. *(delegated decision)*
- **NFR-3.4** The system MUST treat all collected content as not trusted. Collected content MUST NOT run as code in the dashboard, email, or Slack message. *(delegated decision)*

### 4. Availability

- **NFR-4.1** Availability is best effort. No service level is required. *(delegated decision)*

## Open Questions

None. All questions are resolved or decided. Items that the research could not verify are in `reports/Licensed cyber news sources.md` under the unverified items.

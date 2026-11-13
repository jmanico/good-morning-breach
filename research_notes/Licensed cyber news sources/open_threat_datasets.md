# Open Vulnerability & Threat-Intelligence Datasets/APIs: Licenses and Permitted Use (verified Nov 2026)

Context: the use case is a closed, login-only "morning cybersecurity news feed" that automatically collects data, processes it (categorize, risk-score, map to MITRE ATT&CK), shows it on a dashboard, and sends it in email/SMS/Slack alerts. These notes assume the service is **commercial**, meaning it is sold or offered to subscribers who are third parties. Showing data to subscribers counts as display or redistribution to third parties, not internal use. Where purely internal (own-org) use would change the verdict, the notes say so.

Verdict key: **GREEN** = commercial redistribution allowed (attribution and notices may be required). **YELLOW** = usable with conditions: attribution, share-alike, fair-use limits, mixed per-record licenses, or terms that are unclear. **RED** = commercial or third-party redistribution is prohibited, or needs a paid or written license.

All pages were fetched on 2026-11-13 unless noted otherwise.

## Q1. MITRE frameworks: ATT&CK, CVE List / cvelistV5, CWE, CAPEC, D3FEND, ATLAS

### Takeaway
All six MITRE resources allow commercial use. ATT&CK, CWE, CAPEC and CVE use a MITRE royalty-free license that requires you to reproduce MITRE's copyright designation and the license in any copy. D3FEND is MIT-licensed and ATLAS data is Apache-2.0. All are **GREEN**, with notice obligations and trademark care: do not imply MITRE endorsement.

### Cited Findings
- **MITRE ATT&CK** (https://attack.mitre.org; STIX data at https://github.com/mitre-attack/attack-stix-data). Terms of Use: "The MITRE Corporation (MITRE) hereby grants you a non-exclusive, royalty-free license to use ATT&CK® for research, development, and commercial purposes. Any copy you make for such purposes is authorized provided that you reproduce MITRE's copyright designation and this license in any such copy." The required attribution text is: **"© 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation."** — [ATT&CK Terms of Use](https://attack.mitre.org/resources/legal-and-branding/terms-of-use/)
- The attack-stix-data repo LICENSE.txt has the same license and the same "© 2026 The MITRE Corporation…" designation, plus an "AS IS" disclaimer and a statement that ATT&CK does not enumerate all possible techniques. — [attack-stix-data LICENSE.txt](https://raw.githubusercontent.com/mitre-attack/attack-stix-data/master/LICENSE.txt)
- The ATT&CK site footer says: "MITRE ATT&CK and ATT&CK are registered trademarks of The MITRE Corporation." — [ATT&CK Terms of Use page](https://attack.mitre.org/resources/legal-and-branding/terms-of-use/)
- **CVE List** (cve.org; JSON 5 records in github.com/CVEProject/cvelistV5; CVE Services API at cveawg.mitre.org). CVE Terms of Use, "CVE Usage": "MITRE hereby grants you a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable copyright license to reproduce, prepare derivative works of, publicly display, publicly perform, sublicense, and distribute Common Vulnerabilities and Exposures (CVE™). Any copy you make for such purposes is authorized provided that you reproduce MITRE's copyright designation and this license in any such copy." — [CVE Terms of Use (cve-website source; live page at https://www.cve.org/Legal/TermsOfUse is JS-rendered)](https://raw.githubusercontent.com/CVEProject/cve-website/dev/src/views/Legal/TermsOfUse.vue)
- **CWE**: "CWE™ is free to use by any organization or individual for any research, development, and/or commercial purposes… MITRE hereby grants you a non-exclusive, royalty-free license to use CWE for research, development, and commercial purposes. Any copy you make… reproduce MITRE's copyright designation and this license." CWE is a MITRE trademark. — [CWE Terms of Use](https://cwe.mitre.org/about/termsofuse.html)
- **CAPEC**: same MITRE license wording, "for research, development, and commercial purposes", with the same copyright-designation requirement. — [CAPEC Terms of Use](https://capec.mitre.org/about/termsofuse.html)
- **D3FEND**: the repo LICENSE is the "MIT License, Copyright (c) 2021 The MITRE Corporation". — [d3fend LICENSE (GitHub)](https://github.com/mitre/d3fend/blob/master/LICENSE) (redirects to d3fend/d3fend gh-pages)
- **ATLAS** (adversarial ML matrix): atlas-data LICENSE reads "Copyright 2021-2026 MITRE. Licensed under the Apache License, Version 2.0." — [atlas-data LICENSE](https://raw.githubusercontent.com/mitre-atlas/atlas-data/main/LICENSE)

### Inferences
- ATT&CK mapping and showing technique names and IDs on a commercial dashboard or in alerts is **GREEN**. Put the "© 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation." notice and a link to the license in the dashboard footer or about page, and in exported reports. A short link in email/SMS footers is the prudent minimum. The year in the notice changes with each release, so copy it from the current terms.
- CVE descriptions can be republished commercially. Keep the MITRE copyright designation and license notice. Note that CNA-authored content is licensed to MITRE under the submission grant, so the downstream CVE Usage license covers it.
- D3FEND (MIT) requires the copyright and permission notice in copies. ATLAS (Apache-2.0) requires the license and NOTICE file to be kept.
- Avoid using "MITRE ATT&CK" or "CVE" in a way that implies endorsement, because these are trademarks.

### Gaps
- The cvelistV5 repo LICENSE file was not at `main/LICENSE` (404), so I could not confirm whether the repo carries a separate LICENSE file. The cve.org Terms of Use govern.
- I did not fetch D3FEND's website terms (separate from the repo license) or any ATLAS website terms.

## Q2. Vulnerability data: FIRST EPSS, OSV.dev, GitHub Advisory Database, CISA Vulnrichment, CISA KEV, Exploit-DB, Metasploit, NVD

### Takeaway
EPSS, GHSA (CC-BY-4.0), Vulnrichment (CC0) and KEV (CC0) are **GREEN** for commercial use. GHSA needs attribution and EPSS asks for it. OSV.dev is **YELLOW** because licensing differs per source: most are CC-BY/CC0/MIT/Apache, but Ubuntu and Alpine are CC-BY-SA-4.0 and Chainguard/Wolfi is CC-BY-NC-ND-4.0. Exploit-DB (GPLv2 repo) and Metasploit (BSD-3, with GPL and other components) are fine to *reference* (links, "public exploit exists" flags). Redistributing exploit code itself needs license care. **YELLOW** for code; **GREEN** for metadata and flags.

### Cited Findings
- **FIRST EPSS** (https://www.first.org/epss/; CSV and API at https://api.first.org/data/v1/epss). FAQ: "Is EPSS free to use? Yes. EPSS scores are published freely via CSV download and API with no registration required. Attribution is requested when EPSS data is used in publications or products." Scores are "generated by Empirical Security and published freely to the public," and the EPSS SIG at FIRST maintains the system. — [EPSS FAQ](https://www.first.org/epss/faq)
- EPSS model versions: v3 (2023-03-07), v4 (from 2025-03-17), **v5 (v2026.06.15), published from 2026-06-15**. The page footer reads "Copyright © 2015—2026 by Forum of Incident Response and Security Teams." — [EPSS Get the Data](https://www.first.org/epss/data)
- Recent change: data, infrastructure and scoring are now provided by **Empirical Security** (FIRST hosts the SIG). — [EPSS FAQ](https://www.first.org/epss/faq)
- **GitHub Advisory Database** (https://github.com/github/advisory-database; also via the GitHub REST/GraphQL API). LICENSE.md is **Creative Commons Attribution 4.0 International**. — [advisory-database LICENSE.md](https://raw.githubusercontent.com/github/advisory-database/main/LICENSE.md)
- **OSV.dev** (API https://api.osv.dev; dumps at gs://osv-vulnerabilities/all.zip). Licenses listed per source: GitHub Advisory DB (CC-BY 4.0), PyPI (CC-BY 4.0), Go (CC-BY 4.0), Rust (CC0 1.0), Drupal (MIT), Global Security Database (CC0), OSS-Fuzz (CC-BY 4.0), Rocky Linux (BSD), AlmaLinux (MIT), Haskell (CC0), RConsortium (Apache 2.0), OpenSSF Malicious Packages (Apache 2.0), PSF (CC-BY 4.0), Bitnami (Apache 2.0), **Ubuntu (CC-BY-SA 4.0)**, opam (CC0), Erlang EEF CNA (CC-BY 4.0), Android (CC-BY 4.0), Azure Linux (MIT), BellSoft (MIT), **Chainguard/Wolfi (CC-BY-NC-ND 4.0 / Chainguard License for Commercial Scanners)**, CleanStart (Apache 2.0), Curl (MIT), Julia (CC-BY 4.0), Red Hat (CC-BY 4.0), Red Hat Lightwell (CC-BY 4.0), V8/Chromium (Apache 2.0). Converted data: Debian, **Alpine SecDB (CC-BY-SA 4.0)**, NVD CVEs. — [OSV.dev Data sources](https://google.github.io/osv.dev/data/)
- **CISA Vulnrichment** (https://github.com/cisagov/vulnrichment; SSVC, CWE and CVSS enrichment added to CVE records). LICENSE is **CC0 1.0 Universal**. — [vulnrichment LICENSE](https://raw.githubusercontent.com/cisagov/vulnrichment/develop/LICENSE)
- **CISA KEV** (https://www.cisa.gov/known-exploited-vulnerabilities-catalog; CSV/JSON feeds). "The KEV database is distributed under the Creative Commons 0 1.0 License. You may use this data in any legal manner but note that information provided at any 3rd party links… are bound by the policies and licenses of those 3rd party websites. Use of the information does not authorize you to use the CISA Logo or DHS Seal, nor should such use be interpreted as an endorsement by CISA or DHS." The catalog listed 1,781 entries when fetched. — [KEV license.txt](https://www.cisa.gov/sites/default/files/licenses/kev/license.txt) (also mirrored in [kev-data LICENSE](https://raw.githubusercontent.com/cisagov/kev-data/develop/LICENSE)); [KEV catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- **Exploit-DB** (https://www.exploit-db.com; repo https://gitlab.com/exploit-database/exploitdb). The repo LICENSE.md is **GNU GPL v2**. — [exploitdb LICENSE.md](https://gitlab.com/exploit-database/exploitdb/-/raw/main/LICENSE.md). Under the website Terms, user-submitted content is licensed to Exploit-DB and other users under a "nonexclusive, worldwide license to use Your Content", and submitters stay responsible for third-party licenses. — [Exploit-DB Terms](https://www.exploit-db.com/terms)
- **Metasploit Framework** (https://github.com/rapid7/metasploit-framework). "Copyright: 2006-2026, Rapid7, Inc. License: BSD-3-clause", with listed exceptions for third-party components under LGPL-2.1, GPL-2.0, GPL-3.0 (e.g., SharpHound), Apache-2.0 and MIT. — [metasploit-framework LICENSE](https://raw.githubusercontent.com/rapid7/metasploit-framework/master/LICENSE)

### Inferences
- **EPSS: GREEN.** Commercial use is fine. Add a credit such as "EPSS scores from FIRST.org (https://www.first.org/epss)" on the dashboard and in alerts that show scores, as the FAQ requests. No API key is needed.
- **GHSA: GREEN.** CC-BY-4.0 allows commercial use and adaptation if you give attribution, link the license and indicate changes.
- **Vulnrichment and KEV: GREEN.** CC0, no conditions. Do not use the CISA or DHS logo and do not imply endorsement.
- **OSV.dev: YELLOW.** Filter on each record's source or ecosystem. Exclude Chainguard/Wolfi records (NC-ND blocks commercial redistribution and derivative works) unless you take the Chainguard commercial-scanner license. Ubuntu and Alpine records are CC-BY-SA: any adapted version you redistribute must be shared under CC-BY-SA. That is safest if you only link to them or show facts (IDs, affected versions) rather than descriptive text. Other sources need attribution only, or nothing (CC0/MIT/Apache with notice).
- **Exploit-DB and Metasploit: GREEN for metadata and links** (e.g., "public exploit available: EDB-ID 12345" or "Metasploit module exists"). Bare facts and links carry low copyright risk. Redistributing exploit or module source code in alerts would trigger GPLv2 or component-license obligations and reputational and safety issues. Do not embed code. YELLOW if code is redistributed.

### Gaps
- I could not render the NVD API terms-of-use page (https://nvd.nist.gov/developers/terms-of-use; JS-rendered). From prior knowledge, which is unverified here: NVD requests the notice "This product uses data from the NVD API but is not endorsed or certified by the NVD", and API rate limits are higher with a free API key. Confirm this before relying on it.
- The EPSS API rate limits are not documented on the pages fetched (https://www.first.org/epss/api returned "Oops, where is this page?").
- GitHub REST API rate limits for advisories were not checked. The standard GitHub API limits apply.

## Q3. IOC and threat feeds: abuse.ch, OTX, MISP/CIRCL, Shadowserver, GreyNoise, Spamhaus DROP, PhishTank, OpenPhish

### Takeaway
abuse.ch changed its model significantly. All platforms now require an authenticated account (Auth-Key). **URLhaus, MalwareBazaar and ThreatFox are free only for not-for-profit use. Commercial users "may require a paid subscription" managed by Spamhaus.** Feodo Tracker, SSL Blacklist and YARAify remain CC0 for commercial use. OTX is free only for non-commercial use and bars redistribution or service-bureau use. GreyNoise's free tier is limited to internal or non-commercial use. OpenPhish's free feed bars all commercial use. Spamhaus DROP grants no license and bans using the Spamhaus name commercially. PhishTank says commercial API use is OK, but registration status is unclear.

### Cited Findings
- **abuse.ch Terms of Use** (https://abuse.ch/terms-of-use/):
  - "The Platforms are provided in collaboration with Spamhaus Technology Limited ('Spamhaus'), which acts as the primary licensee of the abuse.ch datasets."
  - "2.1 User Access: Access to the abuse.ch Platforms is provided only to: Authenticated Users… Please visit https://auth.abuse.ch/ to authenticate your account."
  - "3.1 … Authenticated Users may access the Platforms for not-for-profit purposes, subject to usage limitations imposed by abuse.ch and/or Spamhaus." Usage is measured in Queries and Exports. Under 3.2, exceeding the limits for "non-commercial or non-profit purposes… may require a paid subscription."
  - "3.4 Exceptions for Feodo Tracker, SSL Blacklist and YARAify… currently free to use without limitations according to Creative Commons principles (CC0) for both commercial and non-commercial purposes."
  - "4.1 Use of the Platforms listed below by companies, networks, or individuals with commercial or for-profit needs may require a paid subscription, which will be managed by Spamhaus… MalwareBazaar (Malware Samples), URLhaus (Malware URLs), ThreatFox (Malware IOCs)."
  - "4.2 Contributor Policy for Commercial Users: … must contribute consistently over a period of six months. During this period, the entity must subscribe and pay via Spamhaus," followed by a commercial review.
  - The page opens: "ABUSE.CH RESERVES THE RIGHT… TO RESTRICT, REVOKE OR PREVENT ACCESS… WITHOUT NOTICE." — [abuse.ch Terms of Use](https://abuse.ch/terms-of-use/)
- The abuse.ch APIs require an `Auth-Key` HTTP header obtained from auth.abuse.ch (MalwareBazaar, ThreatFox, URLhaus API docs). — [MalwareBazaar API](https://bazaar.abuse.ch/api/); [ThreatFox API](https://threatfox.abuse.ch/api/); [URLhaus API](https://urlhaus.abuse.ch/api/). One third-party archive page dates the Auth-Key requirement to 2024, but I found no official dated announcement (seen only in search snippets).
- **AlienVault / LevelBlue OTX** (https://otx.alienvault.com; DirectConnect API needs a free OTX key). EULA: "OTX is free to end users for non-commercial use." Use limitations bar users who "license, sell, rent, lease, transfer, assign, distribute, display, disclose, or otherwise commercially exploit OTX… or otherwise make it available to any third party (e.g., as a service bureau); (vii) share private, non-public indicators." — [LevelBlue OTX EULA](https://levelblue.com/terms/otx-eula)
- **MISP default feeds**: MISP ships a defaults.json list of third-party feeds, including e.g. "CIRCL OSINT Feed" (https://www.circl.lu/doc/misp/feed-osint, default: true) and "ELLIO: IP Feed (Community version)". Each entry is a pointer to an external provider, not a license. — [MISP feed-metadata defaults.json](https://raw.githubusercontent.com/MISP/MISP/2.5/app/files/feed-metadata/defaults.json). The CIRCL OSINT feed was publicly reachable and updated 2026-11-13. — [CIRCL OSINT feed index](https://www.circl.lu/doc/misp/feed-osint/)
- **Shadowserver**: free daily network reports, available on request after validation, about *your own* network or constituency. "Shadowserver offers all services free of charge, for public benefit. We don't sell data." — [Shadowserver Subscribe to Reports](https://www.shadowserver.org/what-we-do/network-reporting/get-reports/)
- **GreyNoise** (Community API / free tier). EULA 2.3: non-paid subscriptions are "for Free Customers wishing to use GreyNoise Products for non-commercial purposes." Section 3.1: "In every case (Free Customers and Paid Customers), such use is limited to your internal business purposes or noncommercial purposes such as academic research." Section 3.2 bars users who "rent, lease, lend, sell, license, sublicense, assign, distribute, publish, transfer, or otherwise make available the Platform to any third party." — [GreyNoise Terms/EULA](https://www.greynoise.io/terms)
- **Spamhaus DROP / DROPv6 / ASN-DROP** (JSON at https://www.spamhaus.org/drop/drop_v4.json, drop_v6.json, asndrop.json). "Provided… free of charge subject to these Terms." "3.1 The content of the DROP List is protected by copyright and database right. Nothing in these Terms shall be construed as granting an assignment or licence of any intellectual property rights." "3.2 YOU MAY UNDER NO CIRCUMSTANCES USE OR PERMIT ANY THIRD PARTY TO USE THE 'SPAMHAUS' NAME… OR ANY REFERENCE TO THE 'SPAMHAUS DATA' IN YOUR MARKETING, PROMOTIONAL OR ANY OTHER COMMERCIAL MATERIALS." Spamhaus may revoke access at its discretion. The lists are intended for firewall and routing filtering. — [Spamhaus DROP Fair Use Policy/Terms](https://www.spamhaus.org/blocklists/drop-fair-use-policy/); [DROP page](https://www.spamhaus.org/blocklists/do-not-route-or-peer/)
- **PhishTank** (Cisco Talos). FAQ: "Is it OK to use the API for both commercial and non-commercial uses? Yes, it is OK." Rate limits are per hour, and the FAQ says "Complete the free registration" to get a key. — [PhishTank FAQ](https://phishtank.org/faq.php). Wikipedia says new registration has been closed since 2020 and was still closed as of June 2026, which conflicts with the FAQ (secondary source, unverified). — [Wikipedia: PhishTank](https://en.wikipedia.org/wiki/PhishTank). phishtank.com/developer_info.php blocked automated fetch (Cloudflare).
- **OpenPhish** (free community feed). Terms: services "are provided solely for your personal use… You agree not to use any part of the Services for any commercial purposes, including… security operations, threat intelligence, detection, enrichment, product development, automation, customer protection… without the prior written consent of OpenPhish," and users agree not to "distribute, display, disclose, create derivative works or otherwise make… available to any third party." — [OpenPhish Terms of Use](https://openphish.com/terms.html)

### Inferences
- **abuse.ch Feodo Tracker, SSL Blacklist, YARAify: GREEN** (CC0, commercial OK; an Auth-Key may still be needed for API access).
- **abuse.ch URLhaus, MalwareBazaar, ThreatFox: RED for a commercial or for-profit service without a Spamhaus subscription.** They are YELLOW only if the operator is genuinely not-for-profit and stays within fair-use volumes. This is the main 2024–2026 licensing change; older docs and blogs often still call these "CC0".
- **OTX: RED** for a commercial subscriber-facing feed. "Display… to any third party" and "service bureau" use are prohibited, and free use is non-commercial only. A purely internal, non-commercial analyst tool would be YELLOW.
- **GreyNoise Community/free: RED** for displaying to subscribers. Internal business use is permitted, so enriching your own risk scores without showing GreyNoise data is arguably allowed internally. Republishing needs a paid or partner agreement.
- **Spamhaus DROP: YELLOW-to-RED.** It is free for network filtering, but no license to redistribute is granted and the Spamhaus name can't appear in commercial materials. Do not republish lists to subscribers or brand alerts as "Spamhaus data."
- **PhishTank: YELLOW.** Commercial API use is explicitly OK, but obtaining a key may be impossible if registration is closed, and the full license terms were not retrieved.
- **OpenPhish free feed: RED.** Use the commercial OpenPhish feed under contract instead.
- **MISP default feeds / CIRCL OSINT: YELLOW.** Licensing is per feed and per event, often carried as TLP markings. Respect TLP (only TLP:CLEAR is publishable) and each provider's terms. MISP lists the feeds but does not license them.
- **Shadowserver: YELLOW/RED.** The free reports cover your own networks or constituency. They are not a general republishable feed, and reuse terms for third-party distribution were not found.

### Gaps
- I did not find the exact abuse.ch query and export volume numbers, or Spamhaus commercial pricing.
- I did not find an official date for the abuse.ch Auth-Key requirement or the commercial-subscription shift. Third-party sources say 2024.
- GreyNoise Community API daily lookup limits were not checked.
- I did not retrieve PhishTank's full terms or confirm whether registration is open.
- The license of the CIRCL OSINT feed content itself was not found on the pages fetched.
- Shadowserver's Terms (https://www.shadowserver.org privacy & terms) were not fetched for redistribution clauses.

## Q4. Ransomware and breach trackers: ransomware.live, ransomwatch, Have I Been Pwned, DataBreaches-type sites

### Takeaway
ransomwatch code is public domain (Unlicense), but the project is a scraper; check the data separately. ransomware.live's free unauthenticated API v2 is "personal use only… not intended for corporate or business use". Its free API PRO (key required, 500,000 calls/month) is "for corporate and business use" subject to its Terms & Conditions, which I could not retrieve. HIBP breach and paste data is CC-BY-4.0 with mandatory visible attribution and a link, so it is **YELLOW/GREEN** (commercial OK with attribution; email-search APIs need a paid key).

### Cited Findings
- **ransomwatch** (https://github.com/joshhighet/ransomwatch). LICENSE is the Unlicense: "free and unencumbered software released into the public domain… for any purpose, commercial or non-commercial." — [ransomwatch LICENSE](https://raw.githubusercontent.com/joshhighet/ransomwatch/main/LICENSE)
- **ransomware.live** (https://www.ransomware.live; JSON at data.ransomware.live; API at api.ransomware.live and api-pro). API v1 is deprecated. **API v2 is free with no authentication, rate-limited to 1 req/min per endpoint, with victims delayed versus PRO, and is "Personal use only… It is not intended for corporate or business use."** **API PRO is "Free (for ever)", requires an API key, has "No rate limit, but fair use applies", 500,000 calls/month, and is marked "For everyone. For corporate and business use, read the Terms & Conditions before using the API."** API PRO+ is "Coming Soon". Footer: "© 2022–2026 All rights reserved." — [ransomware.live API](https://www.ransomware.live/api)
- ransomware.live is a personal project by Julien Mousqueton. It enriches data from third parties (Zscaler ThreatLabz, Hudson Rock, VirusTotal, Censys, FIRST EPSS, CIRCL, NIST, etc.) and tracked 422 groups and 34,038 victims as of 2026-11-13. — [ransomware.live About](https://www.ransomware.live/about)
- **Have I Been Pwned** (API base https://haveibeenpwned.com/api/v3). "License - breach & paste APIs: This work is licensed under a Creative Commons Attribution 4.0 International License… you're welcome to use the public API to build other services, but you must identify Have I Been Pwned as the source of the data. Clear and visible attribution with a link to haveibeenpwned.com should be present anywhere data from the service is used including when searching breaches or pastes and when representing breach descriptions." Acceptable use prohibits causing harm to breach victims, circumventing limits, impersonating user agents, "Misrepresenting the source of the data", and "Not adhering to the Creative Commons Attribution License." Email and domain search endpoints need an `hibp-api-key`, with rate limits by subscription in requests per minute and HTTP 429 with retry-after when exceeded. `/latestBreach`, `/breaches` and `/dataClasses` are documented as public catalog endpoints. — [HIBP API v3 docs](https://haveibeenpwned.com/API/v3)

### Inferences
- **HIBP breach catalog (/breaches, /latestBreach): GREEN with attribution.** Ideal for a "new breach added" morning item. Every dashboard card, email or Slack alert must say "Source: Have I Been Pwned" with a link. In SMS, include at least the name and a short link. **Per-email or domain searches** need a paid key and are only appropriate for subscribers' own verified domains.
- **ransomware.live: YELLOW.** For a commercial service, use API PRO (free key) and review the T&C. Do not use the v2 unauthenticated API (personal use only). Victim-naming content carries defamation and ethics risk. Show "claimed by group X" framing.
- **ransomwatch: GREEN for code.** The scraped leak-site data has no separate license and its sources are criminal sites. The project's activity status in 2026 was not checked.
- **DataBreaches.net-type trackers** (journalistic sites) are copyrighted editorial content. Treat them as news: headline, link and short excerpt only. YELLOW/RED for full-text reuse.

### Gaps
- I could not locate the ransomware.live Terms & Conditions URL (/terms returned 404), so the commercial terms of API PRO are unverified.
- I did not fetch HIBP pricing or key-tier details (the /Pricing URL returned 404) or the Pwned Passwords license.
- I did not research DataBreaches.net or similar site terms directly. The guidance above is general copyright inference.
- I did not check whether ransomwatch is still maintained in 2026.

## Summary verdict table (commercial, subscriber-facing service)

| Source | Endpoint | License | Commercial | Conditions | Key / limits | Verdict |
|---|---|---|---|---|---|---|
| MITRE ATT&CK | attack.mitre.org; github mitre-attack/attack-stix-data | MITRE ATT&CK Terms of Use (royalty-free) | Yes | Reproduce "© 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation." + license; trademark | None (static repo) | GREEN |
| CVE List / cvelistV5 | cve.org; github CVEProject/cvelistV5; cveawg.mitre.org | CVE Terms of Use (perpetual, royalty-free, sublicensable) | Yes | MITRE copyright + license notice | None for repo | GREEN |
| CWE / CAPEC | cwe.mitre.org, capec.mitre.org | MITRE Terms of Use | Yes | Copyright designation + license | None | GREEN |
| D3FEND | d3fend.mitre.org; github d3fend | MIT | Yes | Keep MIT notice | None | GREEN |
| ATLAS | atlas.mitre.org; github mitre-atlas/atlas-data | Apache-2.0 | Yes | License/NOTICE | None | GREEN |
| FIRST EPSS | api.first.org/data/v1/epss; CSV | FIRST published freely; attribution requested | Yes | Credit FIRST EPSS | No registration | GREEN |
| GitHub Advisory DB | github/advisory-database; GitHub API | CC-BY-4.0 | Yes | Attribution, license link, note changes | GitHub API limits | GREEN |
| OSV.dev | api.osv.dev; gs://osv-vulnerabilities | Per-source (CC-BY, CC0, MIT, Apache, CC-BY-SA, CC-BY-NC-ND) | Mostly | Filter Chainguard/Wolfi (NC-ND); SA for Ubuntu/Alpine | No key | YELLOW |
| CISA Vulnrichment | github cisagov/vulnrichment | CC0 1.0 | Yes | None | None | GREEN |
| CISA KEV | cisa.gov KEV CSV/JSON | CC0 1.0 | Yes | No CISA/DHS logo or endorsement | None | GREEN |
| Exploit-DB | exploit-db.com; gitlab exploitdb | GPLv2 (repo) + site Terms | Metadata yes; code GPL | Don't embed exploit code | None | GREEN (refs) / YELLOW (code) |
| Metasploit | github rapid7/metasploit-framework | BSD-3 + GPL/LGPL/Apache components | Metadata yes | Component licenses for code | None | GREEN (refs) |
| abuse.ch Feodo / SSLBL / YARAify | feodotracker.abuse.ch etc. | CC0 | Yes | None | Auth-Key may be needed | GREEN |
| abuse.ch URLhaus / MalwareBazaar / ThreatFox | *.abuse.ch/api (Auth-Key) | abuse.ch ToU (not-for-profit free) | **Paid via Spamhaus** | Fair-use volumes | Auth-Key required | RED (commercial) / YELLOW (non-profit) |
| LevelBlue OTX | otx.alienvault.com API (OTX key) | OTX EULA | **No** (non-commercial; no third-party display) | — | Free key | RED |
| MISP default feeds / CIRCL OSINT | circl.lu/doc/misp/feed-osint | Per feed / TLP | Varies | TLP:CLEAR only; per-provider terms | None for CIRCL OSINT | YELLOW |
| Shadowserver | Free reports (own networks) | Shadowserver terms | Own-network use | Not a general feed | Request + validation | YELLOW/RED |
| GreyNoise Community | api.greynoise.io community | GreyNoise EULA | Internal only; no redistribution | — | Free account | RED (display) / YELLOW (internal) |
| Spamhaus DROP | spamhaus.org/drop/*.json | DROP Terms (no licence granted) | Filtering use only | No "Spamhaus" name in commercial materials | None | YELLOW/RED |
| PhishTank | phishtank.org API | PhishTank terms | Yes (FAQ) | Descriptive User-Agent | Key; registration possibly closed | YELLOW |
| OpenPhish (free) | openphish.com feed | OpenPhish ToU | **No** | Personal only | — | RED |
| ransomware.live | api.ransomware.live (v2), API PRO | All rights reserved; v2 personal-only; PRO under T&C | PRO only | Read T&C | PRO key, 500k/mo | YELLOW |
| ransomwatch | github joshhighet/ransomwatch | Unlicense | Yes | — | — | GREEN (code) |
| Have I Been Pwned | haveibeenpwned.com/api/v3 | CC-BY-4.0 (breach & paste APIs) | Yes | Clear, visible attribution + link everywhere | Paid key for email/domain search; RPM by plan | GREEN (catalog, with attribution) |

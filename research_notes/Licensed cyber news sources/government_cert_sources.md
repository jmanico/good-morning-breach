# Government and National CERT Cybersecurity News/Advisory Sources: Feeds and Reuse Licenses (as of Nov 2026)

Use case under evaluation: a closed, login-only "morning cybersecurity news feed" service that automatically collects (RSS/API), summarizes, categorizes, scores, shows on a dashboard, and sends email/SMS/Slack alerts. Commercial (paid subscribers) vs non-commercial/internal use is distinguished where the license differs.

Research method note: license pages were fetched directly from the official sites on 2026-11-13 where possible (curl/WebFetch). Where a page could not be fetched (JS-rendered or timed out), this is flagged and the citation is to the official URL as surfaced by search, or to a third-party copy.

---

## 1. Summary table

| Source | Feed / API URL(s) | Content | License / terms | Commercial | Attribution | Full text vs summary | Rate limit / key | Verdict |
|---|---|---|---|---|---|---|---|---|
| CISA KEV catalog | https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json ; CSV: https://www.cisa.gov/sites/default/files/csv/known_exploited_vulnerabilities.csv ; schema: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities_schema.json | Structured exploited-CVE data | CC0 1.0 (https://www.cisa.gov/sites/default/files/licenses/kev/license.txt) | Yes | Not required (good practice: link) | Full data may be stored | None published | GREEN (no CISA logo/DHS seal, no implied endorsement) |
| CISA alerts & advisories / ICS / ICS medical / news / blog | https://www.cisa.gov/cybersecurity-advisories/all.xml ; https://www.cisa.gov/cybersecurity-advisories/ics-advisories.xml ; https://www.cisa.gov/cybersecurity-advisories/ics-medical-advisories.xml ; https://www.cisa.gov/news.xml ; https://www.cisa.gov/cisa/blog.xml | Advisories, alerts, news | US federal work (17 U.S.C. 105, no explicit CISA statement found); site content TLP:CLEAR "share without restriction, subject to copyright controls" (https://www.cisa.gov/notification); Terms of Use https://www.cisa.gov/terms-use | Yes | Not legally required; recommended | Full text OK for CISA-authored content; joint/co-sealed advisories may contain foreign-government or third-party copyrighted material -> store summary+link to be safe | None published; be polite | GREEN (with no-endorsement / no-logo caveat; YELLOW for co-sealed joint advisories' third-party portions) |
| NVD CVE API 2.0 (NIST) | https://services.nvd.nist.gov/rest/json/cves/2.0 (API docs: https://nvd.nist.gov/developers/start-here) | CVE records, CVSS, CPE | NVD API Terms of Use https://nvd.nist.gov/developers/terms-of-use | Yes (TOU contemplates commercial services) | Required notice: "This product uses the NVD API but is not endorsed or certified by the NVD." | Full data OK; if you modify content you may not attribute it as NVD | 5 req / rolling 30 s without key; 50 req / 30 s with free key; sleep ~6 s between requests recommended | GREEN (conditions: notice, no endorsement, no NVD attribution on modified data, key not shared) |
| FBI IC3 PSAs / CSAs | https://www.ic3.gov/PSA/RSS ; https://www.ic3.gov/CSA/RSS | Public service announcements, joint cybersecurity advisories | US federal work; no IC3-specific reuse page found | Likely yes | Recommended | Summary+link prudent (joint CSAs co-sealed with foreign agencies) | None found | GREEN/YELLOW (license page not verified) |
| UK NCSC | https://www.ncsc.gov.uk/api/1/services/v1/all-rss-feed.xml (feed URL from prior knowledge, NOT verified this session) | News, blogs, guidance, threat reports | Open Government Licence v3.0 via https://www.ncsc.gov.uk/section/about-this-website/terms-and-conditions | Yes (OGL permits commercial) | Required: acknowledge source + link to OGL "wherever possible" | Full text OK except third-party-licensed material and third-party-credited images; logos excluded | Not stated | GREEN |
| CERT-EU | https://cert.europa.eu/publications/security-advisories-rss | Security advisories | CC BY 4.0 via Commission Decision 2011/833/EU, https://cert.europa.eu/legal-notice | Yes | Required ("appropriate credit", "changes are indicated") | Full text OK; summaries must indicate changes | Not stated | GREEN |
| ENISA | No RSS URL verified | News, threat landscape, publications | ENISA Legal Notice https://www.enisa.europa.eu/about-enisa/legal-notice | Not restricted ("reproduction authorized, provided the source is acknowledged") | Required | Full text OK except Shutterstock images / third-party; logo only for press/media | n/a | GREEN (feed availability unverified) |
| Canada CCCS (Cyber Centre) | https://www.cyber.gc.ca/api/cccs/rss/v1/get?feed=alerts_advisories&lang=en ; https://www.cyber.gc.ca/api/cccs/rss/v1/get?feed=news_events_guidance&lang=en | Alerts & advisories, news/guidance | Canada.ca Terms and conditions (linked from cyber.gc.ca footer) https://www.canada.ca/en/transparency/terms.html | NO without prior written permission ("commercial redistribution") | Required for non-commercial: title, author, "copy of the version available at [URL]" | Non-commercial: full reproduction OK; commercial: headline+short summary+link only, or get permission | Not stated | Commercial: YELLOW/RED for full text (get permission), YELLOW for summary+link; Non-commercial/internal: GREEN |
| Australia ASD's ACSC | Likely https://www.cyber.gov.au/rss/alerts and https://www.cyber.gov.au/rss/advisories (from aggregators, NOT verified on official site) | Alerts, advisories, news, ISM updates | CC BY 4.0, https://www.cyber.gov.au/about-us/copyright | Yes | Required (CC BY) | Full text OK; excludes Coat of Arms, ACSC logo, third-party content, differently licensed material | Not stated | GREEN (verify feed URLs) |
| France CERT-FR (ANSSI) | https://cert.cyber.gouv.fr/feed/ (all); /alerte/feed/ ; /avis/feed/ ; /actualite/feed/ ; /cti/feed/ ; /dur/feed/ ; /ioc/feed/ ; /feed/scada/ ; API: https://cert.cyber.gouv.fr/openapi | Alerts, advisories (avis), news, CTI reports, hardening, IOCs | Licence Ouverte / Open Licence v2.0 (etalab-2.0), https://cert.cyber.gouv.fr/mentions-legales/ | Yes | Required (Etalab 2.0 requires source + date of last update) | Full text OK; ANSSI logo needs prior authorization; reuse does not imply ANSSI approval | Not stated | GREEN |
| Germany BSI / CERT-Bund | https://wid.cert-bund.de/content/public/securityAdvisory/rss ; https://wid.cert-bund.de/content/public/buergercert/rss ; BSI news feeds e.g. https://www.bsi.bund.de/SiteGlobals/Functions/RSSFeed/RSSNewsfeed/RSSNewsfeed_CSW.xml (listed on https://www.bsi.bund.de/EN/Service-Navi/Abonnements/RSS/rss.html) ; CSAF: https://www.bsi.bund.de/csaf | Security advisories (WID), consumer warnings, press, cyber-security warnings | BSI "Nutzungsbedingungen" page exists (linked in site header) but could not be retrieved; related NCC-DE terms require prior consent for commercial use | Unclear; likely requires consent for commercial reuse of text | Likely required | Summary+link prudent | Not stated | YELLOW |
| Japan JVN (JPCERT/CC + IPA) | https://jvn.jp/en/rss/jvn.rdf ; https://jvn.jp/en/rss/jvnJP.rdf ; https://jvn.jp/en/rss/jvnJP_adj.rdf ; MyJVN API https://jvndb.jvn.jp/en/apis/ | Vulnerability notes | "Copyright (c) 2000-2010 JPCERT/CC and IPA. All rights reserved." (https://jvn.jp/en/nav/jvn.html); MyJVN API Terms of Use (PDF) https://jvndb.jvn.jp/apis/myjvn//document/termsofuse.pdf | Unclear | Required | Headline+summary+link only; older notice asks to notify jvn@jvn.jp before redistribution | MyJVN TOU applies | YELLOW |
| CIRCL Vulnerability-Lookup (Luxembourg) | https://vulnerability.circl.lu/recent/all.atom (pattern /recent/<source>.<rss|atom>); docs https://vulnerability.circl.lu/documentation/feeds.html | Aggregated vulns, sightings | Software AGPL-3.0; data license per upstream source (not stated) | Depends on upstream (e.g., NVD, GitHub advisories, vendor feeds) | Per upstream | Per upstream | Not found | YELLOW |

---

## 2. Detailed notes by key question

## Q1. United States: CISA, NVD/NIST, FBI IC3, US-CERT — public domain status, TLP, trademark/endorsement restrictions

### Takeaway
CISA and NVD are the safest sources for commercial use: the KEV catalog is explicitly CC0, CISA site content is marked TLP:CLEAR and shareable without restriction (subject to copyright of any third-party material), and NVD's API terms allow commercial services but require a fixed non-endorsement notice and respect for 5/50-per-30-seconds rate limits. The only real restrictions are no CISA logo/DHS seal, no implied endorsement, and care with co-sealed joint advisories.

### Cited Findings
- CISA lists five official RSS feeds: CISA News https://www.cisa.gov/news.xml; CISA Blog https://www.cisa.gov/cisa/blog.xml; Cybersecurity Alerts & Advisories (all) https://www.cisa.gov/cybersecurity-advisories/all.xml; ICS Advisories https://www.cisa.gov/cybersecurity-advisories/ics-advisories.xml; ICS Medical Advisories https://www.cisa.gov/cybersecurity-advisories/ics-medical-advisories.xml — [CISA Subscribe to Updates](https://www.cisa.gov/about/contact-us/subscribe-updates-cisa)
- KEV catalog download links on the official catalog page: JSON `/sites/default/files/feeds/known_exploited_vulnerabilities.json`, CSV `/sites/default/files/csv/known_exploited_vulnerabilities.csv`, schema `/sites/default/files/feeds/known_exploited_vulnerabilities_schema.json`, and license `/sites/default/files/licenses/kev/license.txt` — [CISA KEV Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- KEV license text (verbatim): "The KEV database is distributed under the Creative Commons 0 1.0 License. You may use this data in any legal manner but note that information provided at any 3rd party links included in the KEV database are bound by the policies and licenses of those 3rd party websites. Use of the information does not authorize you to use the CISA Logo or DHS Seal, nor should such use be interpreted as an endorsement by CISA or DHS." — [CISA KEV license.txt](https://www.cisa.gov/sites/default/files/licenses/kev/license.txt)
- The cisagov GitHub mirror of KEV data is also CC0 — [cisagov/kev-data](https://github.com/cisagov/kev-data)
- CISA notification page: site and email content is TLP:CLEAR unless otherwise marked; "Recipients may share TLP:CLEAR information without restriction, subject to copyright controls." Also: "CISA does not endorse any commercial product or service... Any reference to specific commercial products... does not constitute or imply their endorsement, recommendation, or favoring by CISA." — [CISA Notification](https://www.cisa.gov/notification)
- CISA Terms of Use cover security/authorized use, accuracy disclaimers ("provided for general information only"), linking, and liability for technical disruption of the site; the fetched text contains no copyright/licensing restriction on reuse of content — [CISA Terms of Use](https://www.cisa.gov/terms-use)
- Changes 2025: On 12 May 2025 CISA announced routine updates/KEV notices would no longer be posted on its Alerts & Advisories page and would go only via social media, email, and RSS; it told KEV RSS users to subscribe via GovDelivery — [CISA announcement, 12 May 2025](https://www.cisa.gov/news-events/alerts/2025/05/12/update-how-cisa-shares-cyber-related-alerts-and-notifications). CISA reversed/paused the change the next day after pushback — [CISA statement](https://www.cisa.gov/news-events/news/cisa-statement-cyber-related-alerts-and-notifications); [Infosecurity Magazine](https://www.infosecurity-magazine.com/news/cisa-reverses-decision-advisory/); [heise](https://heise.de/-10381856). As of Nov 2026 the subscribe page still lists the five RSS feeds above — [CISA Subscribe](https://www.cisa.gov/about/contact-us/subscribe-updates-cisa)
- NVD API Terms of Use (verbatim, via scancode license DB copy): "Services which utilize or access the NVD API are asked to display the following notice prominently within the application: 'This product uses the NVD API but is not endorsed or certified by the NVD.' You may use the NVD name in order to identify the source of API content subject to these rules. You may not use the NVD name, to imply endorsement of any product, service, or entity, not-for-profit, commercial or otherwise." and "If you modify the content accessed through the API, you may not attribute the source as the NVD." Keys "should not be used by, or shared with, individuals or organizations other than the original requestor"; rate limits apply across all instances of an application. — [ScanCode LicenseDB copy of NVD API TOU](https://scancode-licensedb.aboutcode.org/nist-nvd-api-tou.html); official page [NVD Terms of Use](https://nvd.nist.gov/developers/terms-of-use) (JS-rendered; could not be fetched directly)
- NVD rate limits: public limit 5 requests in a rolling 30-second window; 50 requests per 30 seconds with an API key; NIST recommends sleeping ~6 seconds between requests — [NVD Start Here](https://nvd.nist.gov/developers/start-here) (via search snippet; page JS-rendered). A third-party copy listing "100 requests per 60 seconds" conflicts and appears outdated — [Wind River copy](https://open.windriver.com/info/uni-license-list/licenses/nist-nvd-api-tou.html)
- FBI IC3 site exposes RSS for PSAs (https://www.ic3.gov/PSA/RSS) and joint Cybersecurity Advisories (https://www.ic3.gov/CSA/RSS) — [IC3 home page links](https://www.ic3.gov/)
- Joint advisories (e.g., co-sealed CSAs) carry TLP:CLEAR "subject to standard copyright rules, information may be distributed without restriction" — [NSA/CISA joint CSA PDF](https://media.defense.gov/2024/Nov/12/2003581596/-1/-1/0/CSA-2023-TOP-ROUTINELY-EXPLOITED-VULNERABILITIES.PDF)

### Inferences
- CISA-, NIST- and FBI-authored text are works of the US federal government and so are not subject to US copyright under 17 U.S.C. 105; this is consistent with CISA's CC0 dedication for KEV and the "TLP:CLEAR ... without restriction, subject to copyright controls" language. However, I did not find an explicit cisa.gov page stating "public domain" for all site content. Practical result: full text may be stored and redistributed for both commercial and internal use.
- "Subject to copyright controls" matters for joint advisories co-authored with UK/AU/CA/NZ agencies (Crown copyright) or containing vendor-supplied content: for those, store summary + link, or rely on the partner's own open licence (OGL, CC BY), which is also permissive.
- US-CERT as a brand is retired/merged into CISA; the old us-cert.cisa.gov feeds were consolidated into the cisa.gov feeds above (prior knowledge; the current subscribe page lists no US-CERT feeds).
- Display rules for the product: show "This product uses the NVD API but is not endorsed or certified by the NVD." in the app (e.g., footer/about page); never use CISA logo/DHS seal or NVD name in marketing in a way that implies endorsement; if CVSS scores or descriptions are rewritten by AI, label them as derived and do not attribute the modified text to NVD.
- For a scoring engine, KEV (CC0) + NVD (permissive TOU) are both GREEN for commercial use.

### Gaps
- Could not fetch nvd.nist.gov pages directly (JS-rendered); rate limits are from official-page search snippets. Did not verify current status of legacy NVD 1.1 JSON data feeds (retirement announced earlier; see https://nvd.nist.gov/General/News/changes-to-feeds-and-apis).
- No IC3-specific copyright/reuse page found (disclaimer URL tried returned 404).
- Search surfaced an Oct 2026 article titled "CISA to discontinue cybersecurity alerts" (https://cybersecuritynews.com/cisa-to-discontinue-cybersecurity-alerts/) and an April 2026 CSA note on a CISA funding lapse (https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/04/CSA_research_note_cisa_funding_lapse_enterprise_guidance_20260423-csa-styled.pdf); neither was read, so whether any feeds were discontinued or paused in 2026 is unverified. The official subscribe page still listed feeds on 2026-11-13. Build monitoring for feed outages.
- No published rate limit for CISA RSS/KEV endpoints.

## Q2. UK NCSC

### Takeaway
NCSC content is Crown copyright licensed under the Open Government Licence v3.0, which permits commercial reuse, including full text, with attribution and an OGL link. Exceptions are third-party-licensed material, third-party-credited images, and logos. GREEN for both use cases.

### Cited Findings
- "Content on the Websites is, unless stated otherwise, subject to Crown copyright." Reuse is allowed "without prior permission" under OGL v3.0; "You must acknowledge the source of the content and include a link to the Open Government Licence wherever possible." — [NCSC Terms & conditions](https://www.ncsc.gov.uk/section/about-this-website/terms-and-conditions)
- Exceptions: "Where materials are stated to include material under licence from third parties, those materials are not licenced for re-use"; "Images credited to a third party are not Crown copyright and are not licenced for re-use"; logos are not covered by OGL — [NCSC Terms & conditions](https://www.ncsc.gov.uk/section/about-this-website/terms-and-conditions)
- Linking is allowed, but sites may not suggest they are "associated with, or endorsed by, the NCSC" — [NCSC Terms & conditions](https://www.ncsc.gov.uk/section/about-this-website/terms-and-conditions)
- The terms say nothing specific about RSS, scraping or automated access beyond banning unauthorized access and DoS — [NCSC Terms & conditions](https://www.ncsc.gov.uk/section/about-this-website/terms-and-conditions)
- The old copyright URL https://www.ncsc.gov.uk/section/about-this-website/copyright now returns 404 (terms consolidated into the terms-and-conditions page) — direct fetch 2026-11-13

### Inferences
- OGL v3.0 attribution statement to use: "Contains public sector information licensed under the Open Government Licence v3.0." with link (standard OGL wording).
- Don't ingest images by default; text-only ingestion avoids the third-party image exception.

### Gaps
- The NCSC RSS URL (https://www.ncsc.gov.uk/api/1/services/v1/all-rss-feed.xml, plus per-type feeds such as report-rss-feed.xml, news-rss-feed.xml) comes from prior knowledge and was not verified this session.

## Q3. EU: CERT-EU and ENISA

### Takeaway
CERT-EU content is CC BY 4.0 under the Commission reuse decision, with an official security-advisories RSS feed: GREEN. ENISA allows reproduction with source acknowledgement: GREEN, but no ENISA RSS feed was verified.

### Cited Findings
- CERT-EU: "Unless otherwise noted, the reuse of this document is authorised under a Creative Commons Attribution 4.0 International (CC-BY 4.0) licence... reuse is allowed, provided appropriate credit is given and changes are indicated." Logos, names, trademarks are excluded; third-party works may need separate permission — [CERT-EU Legal notice](https://cert.europa.eu/legal-notice)
- CERT-EU security advisories RSS: https://cert.europa.eu/publications/security-advisories-rss — link found on [CERT-EU Security Advisories](https://cert.europa.eu/publications/security-advisories)
- ENISA: "Reproduction of ENISA material published on this website is authorized, provided the source is acknowledged, unless it is stated otherwise." Shutterstock stock images are copyrighted; ENISA logo reproduction allowed only for press and media purposes; ENISA adopted an IPR policy in August 2021 — [ENISA Legal Notice](https://www.enisa.europa.eu/about-enisa/legal-notice)

### Inferences
- CC BY 4.0's "indicate if changes were made" means AI summaries of CERT-EU advisories should be labelled as summaries (e.g., "Summary by [service] of CERT-EU advisory X, CC BY 4.0").
- ENISA publishes reports more than time-sensitive alerts; it matters less for a morning feed. The ENISA EUVD (EU Vulnerability Database, launched 2025) may be a better ENISA data source, but its terms were not researched here.

### Gaps
- No ENISA RSS feed URL found; EUVD API terms not checked.

## Q4. Canada CCCS (Cyber Centre)

### Takeaway
The Cyber Centre site falls under the standard Government of Canada terms: free non-commercial reproduction with attribution, but commercial redistribution needs prior written permission. For a paid service, use only headline + your own short summary + link (or ask CSE for permission); for an internal tool, GREEN.

### Cited Findings
- Official RSS feeds: https://www.cyber.gc.ca/api/cccs/rss/v1/get?feed=alerts_advisories&lang=en and https://www.cyber.gc.ca/api/cccs/rss/v1/get?feed=news_events_guidance&lang=en — links found on cyber.gc.ca (fetched 2026-11-13)
- cyber.gc.ca footer "Terms and conditions" links to https://www.canada.ca/en/transparency/terms.html — fetched homepage 2026-11-13
- Non-commercial: "Unless otherwise specified you may reproduce the materials in whole or in part for non-commercial purposes, and in any format, without charge or further permission, provided you" exercise due diligence on accuracy, indicate the complete title and author, and indicate the reproduction is a copy of the version at [URL] — [Canada.ca Terms and conditions](https://www.canada.ca/en/transparency/terms.html)
- Commercial: "Unless otherwise specified, you may not reproduce materials on this site, in whole or in part, for the purposes of commercial redistribution without prior written permission from the copyright administrator." — [Canada.ca Terms and conditions](https://www.canada.ca/en/transparency/terms.html)
- The Cyber Centre portal terms say the name "Canadian Centre for Cyber Security" and graphics may not be used without prior written permission of CSE — [My Cyber Portal terms](https://portal-portail.cyber.gc.ca/en/termsandconditions); CSE terms direct commercial reproduction requests to CSE and say non-Canadian requests for copyright reproduction are generally not permitted — [CSE terms](https://www.cse-cst.gc.ca/en/about-apropos/terms-and-conditions)

### Inferences
- A subscription service that stores and re-sends full advisory text to paying customers is "commercial redistribution" -> needs permission (RED without it). Linking with a headline and an original short summary is likely low-risk (facts aren't copyrightable; short headlines are generally not protected), hence YELLOW.
- Internal, non-commercial use (e.g., a company's own internal SOC dashboard not sold to others) fits the non-commercial grant if attribution + source URL are shown: GREEN. Note: whether an internal tool at a for-profit company counts as "non-commercial" is a legal judgment; it is not redistribution for sale, which is the specific restriction.

### Gaps
- No cyber.gc.ca-specific API rate limit or terms for the /api/cccs/rss endpoint found.

## Q5. Australia ASD's ACSC

### Takeaway
cyber.gov.au content is CC BY 4.0, which permits commercial reuse with attribution: GREEN. Feed URLs not verified on the official site (site timed out).

### Cited Findings
- "All material presented on this website is provided under a Creative Commons Attribution 4.0 International licence", excluding the Commonwealth Coat of Arms, the ACSC logo, third-party content, and material marked with a different licence — [cyber.gov.au Copyright](https://www.cyber.gov.au/about-us/copyright) (via search result; direct fetch timed out)
- ASD's ACSC offers RSS feeds for advisories, alerts, news, ISM updates and publications — [ACSC social media community page](https://www.cyber.gov.au/about-us/about-asdacsc/who-we-are/ACSC-social-media-community)
- Aggregators list https://www.cyber.gov.au/rss/alerts and https://www.cyber.gov.au/rss/advisories (another lists https://www.cyber.gov.au/acsc/view-all-content/advisories/rss); /rss/threats appears inactive — [Feeder listing](https://feeder.co/discover/1dfce0e73d/cyber-gov-au), [Feeder cyber.gov.au](https://feeder.co/discover/site/cyber.gov.au)

### Inferences
- Attribution format e.g. "Source: Australian Signals Directorate, [title], cyber.gov.au, CC BY 4.0".

### Gaps
- Exact current feed URLs unverified (cyber.gov.au timed out for both WebFetch and curl).

## Q6. France CERT-FR (ANSSI)

### Takeaway
CERT-FR content is under the Licence Ouverte / Open Licence 2.0 (Etalab-2.0), which allows commercial reuse with attribution: GREEN. Note the site moved in 2025-2026 from cert.ssi.gouv.fr to cert.cyber.gouv.fr (301 redirect) and now exposes a richer set of feeds plus an API.

### Cited Findings
- "Sauf mention explicite contraire, les contenus présents sur le site internet du CERT-FR sont couverts par la Licence ouverte / open licence, version 2.0." The ANSSI logo is a registered trademark requiring prior authorization; reuse or modification "ne vaut pas approbation par l'ANSSI". Footer: content offered under "licence etalab-2.0" — [CERT-FR Mentions légales](https://cert.cyber.gouv.fr/mentions-legales/)
- https://www.cert.ssi.gouv.fr/mentions-legales/ returns 301 to https://cert.cyber.gouv.fr/mentions-legales/ — direct fetch 2026-11-13
- Feeds listed on [CERT-FR Flux RSS](https://cert.cyber.gouv.fr/flux-rss/): /feed/ (all), /alerte/feed/, /avis/feed/, /actualite/feed/, /cti/feed/, /dur/feed/ (hardening), /ioc/feed/, /feed/scada/; an API link at https://cert.cyber.gouv.fr/openapi

### Inferences
- Etalab 2.0 attribution requires naming the source and the date of last update (standard Etalab 2.0 term; not re-verified this session). Content is French; translation/summarization is a "modification" and is allowed.
- Old cert.ssi.gouv.fr feed URLs may keep redirecting, but point collectors at the new domain.

### Gaps
- OpenAPI spec contents and any rate limits not examined (page is JS-rendered).

## Q7. Germany BSI / CERT-Bund

### Takeaway
BSI offers RSS feeds (German only) including CERT-Bund WID security advisories and CSAF machine-readable advisories, but its usage terms page could not be retrieved; related BSI/NCC-DE terms require prior consent for commercial use. YELLOW: use summary+link for commercial; verify terms or ask BSI.

### Cited Findings
- BSI RSS page lists feeds including CERT-Bund WID: https://wid.cert-bund.de/content/public/securityAdvisory/rss and https://wid.cert-bund.de/content/public/buergercert/rss, plus BSI newsfeeds under https://www.bsi.bund.de/SiteGlobals/Functions/RSSFeed/RSSNewsfeed/ (e.g., RSSNewsfeed_CSW.xml for cyber-security warnings, RSSNewsfeed_Presse_Veranstaltungen.xml) — [BSI RSS](https://www.bsi.bund.de/EN/Service-Navi/Abonnements/RSS/rss.html)
- Feeds are only in German — [BSI RSS](https://www.bsi.bund.de/EN/Service-Navi/Abonnements/RSS/rss.html) (per search summary)
- NCC-DE (hosted by BSI) terms: further use such as commercial or journalistic requires prior consent (contact nkcs@bsi.bund.de) — [NCC-DE Nutzungsbedingungen](https://www.nkcs.bund.de/en/nutzungsbedingungen)
- BSI publishes CSAF advisories; CSAF 2.0 standardized as ISO/IEC 20153:2025 — [BSI it-sa 2025 presentation](https://edge.sitecorecloud.io/nurnbergmes0e18-nmmultisite6e34-prod50da-6065/media/Project/NuernbergMesse/it-sa/Actions/2025/IT-Security-Talks/itsa365-de-20250429_it-sa_insights_BSI_CSAFversum.pdf); info at https://www.bsi.bund.de/csaf

### Inferences
- German official works like laws and official decrees are free under §5 UrhG, but advisories/web articles are generally not "amtliche Werke" in that sense, so assume copyright applies; treat as YELLOW.

### Gaps
- BSI Nutzungsbedingungen page URL guessed wrong (404); actual terms not read. Recommend fetching via the "Nutzungsbedingungen" header link on bsi.bund.de.

## Q8. Japan JPCERT/CC and JVN

### Takeaway
JVN offers English RSS (RDF) feeds and the MyJVN API, but its site notice is "All rights reserved" and an older notice asks users to notify JVN before redistribution. YELLOW: headline + own summary + link; contact jvn@jvn.jp for full-text commercial reuse.

### Cited Findings
- English feeds: https://jvn.jp/en/rss/jvn.rdf, https://jvn.jp/en/rss/jvnJP.rdf, https://jvn.jp/en/rss/jvnJP_adj.rdf — linked from [JVN English home](https://jvn.jp/en/)
- JVN page footer: "Copyright (c) 2000-2010 JPCERT/CC and IPA. All rights reserved." — [JVN about](https://jvn.jp/en/nav/jvn.html)
- MyJVN API and its Terms of Use (IPA) — [MyJVN API](https://jvndb.jvn.jp/en/apis/); [MyJVN Terms of Use PDF](https://jvndb.jvn.jp/apis/myjvn//document/termsofuse.pdf)
- Older JPCERT/CC notice asked users to notify JVN (jvn@jvn.jp) before redistributing or excerpting — [JPCERT/CC JVN project page (mirror)](https://dcmpx.remotevs.com/jp/or/jpcert/www/SL/english/vh/project.html) (old, mirror source; currency unknown)

### Gaps
- Current JPCERT/CC website reuse policy not found; MyJVN TOU PDF not read in full.

## Q9. CIRCL (Luxembourg) and other aggregator-style CERT services

### Takeaway
CIRCL's Vulnerability-Lookup provides RSS/Atom feeds of recent vulnerabilities from many sources, but the AGPL covers the software, not the data; reuse rights follow each upstream source. YELLOW.

### Cited Findings
- Feed pattern /recent/<source>.<rss|atom>, e.g., https://vulnerability.circl.lu/recent/all.atom; also feeds for sightings, comments, bundles — [Vulnerability-Lookup feed docs](https://vulnerability.circl.lu/documentation/feeds.html)
- Software licensed AGPL-3.0 — [Vulnerability-Lookup](https://cve-search.github.io/vulnerability-lookup); [CIRCL service page](https://www.circl.lu/services/cve-search)

### Inferences
- Prefer going to primary sources (NVD, KEV, CERT-FR, etc.) and use CIRCL only for enrichment/sightings, unless CIRCL publishes a data license.

### Gaps
- No data license or rate limit found for vulnerability.circl.lu. Other notable CERTs (Netherlands NCSC-NL, Ireland NCSC-IE, Singapore CSA, New Zealand NCSC, Japan NISC, Korea KISA) were not researched within the tool budget.

## Q10. Cross-cutting conclusions for the morning-feed service (commercial vs internal)

### Takeaway
GREEN for commercial full-text use: CISA (incl. KEV), NVD (with notice), FBI IC3 (likely), UK NCSC (OGL), CERT-EU (CC BY), ENISA (attribution), ASD (CC BY), CERT-FR (Etalab 2.0). YELLOW: BSI, JVN, CIRCL, Canada CCCS (summary+link only for commercial). Canada CCCS full-text redistribution in a paid product without permission is RED; internal non-commercial is GREEN.

### Cited Findings
- See per-source citations above; key license pages: [CISA KEV license](https://www.cisa.gov/sites/default/files/licenses/kev/license.txt), [CISA notification/TLP](https://www.cisa.gov/notification), [NVD TOU](https://nvd.nist.gov/developers/terms-of-use), [NCSC T&C](https://www.ncsc.gov.uk/section/about-this-website/terms-and-conditions), [CERT-EU legal notice](https://cert.europa.eu/legal-notice), [ENISA legal notice](https://www.enisa.europa.eu/about-enisa/legal-notice), [Canada.ca terms](https://www.canada.ca/en/transparency/terms.html), [cyber.gov.au copyright](https://www.cyber.gov.au/about-us/copyright), [CERT-FR mentions légales](https://cert.cyber.gouv.fr/mentions-legales/)

### Inferences
- Common conditions across all GREEN sources: (1) attribution with source link (and licence link for OGL/CC BY/Etalab); (2) no logos/seals; (3) no implied endorsement; (4) mark AI summaries as derived/modified; (5) skip third-party images and third-party-licensed sections.
- A login-only service does not change the licensing analysis: these licenses don't distinguish public vs private redistribution, but Canada's terms do distinguish commercial vs non-commercial.
- Implement a per-source "license profile" (store_full_text: bool, attribution_template, licence_url, commercial_ok) to enforce these rules in the pipeline.

### Gaps
- None of these sources state rate limits for RSS; use conditional GET (ETag/If-Modified-Since) and polling intervals of 15-60 minutes as good practice (not a source requirement).
- This is not legal advice; confirm Canada, BSI and JVN positions directly with the agencies before commercial launch.

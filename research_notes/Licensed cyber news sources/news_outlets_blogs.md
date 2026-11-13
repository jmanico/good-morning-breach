# Cybersecurity news outlets and research blogs: RSS feeds and reuse terms (checked 2026-11-13)

Method: on 2026-11-13 I fetched each site's homepage and its terms or copyright page directly (curl and WebFetch). I pulled RSS URLs from the `<link rel="alternate" type="application/rss+xml">` tags and the license text from footers and terms pages. "Unverified" means the page could not be fetched, was rendered by JavaScript, returned 404, or was behind a bot challenge. Nothing here is legal advice.

Verdict key (as set in the assignment): GREEN = open license or explicit permission. YELLOW = all rights reserved, but a headline, link and short snippet is probably tolerated (some legal risk). RED = the terms explicitly prohibit the use.

## Openly licensed / research blogs: which have open licenses or explicit reuse permission?

### Takeaway
Only two sources checked here have a machine-verifiable open license: EFF Deeplinks (CC BY 4.0) and the SANS Internet Storm Center (CC BY-NC-SA 4.0, a non-commercial license). Kaspersky Securelist is not open-licensed, but its terms explicitly allow republishing article text or excerpts with a link and attribution. Every other vendor or research blog checked is "All rights reserved". Their terms either say nothing about RSS or limit content to personal, non-commercial use. For those, store and show only the headline, a short snippet and a link, never full text.

### Cited Findings

**SANS Internet Storm Center (ISC)**
- RSS: `https://isc.sans.edu/rssfeed.xml` (summary) and `https://isc.sans.edu/rssfeed_full.xml` (full text), both linked from the homepage — [isc.sans.edu](https://isc.sans.edu/)
- License: the footer reads "© 2026 SANS™ Internet Storm Center" with a `rel="license"` link to Creative Commons BY-NC-SA 4.0 (https://creativecommons.org/licenses/by-nc-sa/4.0/) — [isc.sans.edu](https://isc.sans.edu/)
- Verdict: **GREEN for internal or non-commercial use** (attribution required; ShareAlike applies to adaptations, which may include AI-written summaries). **YELLOW for a paid commercial service.** The NC clause bars commercial use of the licensed content, so a paid product should show only headline, link and attribution, or ask SANS for permission. The separate sans.org terms page could not be parsed (JavaScript-rendered), so it is unverified — [SANS terms](https://www.sans.org/terms-of-use/)

**EFF Deeplinks**
- RSS: not extracted automatically. The usual feed is `https://www.eff.org/rss/updates.xml` (unverified).
- License: "Any and all original material on the EFF website may be freely distributed at will under the Creative Commons Attribution 4.0 International License (CC-BY), unless otherwise noted. All material that is not original to EFF may require permission from the copyright holder to redistribute." — [EFF Copyright Policy](https://www.eff.org/copyright)
- Verdict: **GREEN** for commercial and internal use, including storing full text, as long as there is attribution and a link to the license. Watch for third-party material marked "otherwise noted".

**Kaspersky Securelist**
- RSS: `https://securelist.com/feed/` — [securelist.com](https://securelist.com/)
- Terms: "Kaspersky grants You the free of charge right to publish the text of articles (or excerpts from articles) from the Website, without images and without any modification, provided that you give a link to the source in the following format: an active hyperlink to the article on the Website and the name of the source (Securelist blog). If You cite the text of the article in fragments rather than in full, You must indicate that the text is published with abbreviations (or only a quote is given) and an active hyperlink to the full version of the article." Otherwise, distribution without consent is "strictly prohibited" — [Securelist Terms of use](https://securelist.com/terms-of-use/)
- Verdict: **GREEN, with conditions:** no images, no changes to the text, an active link, the credit "Securelist blog", and a note when text is excerpted. The clause does not separate commercial from non-commercial use. An AI-paraphrased summary arguably counts as "modification", so quote verbatim excerpts or write your own one-line description.

**ESET WeLiveSecurity**
- RSS: there is an "RSS Feed" footer link, but the exact URL was not extracted. The usual one is `https://www.welivesecurity.com/en/rss/feed/` (unverified). The footer says the blog is "Moving soon to the ESET Blog", so the feed URL may change — [welivesecurity.com](https://www.welivesecurity.com/en/)
- Terms: Documents "will not be used for any reasons, directly or indirectly connected with commercial use… are for informational, non-commercial or personal use only and will not be copied or posted on any network computer or broadcasted in any media… will not be modified… copyright notice… The resource will always be indicated." Footer: "Copyright © 1992 - 2026 ESET, spol. s r.o. All rights reserved." — [ESET Legal Information](https://www.welivesecurity.com/en/company/legal-information/)
- Verdict: **YELLOW for headline and link only. RED for storing or redistributing text in a commercial service.**

**Palo Alto Networks Unit 42**
- RSS: `https://unit42.paloaltonetworks.com/feed/` — [unit42.paloaltonetworks.com](https://unit42.paloaltonetworks.com/)
- Terms: "You may not: (a) modify the Site Content or use them for any commercial purpose, or any public display…" and "NO PORTION OF THE INFORMATION ON THIS SITE MAY BE REPRODUCED, MODIFIED, PUBLISHED, UPLOADED, POSTED, TRANSMITTED, OR DISTRIBUTED IN ANY FORM… WITHOUT THE PRIOR WRITTEN PERMISSION" — [Palo Alto Networks Terms of Use](https://www.paloaltonetworks.com/legal-notices/terms-of-use)
- Verdict: **RED for snippets or full text in a commercial service. YELLOW (with risk) for headline and link only.**

**Cisco Talos**
- RSS: `https://blog.talosintelligence.com/rss/` — [blog.talosintelligence.com](https://blog.talosintelligence.com/)
- Footer: "© Cisco Systems, Inc. and/or its affiliates. All rights reserved." — [Talos blog](https://blog.talosintelligence.com/). The keywords RSS, feed and non-commercial do not appear in the fetched Cisco Terms & Conditions, so no RSS-specific clause was found — [Cisco Terms & Conditions](https://www.cisco.com/c/en/us/about/legal/terms-conditions.html)
- Verdict: **YELLOW.**

**Microsoft Security Blog / MSRC**
- RSS: `https://www.microsoft.com/en-us/security/blog/feed/` — [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/). The MSRC blog feed URL was not found in the page (`https://msrc.microsoft.com/blog/feed` is unverified).
- Terms: "Unless otherwise specified, the Services are for your personal and non-commercial use." Users may not copy, distribute or sell materials. Documents (white papers, press releases and so on) are licensed "for informational and non-commercial or personal use only". RSS is not mentioned — [Microsoft Terms of Use](https://www.microsoft.com/en-us/legal/terms-of-use)
- Verdict: **YELLOW for headline and link. RED for full text in a commercial service.**

**Google Project Zero**
- RSS: googleprojectzero.blogspot.com now points to `https://projectzero.google/feed.xml` — [Project Zero](https://googleprojectzero.blogspot.com/)
- No Creative Commons or other license statement was found on the page. Google's general Terms of Service (effective July 30, 2026) cover content in Google services — [Google Terms](https://policies.google.com/terms)
- Verdict: **YELLOW** (unverified, no open license found).

**Google Security Blog / Google Cloud Threat Intelligence (Mandiant)**
- security.googleblog.com now redirects to blog.google, which the sandbox blocked, so the feed and terms are unverified. The Google Cloud threat-intel page links to Google's Terms of Service; its RSS URL was not found in the page (`https://cloudblog.withgoogle.com/topics/threat-intelligence/rss/` is unverified) — [Google Cloud Threat Intelligence](https://cloud.google.com/blog/topics/threat-intelligence)
- Verdict: **YELLOW** (unverified).

**Check Point Research**
- Footer: "© 1994-2026 Check Point Software Technologies LTD. All rights reserved." — [research.checkpoint.com](https://research.checkpoint.com/). No RSS link tag was found (`https://research.checkpoint.com/feed/` is unverified). The terms page could not be fetched.
- Verdict: **YELLOW** (terms unverified).

**Sophos (news.sophos.com)**
- The site redirects to sophos.com. The terms page downloaded but held no matching clauses (JavaScript-rendered). Unverified — [Sophos Website Terms](https://www.sophos.com/en-us/legal/website-terms-of-use)
- Verdict: **YELLOW** (unverified).

**The DFIR Report**
- RSS: `https://thedfirreport.com/feed/` — [thedfirreport.com](https://thedfirreport.com/)
- Footer: "© 2025 The DFIR Report. All Rights Reserved." No Creative Commons license was found. The /terms-of-service/ page returned 404. The site sells commercial Threat Intel feeds and private reports, so it has a direct commercial interest in its content — [thedfirreport.com](https://thedfirreport.com/)
- Verdict: **YELLOW.**

**Citizen Lab**
- RSS: `https://citizenlab.ca/feed/` — [citizenlab.ca](https://citizenlab.ca/)
- The footer shows only "© 2026 The Citizen Lab". No Creative Commons notice was found on the homepage or the About page. Report-level licenses, which have historically sometimes been CC, are unverified — [citizenlab.ca](https://citizenlab.ca/)
- Verdict: **YELLOW** (CC not confirmed).

**Krebs on Security**
- RSS: `https://krebsonsecurity.com/feed/` — [krebsonsecurity.com](https://krebsonsecurity.com/)
- The footer shows only "© Krebs on Security". No license or terms page was found.
- Verdict: **YELLOW.**

**Schneier on Security**
- RSS: `https://www.schneier.com/feed/` (also `/feed/atom/`) — [schneier.com](https://www.schneier.com/)
- No license statement was found on the homepage or the About page, and a web search found none either — [Schneier About](https://www.schneier.com/blog/about/)
- Verdict: **YELLOW** (unverified).

**OWASP**
- The homepage footer says "© 2026, OWASP Foundation Inc. All rights reserved." — [owasp.org](https://owasp.org/). OWASP project documents are often CC BY-SA, but the policy page could not be parsed, so that is unverified — [OWASP policies](https://owasp.org/www-policy/). No site-wide RSS feed was found.
- Verdict: **YELLOW** (low value as a news source).

**Risky Business News**
- RSS: `https://news.risky.biz/rss/` — [news.risky.biz](https://news.risky.biz/)
- No license or copyright text was found on the page.
- Verdict: **YELLOW** (unverified).

**Full Disclosure / oss-security mailing lists**
- Full Disclosure RSS: `https://seclists.org/rss/fulldisclosure.rss`. SecLists says "Here we provide web archives and RSS feeds (now including message extracts)" — [seclists.org](https://seclists.org/)
- oss-security is archived on Openwall; no RSS link tag or license text was found — [Openwall lists](https://www.openwall.com/lists/oss-security/). A SecLists oss-sec RSS feed probably exists but is unverified.
- Copyright in each post stays with its author, and no list-level license was found.
- Verdict: **YELLOW** (public disclosures; headline and link to the archive are low risk).

**Wikipedia / Wikinews**
- Not fetched in this session. As general knowledge, Wikipedia text is CC BY-SA 4.0 and Wikinews is CC BY 2.5. This is unverified here.

### Inferences
- For a paid service, only EFF (CC BY) and Securelist (express permission) clearly support redistributing text. ISC is usable for non-commercial or internal deployments, or as headline and link only.
- Vendor blogs (PANW, Microsoft, ESET) use broad terms that bar commercial reuse. In practice vendors want their research amplified, so asking each vendor's PR team for written permission is probably easy and turns YELLOW into GREEN.
- Sites that publish full-text feeds (ISC `rssfeed_full.xml`, WordPress feeds) make it easy to store full text, but the feed format grants no license. Store only title, link, date and at most about 1–2 sentences.

### Gaps
- Feed and terms pages for Google Security Blog, Sophos, Check Point, MSRC, Google Cloud TI and EFF were not confirmed because of JavaScript rendering or sandbox blocks.
- Citizen Lab, OWASP and Schneier license status remains unconfirmed.

## Commercial news outlets: what do their terms and RSS pages say?

### Takeaway
All of the commercial outlets are "All rights reserved". The two with explicit restrictive text are BleepingComputer (no redistribution in any form, and no storing content except for personal, non-commercial use) and Condé Nast (Ars Technica and Wired: RSS content carries the same restrictions as all site content, and no republishing online without permission). The rest show a copyright footer and nothing RSS-specific that could be found. Treat them as YELLOW: headline, short teaser of 1–2 sentences, link, and outlet name, with no full-text storage. Ask for permission or a license where the risk matters.

### Cited Findings

**BleepingComputer**
- RSS: the homepage has a "Social & Feeds" page. The usual feed is `https://www.bleepingcomputer.com/feed/` (unverified).
- Terms: "The publication, sale, or redistribution in any form or medium of text, photos, graphics, audio and/or video materials or any other form of proprietary content found on BleepingComputer.com is strictly prohibited without the prior written permission of Bleeping Computer LLC. Content that is publicly available on BleepingComputer.com may not be stored in a computer, except for personal and non-commercial use." Footer: "Copyright @ 2003 - 2026 Bleeping Computer ® LLC - All Rights Reserved" — [BleepingComputer Terms of Use](https://www.bleepingcomputer.com/terms-of-use/)
- Verdict: **RED for snippets or stored text in a commercial service.** A bare headline and link (facts and a pointer) is the most that might be defensible, and it is high-risk under these terms. Get written permission.

**The Hacker News**
- Footer: "© 2026 The Hacker News. All Rights Reserved." There is an "RSS Feeds" page, but no usage terms could be extracted from it — [thehackernews.com](https://thehackernews.com/), [THN RSS page](https://thehackernews.com/p/rss-feeds.html). The feed is commonly `https://feeds.feedburner.com/TheHackersNews` (unverified).
- Verdict: **YELLOW.**

**SecurityWeek**
- RSS: `https://www.securityweek.com/feed/` — [securityweek.com](https://www.securityweek.com/)
- Footer: "Copyright © 2026 SecurityWeek ®, a Wired Business Media Publication. All Rights Reserved." The terms page returned an empty response (unverified).
- Verdict: **YELLOW.**

**Dark Reading (Informa TechTarget)**
- The footer links to Informa TechTarget terms and a Wrights Media licensing and reprints request page (https://info.wrightsmedia.com/informa-licensing-reprints-request), which signals a paid licensing route — [darkreading.com](https://www.darkreading.com/), [Informa TechTarget Terms](https://www.informatechtarget.com/terms-and-conditions/). The terms text could not be parsed. RSS URL unverified (commonly `https://www.darkreading.com/rss.xml`).
- Verdict: **YELLOW. Reprint licensing is available.**

**The Record (Recorded Future News)**
- RSS: `https://therecord.media/feed/` (found in a link on the page) — [therecord.media](https://therecord.media/)
- Footer: "© Copyright 2026 | The Record from Recorded Future News". The /terms-of-use path returned 404. Recorded Future's corporate terms are product (SaaS) terms and say nothing about news reuse — [Recorded Future Terms](https://www.recordedfuture.com/legal/terms-of-use)
- Verdict: **YELLOW.**

**Help Net Security**
- RSS: `https://www.helpnetsecurity.com/feed/` — [helpnetsecurity.com](https://www.helpnetsecurity.com/)
- Footer: "© Copyright 1998-2026 by Help Net Security". The terms page could not be parsed for reuse clauses — [Help Net terms](https://www.helpnetsecurity.com/terms-of-use/)
- Verdict: **YELLOW.**

**CyberScoop (Scoop News Group)**
- RSS: `https://cyberscoop.com/feed/` — [cyberscoop.com](https://cyberscoop.com/)
- The terms URL returned an ad interstitial, so the terms are unverified — [CyberScoop terms](https://cyberscoop.com/terms-of-use/)
- Verdict: **YELLOW.**

**The Register (Situation Publishing)**
- Footer: "Copyright. All rights reserved © 1998-2026" with a "Ts & Cs" link — [theregister.com](https://www.theregister.com/). The old /Help/feeds/ page now returns 404, and the current RSS URL is unverified (commonly `https://www.theregister.com/security/headlines.atom`).
- Verdict: **YELLOW** (terms unverified).

**Ars Technica (Condé Nast)**
- RSS: `https://arstechnica.com/security/feed/` — [Ars Security](https://arstechnica.com/security/)
- Reprints page: "Copyright law in the United States permits readers to make copies of our work, but only for private use. You may not republish these materials online or in print, or distribute them to others, without explicit permission." — [Ars Reprints](https://arstechnica.com/reprints/)
- Condé Nast User Agreement: content available "via Real Simple Syndication (RSS)… [is] subject to the same terms, conditions, limitations and restrictions applicable to all Content… you may not use such Content or Product in a manner that exceeds such authorization." — [Condé Nast User Agreement](https://www.condenast.com/user-agreement)
- Verdict: **YELLOW for headline and link only. RED for republishing snippets or text without permission.**

**Wired (Condé Nast)**
- RSS: the homepage links `https://www.wired.com/feed/rss`. The security category feed is commonly `https://www.wired.com/feed/category/security/latest/rss` (unverified) — [Wired Security](https://www.wired.com/category/security/)
- Same Condé Nast User Agreement RSS clause as Ars — [Condé Nast User Agreement](https://www.condenast.com/user-agreement)
- Verdict: **YELLOW for headline and link. RED for text.**

**DataBreaches.net**
- Blocked by a Cloudflare "Just a moment..." challenge, so the terms and feed are unverified — [databreaches.net](https://databreaches.net/)
- Verdict: **YELLOW** (unverified). The bot challenge also suggests automated collection may be unwelcome.

### Inferences
- No commercial outlet checked grants an RSS-reuse license. Publishing an RSS feed is widely read as an implied permission to display headlines and links in readers, not to redistribute content commercially.
- A login-only internal dashboard is lower risk than a paid product, but terms like BleepingComputer's ("not be stored in a computer, except for personal and non-commercial use") apply to company-internal use as well.
- Practical mitigation: store only title, URL, date and outlet. Write your own one-line summary rather than copying the lede, and always link out. Seek licenses from Wrights Media (Informa) and Condé Nast for anything more.

### Gaps
- The terms texts for SecurityWeek, The Hacker News, Help Net, CyberScoop, The Register and Informa TechTarget could not be extracted (JavaScript-rendered, empty responses or interstitials).
- The exact feed URLs for BleepingComputer, THN, Dark Reading and The Register are unverified.

## General legal framing: is ingesting RSS headline + link + short excerpt accepted? Known disputes?

### Takeaway
Under US practice, showing a headline and a link is widely treated as low risk. Copying the lede or substantial excerpts for a paid service is where publishers have won. The leading case is AP v. Meltwater (S.D.N.Y. 2013), where a news-clipping service's excerpts were held not to be fair use. Contract terms (ToS) add a separate risk on top of copyright.

### Cited Findings
- In AP v. Meltwater (S.D.N.Y., March 2013), Judge Denise Cote held that Meltwater's subscription excerpting of AP stories was not fair use. She rejected the search-engine analogy because Meltwater served as a substitute rather than driving traffic, and found that copying the opening of a story could take "the heart" of the work. Commentators described the ruling as narrow and specific to for-profit clipping services, and EFF criticized it — [Steptoe SDNY blog](https://www.steptoe.com/en/news-publications/sdny-blog/judge-cote-rules-internet-news-aggregator-violates-copyright-laws-by-excerpting-news-stories-for-subscribers.html); [RCFP](https://www.rcfp.org/judge-rules-news-clipping-service-infringed-associated-press-copyrig/); [Techdirt](https://www.techdirt.com/?p=74861); [Mother Jones](https://www.motherjones.com/kevin-drum/2013/03/judge-limits-fair-use-only-slightly/)
- In the UK, Meltwater agreed to pay the Newspaper Licensing Agency for the right to use UK newspaper content after a Copyright Tribunal case — [Press Gazette](https://pressgazette.co.uk/media_law/associated-press-strikes-legal-blow-against-content-aggregators-after-winning-meltwater-case/)

### Inferences
- A "morning brief" service that sends excerpts to paying subscribers looks a lot like Meltwater (a commercial clipping substitute). Showing only headline and link, with an original short summary, keeps the use transformative and drives traffic to the source.
- In the EU, the press publishers' right (DSM Directive Art. 15) gives publishers rights over snippets beyond "very short extracts". This is not researched here and should be checked if the service will be offered in the EU.

### Gaps
- The appeal or settlement outcome of AP v. Meltwater was not confirmed in this session (reportedly settled in 2013; unverified).
- Disputes specific to cybersecurity outlets (for example, takedowns of security news aggregators) were not found.

# Platform Terms for Community/Social Cybersecurity News Sources (Reddit, Cloudflare Radar, HN, Mastodon, Bluesky, GitHub) — as of Nov 2026

Context: a closed, login-only, presumably paid/commercial "morning cybersecurity news feed" that automatically collects, AI-summarizes, categorizes, risk-scores, shows on a dashboard, and pushes email/SMS/Slack alerts.

Research method note: Reddit's Data API Terms and Developer Terms were retrieved directly from redditinc.com (raw HTML, Nov 13 2026). The Reddit Help Center pages (Responsible Builder Policy, Data API Wiki) returned 403 to automated fetching, and a further attempt to get them was blocked in this environment, so I could not read their text. radar.cloudflare.com/about and infosec.exchange/about also returned 403 / bot-challenge pages.

## Reddit: Data API Terms, Developer Terms, Responsible Builder Policy, approval, rate limits, commercial/AI rules, deletion, RSS, r/netsec and r/cybersecurity

### Takeaway
**RED for a commercial service without a signed Reddit agreement.** The Data API Terms (last revised July 20, 2026) and Developer Terms (last revised March 24, 2026) say commercial use, or use "by or on behalf of a business or as part of a service or product that is monetized," needs a separate written agreement. The license covers only copying and displaying User Content *unmodified* (formatting only). AI summarization is a modification, so it falls outside it. Since Nov 11, 2025, new API credentials also need manual approval under the Responsible Builder Policy. At best, linking out to Reddit threads found by hand or by a non-Reddit source (title plus URL, no body text) is lower risk. Automated ingestion of post or comment text for summaries is not permitted without a deal.

### Cited Findings
- Data API Terms header: "Effective June 19, 2023. Last Revised July 20, 2026." — [Reddit Data API Terms](https://redditinc.com/policies/data-api-terms)
- Scope covers non-API access too: "You may use the Data APIs and any other Materials you access from our Services, whether using the Data APIs or not, only in accordance with the Data API Terms." — [Data API Terms, preamble](https://redditinc.com/policies/data-api-terms)
- §2.4 User Content license: "copy and display the User Content using the Data API solely as necessary to develop, deploy, distribute, and run your App to your App Users. You may not modify the User Content except to format it for such display." No other rights are granted, "including any right to use User Content for other purposes, such as for training a machine learning or AI model, without the express permission of rightsholders." — [Data API Terms §2.4](https://redditinc.com/policies/data-api-terms)
- §2.8: you must use the OAuth token you were given and "will not misrepresent or mask either the user agent or OAuth identity." — [Data API Terms §2.8](https://redditinc.com/policies/data-api-terms)
- §2.9: Reddit "may set and enforce limits" on requests and on the number of App Users, "in our sole discretion." — [Data API Terms §2.9](https://redditinc.com/policies/data-api-terms)
- §3.1: "If you are interested in using the Data APIs for commercial purposes, research in excess of rate limits, or for any use that is not expressly permitted under the Data API Terms, then you will need to enter into a separate agreement with Reddit." — [Data API Terms §3.1](https://redditinc.com/policies/data-api-terms)
- §3.2 restrictions include: no "derive revenues from the use or provision of the Data APIs ... unless there is express written approval from Reddit"; no using "User Content to train a machine learning or AI model without the express permission of rightsholders"; and no "use or retain any User Content ... beyond your approved use case, and you must immediately delete any data not required for it." — [Data API Terms §3.2](https://redditinc.com/policies/data-api-terms)
- §4.2 Attribution: you must display attributions required by the Developer Documentation. You may use the "Reddit" wordmark only in the form "[name] for Reddit," and you may not suggest partnership or endorsement. — [Data API Terms §4.2](https://redditinc.com/policies/data-api-terms)
- Termination: you must "delete any cached or stored User Content ... This includes any data or models that were derived from User Content." — [Data API Terms](https://redditinc.com/policies/data-api-terms)
- Developer Terms header: "Effective September 24, 2024. Last Revised March 24, 2026." — [Reddit Developer Terms](https://redditinc.com/policies/developer-terms)
- Developer Terms §4.1 Commercial Use Restrictions: unless approved in writing, you will not "access or use any of the Reddit Services and Data by or on behalf of a business or as part of a service or product that is monetized" or "monetize, or otherwise obtain or derive revenues of any kind from any portion of Reddit Services and Data, whether directly or indirectly, including from any data derived from the foregoing." — [Developer Terms §4.1](https://redditinc.com/policies/developer-terms)
- Developer Terms deletion sync: "if any User Content is deleted, gains protected status, or is suspended, withheld, modified, or removed from the Services, you will delete or modify that User Content and ... related App Content ... as soon as possible." You must also delete data when it is no longer needed for approved functionality, when Reddit or the user requests it, or when the app stops operating. Data at rest must be encrypted. — [Developer Terms](https://redditinc.com/policies/developer-terms)
- Developer Terms App Review: Reddit "may require you to submit your App for Reddit's review and approval ... after hitting API rate limits, or at any time," using "human and automated review including third-party LLMs." — [Developer Terms](https://redditinc.com/policies/developer-terms)
- Both terms pages link the Responsible Builder Policy at support.reddithelp.com/hc/articles/42728983564564. I could not retrieve its text (HTTP 403). — [Data API Terms (link)](https://redditinc.com/policies/data-api-terms); [RBP URL](https://support.reddithelp.com/hc/articles/42728983564564)
- Nov 11, 2025: a Reddit admin post in r/redditdev, "Introducing the Responsible Builder Policy," closed self-service API access. New credentials need a reviewed request, existing access was said to be unaffected, and developers were pointed to Devvit. Several commenters reported being denied. This comes from a third-party mirror of r/redditdev, not the original thread. — [r/redditdev mirror](https://r.datuan.dev/r/redditdev/comments/1oug31u/introducing_the_responsible_builder_policy_new/nobt04v)
- Unverified third-party claims: approval targets a roughly 7-day response ([molehill blog](https://molehill.pages.dev/blog/reddit_killed_self-service_api_keys_your_options_for_automated_reddit_integration)); unauthenticated .json endpoints return 403 since May 30, 2026 ([Medium](https://medium.com/@alex_79882/reddits-api-is-officially-dead-in-2026-here-s-what-i-use-instead-f88ee5b809c8)); the RBP help article was last updated June 5, 2026 ([redditapis.com](https://www.redditapis.com/blogs/reddit-bot-rules-2026)); commercial pricing is $0.24 per 1,000 calls ([socialcrawl.dev](https://www.socialcrawl.dev/blog/reddit-data-api-2026.md)). None of these could be confirmed against Reddit pages.
- History: the April 2023 terms update introduced paid commercial access and the ML exclusion ([The Register](https://www.theregister.com/2023/04/18/reddit_charging_ai_api/)). In May 2024, Reddit's Public Content Policy said commercial use of public data requires a contract ([Axios](https://www.axios.com/2024/05/09/reddit-public-data-content-policy-ai-privacy)). In June 2024, Reddit said bots and crawlers without an agreement would be rate-limited or blocked ([TechCrunch](https://techcrunch.com/2024/06/25/reddits-upcoming-changes-attempt-to-safeguard-the-platform-against-ai-crawlers)).

### Inferences
- **Summarization:** §2.4 allows display only, "may not modify ... except to format." Generating AI summaries or risk scores from post or comment text is outside the granted license, so it needs Reddit's written approval. Risk-scoring is a "derived data" use. §4.1 of the Developer Terms reaches revenue "derived from" Reddit data "directly or indirectly."
- **Commercial use:** a closed, login-only subscription service is "a service or product that is monetized." Even an internal-only company tool is use "by or on behalf of a business," which §4.1 also covers. So a free-tier or self-service path is unavailable in both cases.
- **RSS (.rss feeds):** no Reddit document I retrieved gives explicit permission for subreddit .rss feeds. The preamble applies the Data API Terms to Materials accessed "whether using the Data APIs or not," so RSS ingestion is most likely governed by the same commercial and modification limits. Under §2.8, unauthenticated .rss polling is also hard to square with "must use the Access Info we provided you." Treat RSS as not a loophole.
- **Practical paths:** (a) sign a commercial Data API agreement with Reddit; (b) don't ingest Reddit at all, and let editors manually link to notable r/netsec threads (title plus link only, no copied text); (c) use the linked-to primary source (vendor advisory or blog) found via Reddit as the actual ingested content.
- **Rate limits:** the widely cited 100 QPM per OAuth client figure could not be verified on an official page in this session. §2.9 gives Reddit full discretion over limits.

### Gaps
- I could not read the Responsible Builder Policy text or the Data API Wiki (rate limits, user-agent format, attribution specifics). Both returned 403, and an alternate retrieval was blocked. A human should read https://support.reddithelp.com/hc/articles/42728983564564 and https://support.reddithelp.com/hc/en-us/articles/16160319875092 in a browser.
- I could not check r/netsec and r/cybersecurity bot rules: their sidebars and wikis were not retrieved. Both subreddits are known to restrict self-promotion and bot posting, but read-only collection is mainly governed by Reddit's terms, not subreddit rules. Unverified.
- Commercial Data API pricing and the approval timeline are unconfirmed by Reddit.

## Cloudflare Radar (including "zero-wire"): what it is, license, API terms, data, rate limits, token, commercial use

### Takeaway
**YELLOW, close to RED for commercial use.** https://radar.cloudflare.com/zero-wire is real and not a typo. "Zero Wire" is a public vulnerability-intelligence feed on Radar that Cloudflare announced on Nov 3, 2026. It has an RSS link on the page. Radar API data and downloads are licensed **CC BY-NC 4.0**, which bars commercial use. Embeddable and downloadable charts are CC BY 4.0. Commercial use needs an exception from radar@cloudflare.com. The API is free but needs a Cloudflare API token with Account > Radar > Read. Linking out with headlines is low risk. Reproducing or summarizing Radar data in a paid product requires the exception.

### Cited Findings
- Zero Wire page ("Understand the latest security threats"): a curated list with a "Needs attention" section, where items are marked Patch, Review, or Assess, and a "Reference" section. Each item has tags, Risk, Recommended action, vendor and blog links, and a "Last reviewed" date. Examples seen on Nov 13, 2026 include CVE-2026-126187 (React Server Components RCE), OpenSSH on musl/Alpine, "php2shell," a Linux TCP UAF, eMudhra intermediate CA compromise, "node2shell," and Citrix NetScaler. The page offers an RSS subscription. No license text appears on the page itself. — [Cloudflare Radar Zero Wire](https://radar.cloudflare.com/zero-wire)
- Cloudflare blog "Introducing Zero Wire, a hub for investigating critical Internet vulnerabilities," Nov 3, 2026: "a public vulnerability intelligence feed on Cloudflare Radar" that brings "the clarity of a news wire service" to critical security developments. It focuses on critical CVEs in Internet-facing software. The post does not mention an API or reuse terms. — [Cloudflare Blog](https://blog.cloudflare.com/zero-wire/)
- A third-party write-up (Nov 4, 2026) says briefings include WAF coverage and a copyable agent prompt, and gives the path as radar.cloudflare.com/security/zero-wire. The /zero-wire path resolved directly in this session. — [flaviocopes.com](https://flaviocopes.com/cloudflare-zero-wire.md); [runtimewire](https://runtimewire.com/article/cloudflare-zero-wire-critical-cve-briefings-radar)
- "Data available via Radar API endpoints is made available under the CC BY-NC 4.0 license." "Radar's API is free." — [Cloudflare Radar docs](https://developers.cloudflare.com/radar/)
- The Radar About page applies CC BY-NC 4.0 to data from the API or direct download, puts embeddable/downloadable charts and images under CC BY 4.0, and says to contact radar@cloudflare.com for a commercial-use exception. This is from a search-result summary because the About page returned 403 to direct fetch. — [Radar About](https://radar.cloudflare.com/about)
- CC BY-NC 4.0 license text (NonCommercial plus attribution) — [Creative Commons](https://creativecommons.org/licenses/by-nc/4.0/)
- Token: "Create a Custom Token, with Account > Radar in the Permissions group, and select Read as the access level." — [Radar: Make your first API request](https://developers.cloudflare.com/radar/get-started/first-request/)
- Rate limit: the Cloudflare API global limit is 1,200 requests per 5 minutes per user, cumulative across dashboard, API key, and token. Exceeding it returns HTTP 429 for 5 minutes. No Radar-specific limit was found. — [Cloudflare API limits](https://developers.cloudflare.com/fundamentals/api/reference/limits/)
- Data sources: Cloudflare's global network (NetFlows, HTTP requests, DNS queries) and anonymized 1.1.1.1 resolver data. Radar's docs have Investigate sections, and Get started includes "Configure alerts" (Radar notifications). — [Radar docs](https://developers.cloudflare.com/radar/); [Get started](https://developers.cloudflare.com/radar/get-started/)

### Inferences
- A closed, paid login service that summarizes and redistributes Radar data or Zero Wire briefings is "primarily intended for or directed towards commercial advantage," so CC BY-NC 4.0 would not cover it. Get a written exception from radar@cloudflare.com, or limit use to a headline plus link to the Radar page.
- For an internal, non-monetized tool, CC BY-NC 4.0 probably allows use with attribution ("Source: Cloudflare Radar, CC BY-NC 4.0" plus link), though internal corporate use is a grey area under NC.
- Zero Wire briefings are Cloudflare-authored editorial text. It is unclear whether CC BY-NC (meant for "data") or the general Cloudflare website terms apply to them. Treat them as copyrighted editorial content and use headline, link, and CVE IDs only. CVE IDs are facts.
- Outage, attack, and BGP (hijack/leak) and traffic-anomaly datasets exist in the Radar API (via the API reference), but I did not enumerate the endpoints in this session.

### Gaps
- I could not fetch the full Radar About page or a Zero Wire-specific license or API.
- I did not find whether Zero Wire has an API endpoint. Only RSS was observed.
- I did not find whether Radar endpoints have limits beyond the global 1,200 per 5 minutes.
- I did not verify the exact BGP hijack/leak, outage (Cloudflare Radar Outage Center), and attack endpoint list from the API reference: https://developers.cloudflare.com/api/resources/radar/

## Hacker News (Y Combinator) Firebase API

### Takeaway
**GREEN/YELLOW.** The official API at hacker-news.firebaseio.com/v0 needs no key or auth and has "no rate limit." The repo is MIT-licensed, but that covers the docs and code, not the user-posted content. No API-specific commercial or AI restrictions are stated. Comment text is user content, so storing titles, URLs, scores, and IDs and linking back is safe. Republishing or summarizing comment bodies in a paid product carries copyright and HN-terms risk that I did not verify.

### Cited Findings
- "There is currently no rate limit." Endpoints live under https://hacker-news.firebaseio.com/v0/. "Only users that have public activity ... are available through the API." The API may change without backward compatibility. The repo is labeled MIT license, and there are no API-specific terms. — [HackerNews/API on GitHub](https://github.com/HackerNews/API)

### Inferences
- Best fit: poll topstories/newstories, keep security-related stories by title or domain, and ingest the linked article URL instead of HN text. Attribute with "via Hacker News" plus a link to the item.

### Gaps
- I did not retrieve Y Combinator's site legal terms (https://www.ycombinator.com/legal/) for any clauses on commercial reuse of HN content.

## Mastodon (infosec.exchange)

### Takeaway
**YELLOW.** Public posts are reachable via the Mastodon REST API and RSS for accounts and hashtags. There is no central platform API license. Each server sets its own rules, and post authors hold copyright. infosec.exchange's rules govern accounts posting on the server and say nothing about read-only collection. However, it bans LLM/AI-operated accounts, and its website now sits behind an Anubis anti-bot wall, which signals hostility to scraping. Read-only, low-volume polling of specific accounts and hashtags with link-back is defensible. Republishing AI summaries of individuals' posts in a paid feed is ethically and legally sensitive. Prefer linking to the original posts.

### Cited Findings
- Rule 14: accounts posting more than 50% via automation must be labeled bots. Automated public posts are limited to 1 per hour and 24 per day. — [infosec.exchange rules API](https://infosec.exchange/api/v1/instance/rules)
- Rule 17: "LLM and AI operated accounts are not permitted." — [infosec.exchange rules API](https://infosec.exchange/api/v1/instance/rules)
- Rule 11: "No attacks against (or from) the instance." Details are on the wiki. — [infosec.exchange rules API](https://infosec.exchange/api/v1/instance/rules); [wiki](https://wiki.infosec.exchange/rules/start)
- infosec.exchange/about returned an Anubis bot-protection "Access Denied" page to automated fetch (Anubis v1.28.2). — [infosec.exchange/about](https://infosec.exchange/about)

### Inferences
- The service should not post to infosec.exchange with an AI account. Read-only API use (public timelines and tag timelines) is unaffected by the posting rules but should be rate-limited and identify itself honestly.
- Many Mastodon users mark their profiles #nobot or #noindex. Honoring these opt-outs and deletions is good practice.

### Gaps
- I did not retrieve infosec.exchange's terms or privacy policy, Mastodon API default rate limits (commonly 300 requests per 5 minutes, unverified here), or the .rss endpoint behavior behind Anubis.

## Bluesky (AT Protocol)

### Takeaway
**YELLOW, partly unverified.** The AT Protocol is open, and public posts are retrievable via the public AppView API or Jetstream/firehose without approval. I could not retrieve the developer guidelines: docs.bsky.app redirects to bsky.network, which came back empty. Bluesky has publicly worked on a user-consent framework for AI and generative uses that third parties are asked to honor. Deletions propagate over the protocol, and third-party apps are expected to process them.

### Cited Findings
- Bluesky said in Nov 2024 that it won't train AI on user posts. Its open API still lets third parties collect data. — [TechCrunch](https://techcrunch.com/2024/11/27/blueskys-open-api-means-anyone-can-scrape-your-data-for-ai-training)
- Mar 2025: Bluesky proposed account- and post-level consent settings covering four categories, including generative AI, and asked outside developers to respect them. Bluesky acknowledged it is up to outside developers to comply. — [TechCrunch](https://techcrunch.com/2025/03/15/bluesky-users-debate-plans-around-user-data-and-ai-training/)
- Bluesky's ToS says account deletion does not guarantee removal from other AT Protocol apps. — [ConductAtlas summary of Bluesky ToS](https://conductatlas.com/platform/bluesky/bluesky-terms-of-service/decentralized-content-deletion-caveat/)
- docs.bsky.app/docs/support/developer-guidelines returns a 308 redirect to bsky.network/docs/support/developer-guidelines, which returned empty content. — [Bluesky developer guidelines](https://docs.bsky.app/docs/support/developer-guidelines)

### Inferences
- Design for compliance: subscribe to delete events and purge, check any consent or label metadata before AI summarization, and link to the original posts.

### Gaps
- Official developer guidelines text, including any commercial-use, AI, deletion, and rate-limit clauses, is unverified. A human should read it in a browser.

## GitHub (Security Advisories, trending)

### Takeaway
**GREEN for the GitHub Advisory Database. YELLOW for "trending."** Advisory data is **CC-BY 4.0**, so commercial use is allowed with attribution. Access is via the REST/GraphQL API (token recommended) or the github/advisory-database git repo (OSV JSON). Under GitHub ToS §H, the API cannot be used for spam, sharing tokens to evade rate limits, or selling users' personal info. GitHub has no official "trending" API, so scraping the trending page has no clear authorization. Use search API queries instead.

### Cited Findings
- "This project is licensed under the terms of the CC-BY 4.0 open source license." — [github/advisory-database](https://github.com/github/advisory-database)
- ToS §H API Terms: excessive or abusive use can lead to suspension. "You may not share API tokens to exceed GitHub's rate limitations." "You may not use the API to download data or Content from GitHub for spamming purposes" or "for the purposes of selling GitHub users' personal information." — [GitHub Terms of Service](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)
- ToS §D.9 (new, about automated access for AI training) contains reciprocity language, with exemptions for academic research and for entities with fewer than 700M MAU. This came from a fetch summary, and the exact wording was not quoted. — [GitHub Terms of Service](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)

### Inferences
- The Advisory DB is the best-licensed source in this set for a commercial feed. Attribute "GitHub Advisory Database (CC-BY 4.0)" with a link to the GHSA ID.
- The REST API standard limits (5,000 requests/hour authenticated, 60/hour unauthenticated) are well known, but I did not verify them this session.

### Gaps
- I did not verify the exact §D.9 text or the current REST rate-limit page, and found no official trending API.

## Summary verdict table (for report writer)

| Source | Access | License/terms | Commercial closed service | AI summarization | Key / approval | Verdict |
|---|---|---|---|---|---|---|
| Reddit (API, .json, .rss) | OAuth Data API; RSS | Data API Terms (rev. 2026-07-20); Developer Terms (rev. 2026-03-24); Responsible Builder Policy (Nov 2025) | Separate written agreement required | Display-only license, "may not modify"; ML training barred without rightsholder permission | Manual approval since Nov 11, 2025 | **RED** (unless licensed) |
| Cloudflare Radar API / data | REST API, downloads | CC BY-NC 4.0 (charts CC BY 4.0) | Not allowed without exception (radar@cloudflare.com) | Allowed only within NC terms | Free token, Account > Radar > Read; 1,200 req/5 min | **YELLOW** (internal) / **RED** (paid, no exception) |
| Cloudflare Zero Wire (launched 2026-11-03) | Web page + RSS | No explicit license; Cloudflare editorial | Headline + link only | Avoid reproducing text | None | **YELLOW** |
| Hacker News | Firebase API, no auth | MIT (repo); no API terms | Not restricted in API docs | Not addressed | None; no rate limit | **GREEN/YELLOW** |
| Mastodon infosec.exchange | REST API / RSS | Per-server rules; authors' copyright | Not addressed | AI accounts banned (posting) | Optional | **YELLOW** |
| Bluesky | AppView API / Jetstream | Dev guidelines unverified | Unverified | Consent framework proposed | None for public reads | **YELLOW** |
| GitHub Advisory DB | REST/GraphQL, git repo | CC-BY 4.0; GitHub ToS §H | Allowed with attribution | Allowed | Token recommended | **GREEN** |

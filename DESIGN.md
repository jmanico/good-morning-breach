---
version: alpha
name: Good Morning Breach
description: First-light briefing design for a private morning cybersecurity news feed, ranked by risk.
colors:
  primary: "#2E2A8C"
  primary-hover: "#1F1C66"
  on-primary: "#FFFFFF"
  neutral: "#EFEEF5"
  surface: "#FFFFFF"
  on-surface: "#1D1A3B"
  on-surface-muted: "#4E4A6B"
  outline: "#7C7898"
  hairline: "#D9D7E5"
  selected: "#E3E1F2"
  dawn: "#F4B740"
  risk-critical: "#A3142E"
  risk-high: "#A8420A"
  risk-medium: "#7A5B00"
  risk-low: "#2C6A47"
  risk-info: "#4B5574"
  error: "#A3142E"
  error-container: "#FBE9EC"
  warning-container: "#FFF1CC"
  success: "#2C6A47"
typography:
  headline-lg:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 32px
    fontWeight: 700
    lineHeight: 1.15
    letterSpacing: -0.01em
  headline-md:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 24px
    fontWeight: 700
    lineHeight: 1.2
  headline-sm:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 19px
    fontWeight: 700
    lineHeight: 1.3
  story-title:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 18px
    fontWeight: 600
    lineHeight: 1.35
  body-md:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  body-sm:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.45
  label-md:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 14px
    fontWeight: 700
    lineHeight: 1.2
  label-sm:
    fontFamily: Atkinson Hyperlegible Next
    fontSize: 13px
    fontWeight: 700
    lineHeight: 1.2
  identifier:
    fontFamily: Atkinson Hyperlegible Mono
    fontSize: 14px
    fontWeight: 500
    lineHeight: 1.3
rounded:
  none: 0px
  sm: 3px
  md: 6px
  full: 9999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 40px
  gutter: 16px
  rail: 280px
  content-max: 760px
  spine-critical: 8px
  spine-high: 6px
  spine-medium: 4px
  spine-low: 3px
  spine-info: 2px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 44px
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    rounded: "{rounded.md}"
    height: 44px
  button-destructive:
    backgroundColor: "{colors.risk-critical}"
    textColor: "{colors.on-primary}"
    rounded: "{rounded.md}"
    height: 44px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.sm}"
    height: 44px
  input-error:
    backgroundColor: "{colors.error-container}"
    textColor: "{colors.on-surface}"
  risk-chip-critical:
    backgroundColor: "{colors.risk-critical}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.sm}"
  risk-chip-high:
    backgroundColor: "{colors.risk-high}"
    textColor: "{colors.on-primary}"
  risk-chip-medium:
    backgroundColor: "{colors.risk-medium}"
    textColor: "{colors.on-primary}"
  risk-chip-low:
    backgroundColor: "{colors.risk-low}"
    textColor: "{colors.on-primary}"
  risk-chip-info:
    backgroundColor: "{colors.risk-info}"
    textColor: "{colors.on-primary}"
  tag-chip:
    backgroundColor: "{colors.selected}"
    textColor: "{colors.on-surface}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
  story-row:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.story-title}"
    rounded: "{rounded.none}"
    padding: 16px
  account-bar:
    backgroundColor: "{colors.on-surface}"
    textColor: "{colors.surface}"
    height: 56px
  page:
    backgroundColor: "{colors.neutral}"
    textColor: "{colors.on-surface}"
  story-meta:
    textColor: "{colors.on-surface-muted}"
    typography: "{typography.body-sm}"
  divider:
    backgroundColor: "{colors.hairline}"
    height: 1px
  logo-sun:
    backgroundColor: "{colors.dawn}"
  status-success:
    textColor: "{colors.success}"
    typography: "{typography.label-md}"
  admin-warning:
    backgroundColor: "{colors.warning-container}"
    textColor: "{colors.on-surface}"
---

# Good Morning Breach

## Overview

**Brief.**
- **Subject:** a private, non-commercial morning feed of cybersecurity news. It collects from licensed sources, ranks each story by risk, tags it with MITRE ATT&CK techniques, and sends a 07:00 alert.
- **Audience:** the owner and up to about ten invited security readers. They are the people who check their phones before coffee. Admins also manage sources, licenses, and accounts.
- **Primary job of the main screens:**
  - *Dashboard:* answer "what needs me this morning?" in under a minute. Show the riskiest stories first and give a link to each original source.
  - *Sign-in:* a closed door with email, password, and TOTP.
  - *Alert settings:* "when and where do I hear about it?"
  - *Admin:* source licenses and health, users, and the audit log.

**Rationale.** The product is a briefing read at first light, so the palette is pre-dawn. It uses night-indigo ink on a pale first-light lavender, and the sun-amber appears only in the mark. Risk is the one bold element. Each story carries a left **risk spine**, and the spine gets thicker and darker as risk rises (8 px Critical down to 2 px Informational). A morning list sorted by risk therefore looks like a horizon going from deep red to slate. Everything else is quiet: one typeface family chosen for legibility, plain sentence-case labels, and no decoration.

**Revisions after plan review.**
- *Dark terminal, neon accent, and monospace everywhere:* this is the cyber-product default (generic trait 2). I replaced it with a light first-light palette.
- *SaaS card per story:* I replaced the cards with one continuous ledger, separated only by hairlines and spines (trait 4).
- *Monospace for small labels:* I restricted it to identifiers people must read character by character, such as CVE IDs and ATT&CK technique IDs (trait 5).
- *Middle-dot metadata strings and "→" links:* I removed them. Metadata goes in labelled pairs.

## Colors

Night indigo and first light, plus a five-step risk ramp. Every text pair passes 4.5:1, and every UI or graphic pair passes 3:1 (WCAG 2.2 AA). The ratios are in the table below.

- **Night indigo (#2E2A8C, primary):** the only colour for actions and links. Hover is #1F1C66.
- **Ink (#1D1A3B, on-surface):** body text, the account bar background, and focus rings.
- **Muted ink (#4E4A6B):** metadata and secondary text. It is never used for an action.
- **First light (#EFEEF5, neutral):** the page background. Content sits on white (#FFFFFF, surface). The product has a light theme only. *(delegated decision)* Dark mode is not supported.
- **Outline (#7C7898):** input and control borders. It meets the 3:1 component contrast. Hairline (#D9D7E5) is used for decorative dividers only and never for the only boundary of a control.
- **Risk ramp:** Critical #A3142E, High #A8420A, Medium #7A5B00, Low #2C6A47, Informational #4B5574. White text on each chip passes 6.0:1 or better. Risk is never shown by colour alone: the word and the spine width carry it too.
- **Dawn (#F4B740):** used only in the logo, where it sits on ink. It is never used for text on light backgrounds.
- **Containers:** error #FBE9EC and warning #FFF1CC, both with ink text.

| Pair | Ratio | Use |
|---|---|---|
| Ink on white / first light | 16.6 / 14.4 | Text |
| Muted ink on white / first light | 8.4 / 7.2 | Metadata |
| Primary on white / first light | 11.5 / 10.0 | Links, secondary buttons |
| White on primary / primary-hover | 11.5 / 14.8 | Primary buttons |
| White on each risk colour | 6.1 to 7.8 | Risk chips, destructive button |
| Each risk colour on first light | 5.3 to 6.8 | Spines, risk text |
| Outline on white / first light | 4.2 / 3.7 | Control borders |
| Ink focus ring on first light | 14.4 | Focus indicator |
| Error red on error container | 6.7 | Error text |
| Dawn on ink | 9.3 | Logo |

## Typography

**Atkinson Hyperlegible Next** is used for everything. It was designed by the Braille Institute so that characters cannot be mistaken for each other, which suits a reader skimming at 07:00. **Atkinson Hyperlegible Mono** is used only for CVE IDs, ATT&CK IDs (T1190), and similar identifiers. Both fonts are SIL OFL licensed. The fonts are self-hosted, because the service makes no third-party requests. *(delegated decision)* The preview falls back to system fonts.

- The scale steps by roughly 1.2 from 13 to 32 px. Body text is 16 px at 1.5 line height. Line length stays at 75 characters or fewer.
- Weights are 400 for reading and 600 or 700 for titles and labels. No other weights are used.
- Sentence case everywhere. Never use all-caps labels, tracked-out eyebrows, or a single highlighted word in a headline.

## Layout

- **Desktop (≥1024 px):** three regions. There is a 56 px ink account bar across the top. The story ledger has a maximum width of 760 px. A 280 px right rail holds Cloudflare Radar data and, for admins only, source health. Filters sit above the ledger in a "Filter stories" disclosure, collapsed by default. Active filters always show as removable chips, so the stories stay above the fold.
- **Mobile (<1024 px):** a single column. The same collapsed filters apply. Navigation wraps to a second row of the account bar. The Radar rail moves below the ledger. The side gutter is 16 px.
- **Times:** all times show in the user's alert time zone (FR-4.6), so the dashboard and the alert agree. *(delegated decision)*
- **Rhythm:** 8 px base with a 4 px half-step. All text is left-aligned and nothing is justified.
- **Dashboard order:** account bar, then the "This morning" heading with a count by risk level, then filters and search, then the ledger, then the rail, then the required notices (FR-8.10, FR-8.11) in the footer.

```
┌ account bar: mark  Good Morning Breach        jo@…  Admin  Sign out ┐
│ This morning, 13 Nov   ▮3 Critical ▮5 High ▮9 Medium ...  │ Radar      │
│ [Search] [Category▾] [Risk▾] [Source▾] [Dates] [ATT&CK▾]  │ outages    │
│ ▌ Critical  Title of story                               │ attacks    │
│ ▌           Sources, time, categories, T-tags, summary   │ BGP        │
│ ▎ High      ...                                          │ Source     │
│ footer: NVD notice, MITRE notice, HIBP credit            │ health     │
└──────────────────────────────────────────────────────────────────────┘
```

## Elevation & Depth

The design is flat. Hierarchy comes from tone (white content on a first-light page), the ink account bar, and the risk spine. There are no shadows except one, on modal dialogs: `0 8px 24px rgba(29,26,59,.28)`. Dialogs also dim the page with a 60% ink scrim, so the shadow is the only lifted surface and always means "decide now".

## Shapes

The corner radius encodes what a shape is:
- **0 px:** story rows and layout regions.
- **3 px:** inputs and risk chips.
- **6 px:** buttons.
- **Full pill:** category and ATT&CK tag chips only.

The risk spine is a square-ended bar on the row's left edge.

## Components

All components are framework-neutral. Every interactive element has a 3 px ink focus outline with a 2 px offset and a target of at least 44 × 44 px.

- **Buttons:**
  - *Primary:* filled indigo.
  - *Secondary:* white with an indigo label and an outline border.
  - *Destructive:* filled Critical red, used only inside a confirmation dialog.
  - *States:* default, hover (darker), focus (ring), disabled (outline border, muted text, and the reason shown beside the button), busy (label changes to the action in progress, such as "Sending test…").
- **Inputs:** a label above the field and helper text below it. The error state uses the error container, a red 2 px border, and an error message that starts with "Error:" in red text. The field is linked to its message.
- **Risk chip:** a filled chip with the risk word. It always appears next to the spine of the same colour.
- **Sentiment:** plain muted text ("Tone: Negative"). It never uses colour or emoji, because tone is not risk.
- **Tag chips:** categories, and ATT&CK tags shown as `T1190` plus the technique name and its tactic. They link to attack.mitre.org (FR-7.2). Active filter chips use the selected fill and have a remove control.
- **Story row:** spine, risk chip, title linked to the original source, source names, publication time, categories, ATT&CK tags, a summary only where FR-8.8 permits it, and the attribution or licence line (FR-8.5, FR-8.12). Variants:
  - *Headline-only:* for Reddit, "all rights reserved", and Zero Wire sources. It has no summary, no category, and no scores for Reddit (FR-1.17). Zero Wire shows its action label.
  - *Related:* stories that share a CVE are grouped under a "Related: CVE-…" disclosure.
- **Risk count bar:** five segments sized by count, each labelled with its number and word.
- **Radar panel:** lists of outages, attack trends, and BGP events. Each one has a time and a link.
- **Admin warning:** a warning-container banner that names the failing source and how long it has been failing (FR-8.7).
- **Empty state:** "No new stories at or above Medium since 07:00 yesterday. Change your minimum risk in Alert settings."
- **Alert settings form:** time, time zone, days, channels, minimum risk, and an on/off switch shown as a labelled checkbox. Phone numbers show a "Verify number" step. A saved Slack webhook shows as "Slack webhook saved" with a "Replace" action.

- **Email alert:** a single column up to 600 px wide, using these colour tokens and risk chips with the risk word. It uses system fonts only, because email clients don't load self-hosted fonts reliably. It contains no images and no scripts, and it always includes a plain-text part. *(delegated decision)*

### Security-relevant interactions

- **Signed-in state:** the ink account bar is always present after sign-in. It shows the account email, a role label ("Admin" or "User"), and a "Sign out" button. Admin-only navigation renders only for admins. Pages that need setup (first-login TOTP, FR-6.15) hide all other navigation until setup is done. ASSUMPTION: a dialog warns two minutes before the 30-minute idle sign-out (FR-6.10), with "Stay signed in".
- **Destructive and privileged actions:** deleting an account, removing or enabling a source, changing a role, and disabling a category open a dialog. The dialog names the target and its consequence, for example "Delete jo@example.org? Their email, phone number, and Slack webhook are deleted. This can't be undone." Account deletion requires typing the account email. The destructive button never has default focus. "Cancel" does. Impossible actions are disabled with the reason shown, for example "This is the last active admin" (FR-9.3). Enabling a source without a licence record is disabled with "Add a licence record first" (FR-8.3).
- **What errors may reveal:**
  - *Sign-in:* every failure shows one message: "Email, password, or code is incorrect." (FR-6.8). Password reset always says "If that address has an account, we sent a link."
  - *All errors:* never show stack traces, internal IDs, source credentials, saved webhook addresses (NFR-3.3), or whether another user exists.
  - *Lockout:* a locked account shows the same single sign-in error, so lockout never confirms that an account exists. *(delegated decision)*
- **User-supplied and collected content:** all story text, source names, category names, and Reddit titles render as plain text, never as markup (NFR-3.4). Links to original items show their destination domain in visible text beside the title. Reddit titles are shown unchanged (FR-1.17). Long unbroken strings wrap so they cannot push the layout off screen.

## Do's and Don'ts

- Do show risk as a word, a colour, and a spine width together.
- Do keep the indigo primary for actions and links only.
- Do put the required notices and credits (FR-8.10, FR-8.11) in every dashboard footer.
- Don't show government logos or seals, or suggest any source endorses the service (FR-8.13).
- Don't use cards, shadows, or gradients for stories. Use the ledger.
- Don't use all-caps labels, middle-dot metadata strings, or arrow-suffixed links.
- Don't use dawn amber for text or controls.
- Don't show a summary, category, or score on a Reddit item.

## Open Questions

None. DQ-1 to DQ-5 were resolved by delegated decision (owner instruction to answer all open questions). They are recorded above and marked *(delegated decision)*.

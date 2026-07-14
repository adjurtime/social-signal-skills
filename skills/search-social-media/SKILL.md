---
name: search-social-media
description: >-
  Search, compare, and assess timely public information on weakly indexed social
  platforms such as Xiaohongshu, X, Weibo, Reddit, LinkedIn, Zhihu, Bilibili,
  and YouTube. Automatically classify natural-language requests into one or more
  of four basic questions: facts and changes, experience and evaluation, methods
  and solutions, or opinions and trends. Use for recent social signals,
  firsthand reports, user reactions, troubleshooting, rumors, and cross-platform
  comparison. Exclude private or unauthorized content and do not post or
  interact with content.
---

# Search Social Media

## Core contract

Use this skill as a lightweight cross-platform retrieval and evidence layer. Search public or account-authorized platform-native content that ordinary web search may not index well.

Do not require the user or a calling skill to choose a search category. Infer the question, search it, filter low-value content, compare platforms, and return a compact evidence packet. Let downstream skills perform domain planning, recommendations, monitoring, scheduling, or delivery.

Treat social posts as signals, not automatically as facts. Separate discovery, testimony, opinion, and verification.

## Classify the basic question

Assign one primary mode and any useful secondary modes. Do not force a request into only one mode.

### 1. Facts and changes

Answer: What happened? What changed? What is the current state?

Prioritize in this order:

1. verification and original-source proximity;
2. event time and current validity;
3. independent corroboration;
4. relevance;
5. engagement only as a discovery tie-breaker.

Search exact names, dates, announcements, observed rollout, corrections, reversals, and counterclaims.

### 2. Experience and evaluation

Answer: What is it actually like? What worked, failed, or caused friction?

Prioritize in this order:

1. commercial independence and credible firsthand context;
2. match to the situation being asked about;
3. concrete details, trade-offs, and negative as well as positive evidence;
4. diversity across authors, times, and platforms;
5. freshness when the experience can change.

Search lived-experience language, complaints, limitations, comparisons, and counterexamples. Apply the commercial-content filter strictly.

### 3. Methods and solutions

Answer: How can it be done, reproduced, or fixed?

Prioritize in this order:

1. reproducible steps or direct demonstration;
2. version, device, region, and configuration match;
3. relevant expertise or repeated successful use;
4. independent confirmation;
5. freshness for version-sensitive procedures.

Search exact errors, versions, settings, workarounds, failure conditions, and reports that a proposed fix did not work.

### 4. Opinions and trends

Answer: What do relevant communities think, and how is the discussion moving?

Prioritize in this order:

1. audience and community relevance;
2. diversity and independence of viewpoints;
3. identifiable incentives and authentic participation;
4. change over time;
5. engagement only as a signal of visibility.

Separate sentiment from factual claims. Do not convert a loud or coordinated group into a population-level conclusion.

### Combine modes

Use a primary mode to control ranking and secondary modes to add evidence rather than averaging all criteria.

Example: `Did Codex change its usage-limit reset behavior, and how are users reacting?` uses **facts and changes** as the primary mode and **opinions and trends** as the secondary mode. Verify the change before summarizing reactions.

## Infer cross-cutting conditions

Infer these conditions from natural language; ask only when ambiguity would materially change the work:

- **time:** live, recent delta, or stable baseline;
- **scope:** location, language, audience, product version, or community;
- **source preference:** ordinary users, local observers, professionals, direct subjects, or official accounts;
- **verification intensity:** normal, disputed, or high-stakes;
- **depth:** quick scan or bounded deep search.

For a stable baseline, look for experiences or explanations repeated across a longer period. For a recent delta, use a clear cutoff and report when an item is likely to expire. When both matter, report `Stable baseline` and `Recent changes` separately.

Use these default time windows only as starting points:

- breaking events: 6–24 hours;
- active product, company, platform, or public-event changes: 7–30 days;
- user experience and troubleshooting: 3–12 months;
- background opinion: no strict limit, while preferring material still relevant now.

## Choose platforms and access tools

Read [references/platforms.md](references/platforms.md) before selecting platforms or applying platform-specific queries.

Start with two complementary platforms. Add a third or fourth only when it contributes a different audience, language, geography, or evidence type. Assign each platform a role: discovery, original-source tracing, independent corroboration, firsthand observation, or community reaction.

Choose the safest capable access method in this order:

1. use a trusted, purpose-built platform connector or MCP tool when it exposes the required public content through a documented, authorized interface;
2. use controlled Chrome with the user's existing logged-in session for platform-native results that require account state;
3. use an in-app or ordinary browser for public pages that do not depend on the user's Chrome session;
4. use Computer Use only when structured browser or connector controls cannot operate the necessary visible interface;
5. use ordinary web search for discovery or coverage gaps, not as a substitute for native search when native results materially differ.

For each selected platform, verify the first candidate access method with the smallest useful read-only probe. Treat an access path as available only when it returns the platform-native result or content needed for the task; a configured connector, installed command, or visible login is not enough by itself.

Classify the live access state as `available`, `authorization required`, `constrained`, or `unavailable`, and keep one active access path per platform for the current task. On an ordinary transient failure, retry once; if it still fails, move to the next already available and user-authorized method in the order above. Do not invent commands, install packages or connectors, add browser extensions, or request exported credentials as part of a search. Report a material access gap and ask separately before any setup work.

Treat MCP as an access interface, not a credibility signal. An unofficial MCP that wraps fragile private endpoints or browser automation may be less stable and riskier than controlled Chrome. Do not add a connector merely because it is called MCP.

Prefer visible, user-authorized access. Do not use hidden private APIs, CAPTCHA bypasses, anti-detection browsers, proxy pools, or extracted session credentials.

## Build queries

Generate at most three query bundles per platform:

1. **Exact:** formal entity, event, claim, version, date, or place.
2. **Expansion:** aliases, abbreviations, colloquial terms, symptoms, local-language equivalents, and community jargon.
3. **Counter:** correction, denial, failure, counterexample, negative experience, source, or reproduction terms.

Adapt the bundles to the primary mode. Do not run all bundles when the exact query already produces diverse, relevant evidence. Stop when additional variants or scrolling mostly repeat existing claims.

Example for `Did Codex change its usage-limit reset behavior?`:

- exact: `Codex usage limit reset change`;
- expansion: `Codex quota reset rolling window usage cap`;
- counter: `Codex reset unchanged reverted official clarification`.

## Filter commercial and inauthentic content

Apply this filter before ranking evidence on every platform.

### Exclude from organic evidence

- explicit advertisements, affiliate links, discount codes, booking or purchase calls to action;
- vendor, agency, or brand posts presented as independent user recommendations;
- copied promotional text or coordinated campaigns with no independent evidence;
- obvious bot spam, mass-generated posts, or engagement bait that adds no substantive information.

Use a commercial post only for the organization's own stated offer or position, and label it accordingly.

### Down-rank and seek corroboration

- repeated praise of one provider with no limitations or alternatives;
- templated listicles with generic completeness but no dates, sequence, mistakes, measurements, or verifiable context;
- suspiciously identical structure, wording, images, or recommendations across accounts;
- polished causal claims unsupported by documents, tests, or firsthand detail;
- posts whose author relationship to the promoted subject is unclear.

Do not label a post as AI-generated from prose style alone. Classify commercial or automated-content risk as `low`, `medium`, or `high` from incentives, provenance, specificity, duplication, and behavior together. Exclude high-risk items from conclusions; use medium-risk items only when independently corroborated.

Report only the number and main reasons for filtered items unless the user asks to inspect them.

## Execute and capture

For each selected platform:

1. run the smallest useful query set;
2. compare recent and relevant or popular views when both matter;
3. collect 5–15 strong candidates and stop before 20 unless deep search was requested;
4. open enough candidates to judge provenance, evidence, context, and commercial risk;
5. preserve meaningful disagreement and failed solutions.

Capture when visible:

- active access path, live access state, and material access limitation;
- platform, title or atomic claim, account, and identifiable role;
- post time, described event time, and discovery time;
- direct URL and visible engagement;
- evidence or firsthand context offered;
- commercial or automated-content risk.

Do not infer missing dates, identities, or engagement values.

## Normalize and assess

- Split bundled posts into atomic claims.
- Merge duplicate URLs, copied screenshots, and obvious cross-posts.
- Count a repost or coordinated cluster as one source unless a member adds independent evidence.
- Trace claims to the earliest visible or primary source.
- Preserve conflicts rather than averaging them away.

Label source identity separately:

- official institution or direct subject;
- identifiable firsthand participant;
- relevant professional;
- ordinary user;
- anonymous or unverifiable account.

Label evidence status separately:

- **Verified:** traceable to a primary statement, document, or direct evidence.
- **Corroborated:** supported by at least two independent sources with consistent details.
- **Plausible single source:** credible access or firsthand context without independent support.
- **Unverified:** anonymous, second-hand, screenshot-only, unsupported, or commercially compromised.
- **Contradicted:** conflicts with a reliable correction, primary source, or stronger evidence.

For releases, policies, benefits, or future events, also label the state:

- **Announced**;
- **Rolling out**;
- **User-observed**;
- **Broadly confirmed**;
- **Corrected or reversed**.

A newer repost is not new evidence. An older primary source may outrank a newer rumor. Do not upgrade an announcement to completion because many accounts repeat it.

For medical, legal, financial, safety, entry-rule, or other high-stakes claims, use social media for discovery and lived experience only. Require authoritative verification before presenting rules or recommendations as reliable.

## Return a social evidence packet

Return the smallest structure that preserves provenance:

1. **Answer:** strongest current conclusion and uncertainty.
2. **Stable baseline and recent changes:** include both only when the question needs both.
3. **Strongest signals:** atomic claim, platform, source, time, evidence status, and direct link.
4. **Consensus, disagreement, and failed counterexamples.**
5. **Unverified or filtered-content note:** material rumors plus the count and main reasons for excluded commercial or automated items.
6. **Coverage:** platforms and roles, active access paths and states, time window, query families, and meaningful gaps.

For a quick search, compress these sections. Paraphrase unless exact wording is essential. Never invent quotations, inaccessible content, or population-level conclusions from an unrepresentative sample.

Do not turn the evidence packet into a domain plan. A travel, purchasing, technical-support, or research skill may call this skill and combine its output with official sources, user constraints, and domain reasoning.

## Preserve read-only safety

- Do not like, repost, comment, follow, message, publish, or modify account state.
- Do not inspect or export cookies, passwords, local storage, or session tokens.
- Do not access private messages, closed groups, paid communities, friends-only posts, or leaked personal information.
- Search platforms sequentially and keep each pass bounded.
- Stop on CAPTCHA, risk-control warnings, forced verification, or unexpected login challenges. Ask the user to complete supported login or verification manually.

## Support downstream reuse

When a caller supplies a previous-search time, baseline URLs, or prior claims, return only material additions, corrections, and changes while still reporting coverage.

Include direct URLs and search time so a separate workflow can monitor changes. Do not create schedules, persist monitoring state, or send email unless the user explicitly requests those separate actions.

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

Use this skill as a bounded, read-only evidence layer for public or account-authorized social content that general web search may index poorly. Return traceable signals and uncertainty; leave domain recommendations, monitoring, publishing, and account actions to their owning workflows.

## Evidence contract

- A social post can establish that a named source said or experienced something; it does not automatically establish that the underlying claim is true.
- Separate discovery, firsthand testimony, professional interpretation, public opinion, and authoritative verification.
- Never infer missing identity, date, location, engagement, authorship, or access from context alone.
- Preserve disagreement and failed solutions; do not average conflicting claims into false consensus.
- Do not call prose “AI-generated” from style alone. Assess low-integrity or commercial risk from provenance, incentives, duplication, specificity, and behavior together.
- For medical, legal, financial, safety, travel-entry, or other high-stakes rules, use social media for discovery and lived experience only. Verify material rules with the controlling authority before treating them as reliable.

## 1. Interpret the request

Assign one primary question and any useful secondary question:

1. **Facts and changes:** what happened, when, and whether it is still current.
2. **Experience and evaluation:** what identifiable users experienced, including conditions and limitations.
3. **Methods and solutions:** which steps were attempted, in what environment, with what outcome.
4. **Opinions and trends:** which narratives or reactions appear in a defined community and time window.

Infer time window, geography/language, named entities, desired depth, and verification intensity. Ask only when ambiguity would materially change the search target or evidence standard. If “latest,” “recent,” or an unstable current state is requested, record the search time and use current retrieval.

## 2. Select sources by role

Read `references/platforms.md` when platform choice or access behavior is uncertain.

Choose the smallest complementary set that can answer the question. Prefer diversity of role over platform count—for example, a primary-source account plus a user community, or a specialist forum plus a broad discussion platform. Do not claim cross-platform consensus from two platforms that recycle the same source.

For each source, record its role:

- primary or direct subject;
- identifiable firsthand participant;
- relevant professional or specialist;
- ordinary user or community discussion;
- anonymous or unverifiable account.

## 3. Probe access before searching deeply

Use one small read-only probe per selected platform and record the live state: accessible, login required, blocked, partial, or unavailable.

Access order:

1. purpose-built connector or platform skill;
2. the user's existing authorized Chrome session;
3. in-app browser or controlled browser;
4. computer-use only when structured browser access cannot complete a necessary read-only step;
5. public web discovery as a fallback, clearly labeled when it cannot expose platform-native context.

Do not install extensions or dependencies, export cookies/tokens, bypass CAPTCHA or risk controls, or ask for passwords. When login is needed, ask the user to complete it manually. Stop on unexpected verification, account warnings, or private-content boundaries.

## 4. Build bounded query families

Start with the smallest useful set:

- **Exact:** names, handles, product/version, quoted error, event, and date.
- **Expansion:** aliases, translations, local terminology, symptoms, or related mechanism.
- **Counter:** correction, rollback, failure, unchanged state, opposing experience, or official clarification.

Use up to three query families as a default, not a quota. Stop earlier when new results repeat known sources and claims; expand only when an evidence gap could change the answer. For deep-search requests, state the expanded scope before continuing.

## 5. Capture evidence, not screenshots of impressions

Open enough candidates to judge provenance and context. Candidate counts are heuristics; stop by coverage and saturation rather than scroll length.

Capture when visible:

- atomic claim and the source's role;
- platform, account, direct URL, and stable identifier if available;
- post time, described event time, and discovery time as separate fields;
- firsthand details, documents, tests, screenshots, or reproducible steps offered;
- environment, version, geography, sample, or other conditions;
- visible engagement only as an attention signal;
- commercial, automation, or coordination risk.

Paraphrase by default. Quote only when exact wording is material and keep the excerpt short.

## 6. Filter and normalize

Exclude from organic evidence:

- explicit ads, affiliate links, discount codes, purchase calls, or undisclosed vendor material;
- copied promotion, obvious spam, engagement bait, and coordinated duplicates with no independent evidence;
- content whose only support is another unattributed screenshot or repost.

A brand or organization post may support what that organization officially stated, but not independent evaluation of its own offer.

Down-rank claims with unclear incentives, generic praise, no conditions, copied structure, unsupported causal stories, or hidden author relationships. Label risk `low`, `medium`, or `high`; use high-risk items only to document that a claim circulates, not that it is true.

Then:

- split bundled posts into atomic claims;
- merge duplicate URLs, cross-posts, copied screenshots, and coordinated clusters;
- trace reposted claims to the earliest visible or primary source;
- count independent evidence, not account count;
- preserve counterexamples and corrections.

## 7. Assess each claim

Keep source identity separate from evidence status:

- **Verified:** matched to the appropriate primary statement, document, or directly inspectable evidence.
- **Corroborated:** consistent detail from at least two genuinely independent sources.
- **Plausible single source:** credible firsthand access or specialist context without independent support.
- **Unverified:** anonymous, second-hand, screenshot-only, unsupported, inaccessible, or commercially compromised.
- **Contradicted:** conflicts with a stronger primary source, correction, or better evidence.

For releases, policies, benefits, and future events, also distinguish `announced`, `rolling out`, `user-observed`, `broadly confirmed`, and `corrected/reversed`. A newer repost is not newer evidence, and repetition does not turn an announcement into completed rollout.

## 8. Return a compact evidence packet

Lead with the answer and uncertainty, then include only the sections needed:

1. **Current conclusion:** what the evidence supports now and what remains uncertain.
2. **Strongest signals:** atomic claim, source role, platform, relevant times, evidence status, and direct link.
3. **Agreement and disagreement:** independent convergence, material counterexamples, and failed solutions.
4. **Unverified/filtered note:** important rumors plus the count and main reasons for excluded or down-ranked items.
5. **Coverage:** platforms, roles, access state, time window, query families, search time, and meaningful gaps.

Do not generalize to a population without a defined sampling method. Do not invent inaccessible quotations or represent a thin convenience sample as “the internet thinks.”

## Read-only safety and stopping rules

- Do not like, repost, comment, follow, message, publish, save, or modify account state.
- Do not inspect private messages, closed groups, paid communities, friends-only posts, or leaked personal data.
- Do not expose cookies, session tokens, credentials, or private account identifiers in notes or output.
- Stop when the core claim has appropriate verification and further results are duplicates; when selected sources are inaccessible and fallbacks cannot answer; or when risk controls require user action.
- If a prior search cutoff, URLs, or claim list is supplied, return material additions, corrections, and changes rather than repeating the full baseline.

Include direct URLs and search time so another workflow can reuse the evidence. Do not create schedules, alerts, or persistent monitoring unless the user separately requests them.

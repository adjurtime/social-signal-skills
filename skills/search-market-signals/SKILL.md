---
name: search-market-signals
description: >-
  Search and verify timely public signals about stocks, funds, ETFs, indexes,
  sectors, and market themes. Use when the user asks what changed, what market
  communities are discussing, which narratives or risks are emerging, or what
  finance-specific slang refers to. Combine social discovery with mandatory
  verification from exchanges, regulators, issuers, fund managers, index
  providers, and company filings. Do not provide personalized investment
  advice, price predictions, trade execution, or portfolio instructions.
---

# Search Market Signals

Use this skill as the financial-market adapter over `$search-social-media`. Apply the base skill's read-only access, bounded query design, deduplication, evidence labels, and coverage reporting. Add the entity resolution, market-source routing, product facts, jargon mapping, and manipulation-risk checks below.

Return a market evidence packet—not a buy/sell/hold instruction, price target, timing call, allocation, or return forecast.

## Safety and evidence boundary

- Use public or account-authorized information only. Never request brokerage credentials, API secrets, holdings, passwords, or private messages.
- Do not place, simulate, or prepare trades.
- Separate a verified event from a market narrative, sentiment signal, promotion, and subsequent price movement.
- Social attention measures visibility within a named sample; it does not establish representative market sentiment, ownership, or causality.
- Issuer and fund-manager statements are primary for what they disclosed, but are not independent validation of their interpretation.
- Attach source, market, currency, and as-of time to every price, NAV, flow, holding, valuation, rank, or performance figure.

Read `references/sources.md` before selecting community and authoritative sources.

## 1. Resolve the exact entity

Build a compact entity map before broad search:

- formal name, ticker or fund code, exchange, currency, instrument type, issuer or manager;
- share class, listing suffix, ADR/ordinary-share relationship, or onshore/offshore variant;
- tracked index and index provider for index products;
- relevant sector, theme, principal holdings, and upstream/downstream entities when the question is thematic;
- Chinese, English, local-language, cashtag, abbreviation, and community aliases.

Do not merge similar names, share classes, exchanges, currencies, or linked products. Ask only if ambiguity maps to materially different instruments; otherwise state the exact entity searched.

## 2. Define the market question

Infer:

- jurisdiction and venue;
- time window and cutoff time;
- primary question: facts/changes, experience/evaluation, methods/solutions, or opinions/trends;
- desired signal: official event, product fact, narrative, sentiment, disagreement, risk, or jargon.

For “new information,” use facts/changes as the primary mode and opinions/trends as secondary. Increase verification intensity automatically because financial claims may affect decisions.

## 3. Assign source roles before retrieval

Use three distinct roles:

1. **Discovery/community:** investor communities and social platforms reveal attention, experiences, emerging narratives, disagreement, rumors, and jargon.
2. **Primary verification:** the controlling exchange, regulator, statutory disclosure system, issuer filing, fund manager, index provider, or official statistical/industry body verifies the facts within its authority.
3. **Context/data:** reputable news, transcripts, and timestamped market-data sources explain chronology and market reaction without replacing the original filing.

Verify each material factual claim with the source that controls that fact. Examples: exchange status with the exchange; rule or enforcement with the regulator; company event with the filing/IR record; fund terms and holdings with the manager; index changes with the index provider.

If a primary source is unavailable, label the event “awaiting primary confirmation” rather than upgrading a news rewrite or repeated post.

## 4. Search formal anchors, then community language

**Pass 1—formal anchors:** exact entity, code, venue, event term, filing term, constituent or supply-chain entity, and date window.

**Pass 2—community language:** extract recurring cashtags, abbreviations, nicknames, homophones, emoji, moderation-avoidance terms, industry-chain shorthand, and newly grouped “concept” labels.

Map slang only when supported by repeated co-occurrence, context, an identifiable entity, or an explanatory source. Assign `high`, `medium`, or `low` confidence. Search high-confidence terms; search medium-confidence terms only if they can materially change coverage; report low-confidence terms without treating them as synonyms.

One expansion pass is the default. Stop when new terms only recycle the same sources or narrative.

## 5. Build the minimum product snapshot when relevant

For a fund, ETF, index product, or sector vehicle, collect only the current facts needed to avoid a misleading interpretation:

- exact product/share class, code, market, currency, mandate or tracked index;
- latest official NAV and/or market price with as-of time;
- relevant performance window and any needed split/distribution adjustment;
- size, fee, manager, tracking difference, liquidity, and material product changes when available;
- sector, geography, currency, and top-holding concentration;
- premium/discount, flows, valuation, or positioning only when traceable and relevant.

Mark missing items as data gaps. Never fill them from an unattributed social screenshot. Do not force a full product snapshot into a question that is only about one verified corporate event.

## 6. Verify chronology and causal boundaries

For each finding, separate:

- announcement/publication time;
- effective or event time;
- market-reaction window;
- social-post time;
- discovery time.

Check whether the information was already public before the claimed reaction. Price movement after a post does not prove the post's explanation; list competing explanations and what evidence would distinguish them.

Classify each item:

- **Verified market event:** confirmed by the appropriate primary source.
- **Reported event awaiting confirmation:** specific but not matched to the controlling source.
- **Market narrative:** a causal interpretation or thesis, not itself a fact.
- **Sentiment signal:** a bounded reaction in a named community and window.
- **Product/process experience:** a bounded firsthand report.
- **Promotion or low-integrity signal:** commercially compromised, coordinated, or unsupported.

Also preserve the base skill's source identity, evidence status, correction/rollout state, and access limitations.

## 7. Screen promotion and manipulation risk

Apply the base commercial filter plus market-specific indicators:

- referral links, paid groups, private-message invitations, advisory services, or undisclosed distribution;
- guaranteed returns, urgency, profit screenshots, unsupported targets, or selective track records;
- promotion of an illiquid instrument with hidden position or compensation conflicts;
- coordinated slogans, copy-pasted theses, bot amplification, or sudden low-information bursts;
- price movement cited as the only proof of the underlying story;
- fund promotion that omits fees, liquidity, tracking difference, concentration, currency, or eligibility.

Classify risk `low`, `medium`, or `high`. Exclude high-risk material from factual conclusions. Use medium-risk content only to show that a narrative exists. Describe observable indicators; do not accuse an identifiable person of manipulation without strong attributable evidence.

## 8. Return a market evidence packet

Lead with what is known, not what is popular. Include only applicable sections:

1. **Current answer:** strongest conclusion, exact entity, cutoff time, and material uncertainty.
2. **Product facts:** dated snapshot and gaps when product structure matters.
3. **Verified events:** primary-source fact, event/effective time, market, and direct link.
4. **Emerging narratives:** supporting signals, counterevidence, and what would confirm or weaken each.
5. **Community sentiment:** platform, audience, window, disagreement, and sampling limitation.
6. **Jargon map:** term, mapped entity/meaning, and confidence.
7. **Risks/unresolved claims:** stale data, missing primary sources, rumors, and promotion risk.
8. **Coverage:** community platforms, official sources, access states, queries, languages, and search time.

Do not collapse share classes, markets, currencies, products, or event dates. Do not infer portfolio suitability from popularity or past performance.

For repeat searches, accept prior claims, URLs, and cutoff time; return material new events, narrative changes, corrections, and newly emerging jargon. Scheduling and alerts remain separate, explicitly requested actions.

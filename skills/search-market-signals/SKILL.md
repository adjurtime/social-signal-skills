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

## Core contract

Use this skill as a financial-market adapter over `$search-social-media`.

Apply `$search-social-media` for the four basic questions, cross-platform retrieval, deduplication, commercial-content filtering, credibility labels, browser access, and read-only safety. Add only the market-specific entity mapping, source routing, jargon discovery, verification, and output rules below.

Return a market evidence packet, not a buy, sell, hold, timing, allocation, or return forecast. Separate verified events from narratives, sentiment, and promotion.

Use public or account-authorized information only. Never request account passwords, trading credentials, API secrets, holdings, or brokerage access. If a source requires login, ask the user to log in manually in Chrome. Do not place or simulate trades.

Read [references/sources.md](references/sources.md) before choosing platforms and authoritative sources.

## Interpret the request

Infer the following unless ambiguity would materially change the search:

- instrument or theme: stock, fund, ETF, index, sector, commodity-linked theme, or market-wide event;
- market and venue: mainland China, Hong Kong, United States, or another jurisdiction;
- time window: intraday, recent days, recent weeks, or longer baseline;
- primary question: facts and changes, experience and evaluation, methods and solutions, or opinions and trends;
- desired signal: official event, emerging narrative, sentiment, disagreement, risk, or jargon.

For ordinary requests about `new information`, use **facts and changes** as the primary mode and **opinions and trends** as the secondary mode. Increase verification intensity automatically because financial claims can affect decisions.

Ask for clarification only when a name or code maps to multiple materially different instruments or markets.

## Resolve the market entity

Build an entity map before broad social search:

- formal name and common names;
- ticker, fund code, exchange, and currency when relevant;
- instrument type and issuer or fund manager;
- tracked index and index provider for index funds or ETFs;
- sector, theme, principal holdings, and upstream or downstream entities when the question concerns a market narrative;
- English, Chinese, local-language, and community aliases.

Do not assume that similar names, share classes, exchange suffixes, or linked products are interchangeable. Record the exact instrument used in the search.

## Use a two-pass jargon search

### Pass 1: formal anchors

Search the verified entity names, codes, sector terms, constituent names, official event terms, and date window. Collect a small set of current, diverse results.

### Pass 2: community language

Extract recurring:

- abbreviations, cashtags, nicknames, homophones, emoji, and deliberate substitutions;
- industry-chain shorthand and newly grouped `concept` names;
- phrases describing rallies, drawdowns, crowding, rotation, fear, or enthusiasm;
- coded references used to avoid moderation or direct promotion rules.

Map a term only when its meaning is supported by context, repeated co-occurrence, identifiable entities, or an explanatory source. Assign `high`, `medium`, or `low` mapping confidence. Search high-confidence terms; search medium-confidence terms only when they could materially change coverage. Report low-confidence terms without treating them as synonyms.

Limit expansion to one additional pass unless the user asks for a deep search. Do not let slang discovery create unbounded queries.

## Separate source roles

Use three roles rather than treating every website as equivalent.

### 1. Discovery and community interpretation

Use investor communities and general social platforms to discover:

- emerging themes and causal stories;
- user-observed effects and practical product issues;
- sentiment, disagreement, and attention shifts;
- rumors, misunderstood announcements, and new jargon.

These sources show what is being discussed, not necessarily what is true.

### 2. Primary verification

Verify material factual claims against the source with the relevant authority:

- exchange and statutory disclosure platforms for listings, filings, trading status, inquiries, disciplinary actions, and exchange-traded fund notices;
- regulators for rules, enforcement, approvals, and investor warnings;
- company filings and investor-relations pages for company events;
- fund managers for prospectuses, periodic reports, holdings, fees, distributions, and product changes;
- index providers for methodology, constituents, rebalances, and classification;
- official statistical or industry bodies for macro and sector data.

Exchange announcements are mandatory for exchange-governed events, but they are not a complete source for every catalyst. Policy changes, industry data, commodity events, overseas developments, and community narratives may originate elsewhere.

### 3. Context and market data

Use reputable news, transcripts, and timestamped market-data sources to explain context. Do not substitute a news rewrite for the original filing when the original is available.

Attach timestamps and market venue to prices, flows, holdings, valuations, and rankings. Treat figures copied into social posts as unverified until matched to a traceable data source.

## Build a fund or product facts snapshot

Before evaluating a fund, ETF, index product, or sector vehicle, collect the smallest current snapshot that can prevent a misleading conclusion:

- exact product, share class, code, market, currency, and tracked index or mandate;
- latest official NAV or market price with its as-of date;
- recent performance over relevant windows and, when available, drawdown or volatility;
- fund size, fees, manager or tracking difference, and material product changes;
- sector, geography, currency, and top-holding concentration;
- premium or discount, liquidity, distributions, splits, or other technical adjustments when applicable;
- valuation, flows, or positioning only when the source and timestamp are traceable.

Mark unavailable items as gaps. Do not fill them with figures copied from social posts. A downstream portfolio review should know both what the market is discussing and what product the user actually owns.

## Route the search by question

### Facts and changes

Search the authoritative source and social discussion in parallel. Rank:

1. primary filing, exchange, regulator, issuer, or fund-manager statement;
2. event time and current validity;
3. independent reporting or direct observation;
4. community interpretation;
5. engagement only as visibility.

### Experience and evaluation

Use for fund-platform usability, subscription or redemption friction, tracking experience, disclosure accessibility, or other lived product experience. Filter referral promotion and sponsored recommendations strictly. Do not generalize one investor's return or tax situation.

### Methods and solutions

Use for locating a disclosure, interpreting a product mechanism, reproducing a public calculation, or resolving a platform-data mismatch. Prefer official definitions, versioned methodology, and reproducible steps. Do not turn procedural explanation into a trading instruction.

### Opinions and trends

Sample different communities, languages, time points, and opposing views. Separate:

- attention from conviction;
- sentiment from holdings;
- narrative popularity from factual confirmation;
- repeated promotion from independent agreement.

Do not claim representative market sentiment without a defined sample and method.

## Detect promotion and manipulation risk

Apply the base commercial-content filter plus these market-specific warnings:

- referral links, paid groups, private-message invitations, courses, advisory services, or undisclosed product distribution;
- guaranteed returns, urgency, screenshots of profits, unsupported target prices, or selective track records;
- accounts promoting an illiquid instrument while hiding position or compensation conflicts;
- coordinated slogans, copy-pasted theses, bot amplification, or sudden low-information posting bursts;
- commentary that cites only price movement as proof of the underlying story;
- fund or ETF promotion that ignores fees, liquidity, tracking difference, concentration, currency, or eligibility.

Classify promotion or manipulation risk as `low`, `medium`, or `high`. Exclude high-risk material from conclusions. Use medium-risk content only to document that a narrative exists, not to support the narrative's truth.

Do not accuse an identifiable person of manipulation without strong, attributable evidence. Describe observable indicators and uncertainty.

## Classify each finding

Assign one content class before synthesis:

- **Verified market event:** confirmed by the appropriate primary source.
- **Reported event awaiting confirmation:** specific and relevant but not yet matched to a primary source.
- **Market narrative:** a causal interpretation or thesis that may explain attention but is not itself a fact.
- **Sentiment signal:** an observed reaction within a named platform or community.
- **Product or process experience:** a bounded firsthand report.
- **Promotion or low-integrity signal:** commercially compromised, coordinated, or unsupported.

Also preserve the base skill's source identity, evidence status, event time, and rollout or correction state.

## Return a market evidence packet

Lead with what is known, not with what is popular:

1. **Current answer:** strongest conclusion and material uncertainty.
2. **Product facts:** exact product, dated NAV or price, structure, concentration, fees, and material data gaps when applicable.
3. **Verified events:** primary-source fact, event time, market, and direct link.
4. **Emerging narratives:** supporting signals, counterarguments, and what would confirm or weaken each narrative.
5. **Community sentiment:** platform, audience, time window, disagreement, and sampling limitation.
6. **Jargon map:** term, likely meaning, mapped entity, and confidence.
7. **Risks and unresolved claims:** rumors, stale information, missing disclosures, and promotion risk.
8. **Coverage:** platforms, official sources, query families, time window, and inaccessible sources.

Keep the packet concise. Do not collapse multiple share classes, markets, products, or event dates into one claim. Do not infer portfolio suitability from popularity or past performance.

## Support downstream use

A separate investment-research or portfolio skill may combine this packet with objectives, risk tolerance, valuation, diversification, liquidity, tax, and scenario analysis. Keep those decisions outside this search skill.

For repeat searches, accept prior claims, URLs, and a cutoff time. Return material new events, narrative changes, corrections, and newly emerging jargon. Do not create monitoring schedules or send alerts unless the user explicitly requests those separate actions.

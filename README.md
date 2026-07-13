# Social Signal Skills

A small set of Codex skills for retrieving public social-media information, evaluating market signals, and maintaining a read-only fund portfolio record.

## Skills

- `search-social-media`: Search public content across platforms such as Xiaohongshu, X, and Zhihu. It selects a search strategy by the user's underlying question, filters commercial or synthetic-looking content, and separates observation from verification.
- `search-market-signals`: Adds market entities, jargon discovery, official-source checks, time sensitivity, and evidence weighting on top of `search-social-media`.
- `track-fund-portfolio`: Records holdings and fund operations, reconciles confirmed transactions, and uses `search-market-signals` only when external signals could materially affect a portfolio conclusion.

Install all three because they form a dependency chain:

`search-social-media` → `search-market-signals` → `track-fund-portfolio`

## Safety boundary

These skills read public information and portfolio records. They do not place orders, modify brokerage or payment accounts, or treat social-media posts as verified facts. Market outputs are research support, not guaranteed investment advice.

## License

MIT

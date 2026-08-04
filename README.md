# Synthetix

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Synthetix is a derivatives liquidity protocol providing perpetual futures trading on Ethereum and EVM-compatible L2 networks including Optimism and Base. The platform offers REST and WebSocket APIs for trading operations, market data, account management, collateral tracking, and analytics.

## APIs

| API | Base URL | Auth |
|-----|----------|------|
| Info API (Public) | `https://papi.synthetix.io/v1/info` | None |
| Trade API (Authenticated) | `https://papi.synthetix.io/v1/trade` | EIP-712 |
| WebSocket Info | `wss://papi.synthetix.io/v1/ws/info` | None |
| WebSocket Trade | `wss://papi.synthetix.io/v1/ws/trade` | EIP-712 |

## Key Capabilities

- Market data: prices, candles, funding rates, orderbook depth, contract specs
- Trading: place/modify/cancel orders (market, limit, stop-loss, take-profit, TWAP, GTD)
- Account management: subaccounts, delegation, collateral deposits/withdrawals
- Analytics: position history, PnL, trade history, balance updates
- Real-time: WebSocket subscriptions for prices, orderbook, and account events

## Authentication

All trading actions use EIP-712 cryptographic signatures — no API keys required. Public market data endpoints require no authentication. First deposit to the deposit contract auto-creates a master account.

- Deposit Contract (Mainnet): `0xD62595c3c23B690BAEE0935e107A209Cb1Dbd37B`
- Auth Docs: https://developers.synthetix.io/developer-resources/api/authentication

## Rate Limits

Token bucket model with 10-second rolling windows:

- Per-IP: 10,000 tokens / 10s (all connections from same IP)
- Per-subaccount: 1,000–5,000 tokens / 10s (scales with fee tier)
- HTTP 429 on limit exceeded; implement exponential backoff

## Fees

Volume-based tiered trading fees (no API subscription cost):

- Regular User: 0.020% maker / 0.050% taker
- Tier 7 ($5B+ 14d volume): 0.000% maker / 0.017% taker
- Tiers update automatically based on 14-day rolling notional volume

## Resources

- Developer Docs: https://developers.synthetix.io/
- Protocol Docs: https://docs.synthetix.io/
- GitHub: https://github.com/Synthetixio
- Python SDK: https://synthetixio.github.io/python-sdk/
- Discord: https://discord.gg/synthetix

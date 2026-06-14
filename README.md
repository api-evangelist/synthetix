# Synthetix

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

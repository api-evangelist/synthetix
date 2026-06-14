# Synthetix GraphQL API

## Description

Synthetix exposes GraphQL APIs via The Graph protocol, providing indexed blockchain data for the Synthetix V3 derivatives liquidity protocol. Subgraphs are available for the core protocol (pools, collateral, positions, vaults, liquidations), the Perps V2/V3 market (perpetual futures), and the Spot market (synthetic asset swaps). Deployments exist for Ethereum mainnet, Optimism, Base (Andromeda), and testnets.

## Endpoints

### Core Protocol Subgraph (Base Mainnet - Andromeda)
```
https://subgraph.satsuma-prod.com/synthetix/core-base-mainnet-andromeda/api
```

### Perps Market Subgraph (Base Mainnet - Andromeda)
```
https://subgraph.satsuma-prod.com/synthetix/perps-market-base-mainnet-andromeda/api
```

### Spot Market Subgraph (Base Mainnet - Andromeda)
```
https://subgraph.satsuma-prod.com/synthetix/spot-market-base-mainnet-andromeda/api
```

### Core Protocol Subgraph (Optimism Mainnet)
```
https://subgraph.satsuma-prod.com/synthetix/core-optimism-mainnet/api
```

### The Graph Hosted Explorer
```
https://thegraph.com/explorer?search=synthetix
```

## Authentication

No authentication is required for read-only subgraph queries. The Graph decentralized network endpoints may require a The Graph API key for production usage. Satsuma-hosted endpoints are publicly accessible.

## Example Query

```graphql
{
  markets(first: 10, orderBy: perpsMarketId) {
    id
    perpsMarketId
    marketName
    marketSymbol
    price
    skew
    size
    currentFundingRate
    makerFee
    takerFee
  }
}
```

```graphql
{
  pools(first: 5) {
    id
    owner
    name
    total_weight
    configurations {
      market {
        id
        reported_debt
        net_issuance
      }
      weight
    }
  }
}
```

## Schema Sources

Schemas are defined in the Synthetix V3 monorepo:
- Core protocol: `protocol/synthetix/subgraph/`
- Perps market: `markets/perps-market/subgraph/`
- Spot market: `markets/spot-market/subgraph/`

GitHub: https://github.com/Synthetixio/synthetix-v3

## Notes

- All numeric fields use `BigInt` or `BigDecimal` to preserve EVM precision (18-decimal wei values).
- Subgraph deployments are network-specific; separate subgraphs exist for Base Mainnet, Optimism Mainnet, Arbitrum Mainnet, and their respective testnets.
- The `@derivedFrom` directive is used extensively for reverse lookups (e.g., `configurations` on `Pool`, `positions` on `Account`).
- Synthetix V3 replaced the legacy V1/V2 architecture; the older `synthetixio-team/synthetix` subgraph on The Graph hosted service covered SNXHolder, Synth, SynthExchange, and FeesClaimed entities from V1/V2.
- Perps market data (funding rates, skew, order settlement) is indexed per network per market.
- The Graph documentation: https://thegraph.com/docs/

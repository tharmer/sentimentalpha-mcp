# SentimentAlpha.ai — Social Arbitrage Oracle Suite

Multi-tool MCP server: six Grok-powered oracles for autonomous AI agents.

**Live Service:** https://sentimentalpha.ai
**MCP Manifest:** https://sentimentalpha.ai/v1/mcp-manifest
**Agent Discovery:** https://sentimentalpha.ai/.well-known/agent.json
**OpenAPI Spec:** https://sentimentalpha.ai/openapi.json

## Six Oracle Tools

### 1. Narrative Alpha (`get_x_narrative_alpha`)
Real-time X/Twitter sentiment, narrative velocity, KOL tracking, contrarian reversal signals, and cross-asset ticker extraction. Social arbitrage intelligence for autonomous agents.

**Endpoint:** `POST /v1/narrative-alpha` (x402 paid) | `POST /v1/narrative-alpha/preview` (free)

### 2. Manipulation Risk (`analyze_manipulation_risk`)
Pre-trade safety oracle: bot farm detection, coordinated campaign analysis, KOL shill scoring, wallet-linked posting patterns, narrative fingerprinting, and astroturf flags.

**Endpoint:** `POST /v1/manipulation-alpha` (x402 paid) | `POST /v1/manipulation-alpha/preview` (free)

### 3. Convergence Alpha (`analyze_convergence`)
Multi-modal convergence: X narrative velocity + on-chain wallet flows + meme virality + prediction market delta. High-conviction trade signals when all signals align.

**Endpoint:** `POST /v1/convergence-alpha` (x402 paid) | `POST /v1/convergence-alpha/preview` (free)

### 4. Spend Guard Alpha (`analyze_spend_guard`)
Agent FinOps oracle: cost analysis for any x402 service. Spend projections, daily caps, swarm risk, and "should I run this?" recommendations. Free to use.

**Endpoint:** `POST /v1/spend-guard-alpha` (free)

### 5. Reputation Alpha (`analyze_reputation`)
Entity trust oracle: trust scoring for wallets, KOLs, agents, and services. Manipulation history, on-chain profile, social credibility analysis.

**Endpoint:** `POST /v1/reputation-alpha` (x402 paid) | `POST /v1/reputation-alpha/preview` (free)

### 6. Alert Alpha (`evaluate_alerts`)
Threshold monitoring oracle: watchlist-driven alert evaluation. Define thresholds for sentiment, velocity, or manipulation — get triggered alerts with context and recommended check intervals.

**Endpoint:** `POST /v1/alert-alpha` (x402 paid) | `POST /v1/alert-alpha/preview` (free)

## Quick Start

```bash
# Free preview — no API key, no signup, no payment
curl -s -X POST https://sentimentalpha.ai/v1/narrative-alpha/preview \
  -H "Content-Type: application/json" \
  -d '{"query": "$BTC"}' | python3 -m json.tool

# Manipulation check
curl -s -X POST https://sentimentalpha.ai/v1/manipulation-alpha/preview \
  -H "Content-Type: application/json" \
  -d '{"query": "$PEPE"}' | python3 -m json.tool

# Convergence analysis
curl -s -X POST https://sentimentalpha.ai/v1/convergence-alpha/preview \
  -H "Content-Type: application/json" \
  -d '{"query": "$SOL"}' | python3 -m json.tool

# Reputation check
curl -s -X POST https://sentimentalpha.ai/v1/reputation-alpha/preview \
  -H "Content-Type: application/json" \
  -d '{"query": "vitalik.eth"}' | python3 -m json.tool

# Alert evaluation
curl -s -X POST https://sentimentalpha.ai/v1/alert-alpha/preview \
  -H "Content-Type: application/json" \
  -d '{"query": "$BTC", "watchlist": [{"ticker": "$BTC", "condition": "sentiment_above", "threshold": 0.5}]}' | python3 -m json.tool
```

## MCP / Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "sentimentalpha": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://sentimentalpha.ai/v1/mcp-manifest"]
    }
  }
}
```

## Pricing

$0.005 USDC per query via x402 micropayments on Base (5 paid tools). Spend Guard is free.

## Architecture

- Grok API (Responses API + `web_search` tool) for live X/Twitter data
- Dual-layer cache: L1 in-memory (~0ms) + L2 Redis (~50ms)
- Velocity-based TTL: hot narratives 60s, warm 120s, stable 300s
- x402 micropayments on Base USDC
- MCP-native discovery via manifest + .well-known/agent.json

# Polymarket Anjun Copy Trading Bot

A specialized Polymarket Copy Trading bot designed to replicate the trades of **Anjun**, a top-tier Polymarket trader.

This bot monitors Anjun's wallet (`0x43372356634781eEA88d61BbDd7824cdcE958882`), detects their market moves, and automatically executes mirror trades on your account.

## Target Trader: Anjun

- **Wallet Address**: `0x43372356634781eEA88d61BbDd7824cdcE958882`
- **Strategy**: Prediction market strategies.

## Features

- **Dedicated Monitoring**: Tracks Anjun's specific trading patterns.
- **Fast Execution**: Polls for new activities every second.
- **Position Sizing**: Calculates order sizes proportional to your balance vs Anjun's balance.
- **Risk Controls**: 
  - Price deviation protection (skips if price moves >0.05 from Anjun's entry).
  - Retry logic for failed orders.
- **History**: Logs all detected and executed trades to MongoDB.

## Installation

You'll need Node.js 18+, MongoDB, and a funded Polygon wallet (USDC).

```bash
git clone https://github.com/LemnLabs/polymarket-trading-bot.git
cd polymarket-trading-bot
npm install
```

## Configuration

Copy `env.example` to `.env` and configure it. **The `USER_ADDRESS` is pre-filled below for Anjun.**

```env
# Target Wallet (Anjun)
USER_ADDRESS=0x43372356634781eEA88d61BbDd7824cdcE958882

# Your Wallet Details
PROXY_WALLET=0xYourWalletAddress
PRIVATE_KEY=your_private_key

# Polymarket API
CLOB_HTTP_URL=https://clob.polymarket.com
CLOB_WS_URL=wss://clob-ws.polymarket.com
RPC_URL=https://polygon-rpc.com
USDC_CONTRACT_ADDRESS=0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174

# Bot Settings
MONGO_URI=mongodb://localhost:27017/polymarket_anjun
FETCH_INTERVAL=1
TOO_OLD_TIMESTAMP=24
RETRY_LIMIT=3
```

## Usage

Build and start the bot:

```bash
npm run build
npm start
```

Or for development:

```bash
npm run dev
```

## How it Works

1. **Scans**: The bot continuously polls Polymarket's data API for Anjun's latest activity.
2. **Filters**: Identifies valid `TRADE` events and filters out noise.
3. **Analyzes**: Compares current market price to Anjun's execution price.
4. **Executes**: If the price is within the safety threshold (0.05), it places a matching order on your behalf using your configured proxy wallet.

## Disclaimer

This software is for educational purposes. Copy trading involves significant risk.
- **Slippage**: You may get worse prices than Anjun due to latency.
- **Losses**: Even top traders like Anjun take losses. You are responsible for your own funds.
- ** DYOR**: Always monitor the bot's performance.

## License

ISC

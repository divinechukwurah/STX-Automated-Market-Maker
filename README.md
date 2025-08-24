Concentrated Liquidity AMM Contract

Overview

This contract implements a concentrated liquidity automated market maker (AMM) inspired by Uniswap v3, deployed on the Stacks blockchain using the Clarity smart contract language. Unlike constant-product AMMs, this design allows liquidity providers (LPs) to specify custom price ranges (via ticks) where their liquidity is active, improving capital efficiency and enabling tighter spreads for traders.

✨ Key Features

Pool Creation

Supports multiple fee tiers: 0.3%, 1%, 3%.

Initializes pools with token pairs and a starting square-root price.

Liquidity Management

Mint positions: Add liquidity within a specified tick range.

Burn positions: Remove liquidity and withdraw owed tokens.

Tracks position-specific liquidity, fees, and unclaimed rewards.

Swap Functionality

Supports exact input single swaps.

Enforces slippage protection with minimum output amounts.

Simplified but extendable swap math for precision pricing.

Tick and Price Management

Maintains tick states with gross/net liquidity values.

Updates ticks when liquidity is added/removed.

Price updates rely on square-root price representation (x96 fixed point).

Fee Accrual

Fees grow globally per pool and per tick.

Simplified tracking for inside/outside fee growth, extendable for more precise accounting.

🛠️ Data Structures

pools – Stores pool state (sqrt price, tick, liquidity, fees).

positions – Tracks liquidity provider positions with fee growth snapshots.

ticks – Tracks liquidity and fee growth at specific ticks.

🔐 Error Codes

u100 → Unauthorized

u101 → Invalid amount

u102 → Insufficient liquidity

u103 → Invalid tick

u104 → Position not found

u105 → Slippage exceeded

u106 → Invalid token

u107 → Invalid fee tier

u108 → Identical tokens

📜 Functions
Administrative

create-pool(token0, token1, fee, sqrt-price-x96) → Creates a new liquidity pool.

Liquidity Management

mint-position(...) → Adds liquidity in a tick range.

burn-position(...) → Removes liquidity.

Swaps

exact-input-single(...) → Performs a swap given an input amount.

Helpers

Tick-to-price conversions (tick-to-sqrt-price, sqrt-price-to-tick).

Liquidity calculations (calculate-liquidity-for-amounts, calculate-amounts-for-liquidity).

Read-Only Views

get-pool(token0, token1, fee)

get-position(owner, token0, token1, fee, tick-lower, tick-upper)

get-tick(token0, token1, fee, tick)

🚀 Usage Workflow

Admin creates a pool with a fee tier and initial price.

Liquidity Providers mint positions by specifying:

Token pair

Fee tier

Tick range

Desired token amounts

Traders perform swaps via exact-input-single, respecting slippage.

Liquidity Providers burn positions to withdraw liquidity and earned fees.

⚠️ Notes & Limitations

Tick-to-price conversion is simplified (not production-accurate).

Fee growth inside/outside positions currently stubbed (u0).

Swap math is simplified and should be extended for real-world use.

Security review required before deployment in production.

📄 License

MIT License
# YieldAggregator

A Clarity smart contract for aggregating STX yield across multiple strategies on the Stacks blockchain.

## Overview

YieldAggregator is a yield farming protocol that allows users to deposit STX and earn yield from multiple underlying strategies. The contract manages strategy registration, user deposits/withdrawals, and proportional asset distribution through a share-based accounting system.

## Features

- **Multi-Strategy Support**: Register and manage multiple yield strategies with configurable weights
- **Share-Based Accounting**: Users receive shares proportional to their deposits (1:1 ratio)
- **Admin Controls**: Secure admin functions for strategy management and weight adjustments
- **Proportional Withdrawals**: Users redeem shares for their proportional share of aggregated assets
- **Error Handling**: Comprehensive error codes for invalid operations and access control

## How It Works

1. **Admin registers strategies** with weight allocations
2. **Users deposit STX** to mint shares (1 STX = 1 share)
3. **Aggregator distributes deposits** to strategies based on weights
4. **Users withdraw** by redeeming shares for proportional STX

## Contract Functions

### Admin Functions

- `register-strategy(strategy-principal, weight)` - Register a new yield strategy with weight
- `update-weight(idx, weight)` - Adjust strategy weight for rebalancing

### User Functions

- `deposit(amount)` - Deposit STX and mint shares
- `withdraw(share-amount)` - Redeem shares for STX

### Read-Only Functions

- `get-shares(who)` - Query user's share balance
- `get-strategy(idx)` - Get strategy details by index
- `get-strategy-balance(idx)` - Get strategy's STX balance
- `sum-all-assets()` - Get total assets under management


## Usage Example

```clarity
;; Register a strategy with 50% weight
(contract-call? .yield-aggregator register-strategy .strategy-1 u5000)

;; Deposit 1000 STX
(contract-call? .yield-aggregator deposit u1000000000)

;; Check your shares
(contract-call? .yield-aggregator get-shares tx-sender)

;; Withdraw 500 shares
(contract-call? .yield-aggregator withdraw u500000000)

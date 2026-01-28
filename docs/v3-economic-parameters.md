# V3 Economic Parameters Reference

This document lists only V3-specific economic parameters.

## Bold V3 Parameters (SystemParams.sol)

| Parameter | Description |
|-----------|-------------|
| MIN_DEBT | Minimum net debt |
| LIQUIDATION_PENALTY_SP | SP liquidation penalty (>=5%) |
| LIQUIDATION_PENALTY_REDISTRIBUTION | Redistribution penalty (<=20%) |
| CCR, SCR, MCR | Collateral ratios (100-200%) |
| BCR | Batch CR buffer (5-50%) |
| MIN_ANNUAL_INTEREST_RATE | Min interest (<=250%) |
| REDEMPTION_FEE_FLOOR | Min redemption fee |
| SP_YIELD_SPLIT | Yield to SP depositors |

## Mento V3 Parameters (FPMM.sol)

| Parameter | Description |
|-----------|-------------|
| lpFee | LP fee (combined <=2%) |
| protocolFee | Protocol fee |
| rebalanceIncentive | Rebalance bonus (<=1%) |
| rebalanceThreshold* | Deviation thresholds (<=10%) |

## TradingLimitsV2

| Parameter | Description |
|-----------|-------------|
| limit0 | 5-min window limit |
| limit1 | 1-day window limit |

## CDPLiquidityStrategy

| Parameter | Description |
|-----------|-------------|
| stabilityPoolPercentage | SP % for rebalancing |
| maxIterations | Max redemption loops |

# V3 Economic Parameters Reference

This document lists only V3-specific economic parameters.

---

# Bold V3 Parameters

## SystemParams.sol (Configurable at deployment)

| Parameter | Constraints | Description |
|-----------|-------------|-------------|
| MIN_DEBT | > 0 | Minimum net debt |
| LIQUIDATION_PENALTY_SP | >= 5% | SP liquidation penalty |
| LIQUIDATION_PENALTY_REDISTRIBUTION | >= SP, <= 20% | Redistribution penalty |
| COLL_GAS_COMPENSATION_DIVISOR | <= 1000 | Collateral comp divisor |
| COLL_GAS_COMPENSATION_CAP | <= 10 ether | Max collateral comp |
| ETH_GAS_COMPENSATION | <= 1 ether | Fixed gas compensation |
| CCR | 100-200% | Critical Collateral Ratio |
| SCR | 100-200% | Shutdown Collateral Ratio |
| MCR | 100-200% | Minimum Collateral Ratio |
| BCR | 5-50% | Batch CR Buffer |
| MIN_ANNUAL_INTEREST_RATE | <= 250% | Min interest rate |
| REDEMPTION_FEE_FLOOR | <= 100% | Min redemption fee |
| INITIAL_BASE_RATE | <= 1000% | Starting base rate |
| REDEMPTION_MINUTE_DECAY_FACTOR | - | Decay per minute |
| REDEMPTION_BETA | - | Volume sensitivity |
| SP_YIELD_SPLIT | <= 100% | SP depositor yield % |
| MIN_BOLD_IN_SP | >= 1e18 | Min BOLD in SP |
| MIN_BOLD_AFTER_REBALANCE | >= MIN_BOLD_IN_SP | Min after rebalance |

## Constants.sol (Hardcoded)

| Parameter | Value | Description |
|-----------|-------|-------------|
| MAX_ANNUAL_INTEREST_RATE | 250% | Max interest ceiling |
| MAX_ANNUAL_BATCH_MANAGEMENT_FEE | 10% | Max batch fee |
| MIN_INTEREST_RATE_CHANGE_PERIOD | 1 hour | Rate change cooldown |
| URGENT_REDEMPTION_BONUS | 1% | Post-shutdown bonus |
| MAX_LIQUIDATION_PENALTY_REDISTRIBUTION | 20% | Max redist penalty |

---

# Mento Core V3 Parameters

## FPMM.sol (Per-pool, owner updatable)

| Parameter | Constraints | Setter |
|-----------|-------------|--------|
| lpFee | combined <= 2% | setLPFee() |
| protocolFee | combined <= 2% | setProtocolFee() |
| protocolFeeRecipient | non-zero if fee > 0 | setProtocolFeeRecipient() |
| rebalanceIncentive | <= 1% | setRebalanceIncentive() |
| rebalanceThresholdAbove | <= 10% | setRebalanceThresholds() |
| rebalanceThresholdBelow | <= 10% | setRebalanceThresholds() |

## FPMMFactory.sol (Factory defaults)

| Parameter | Constraints | Setter |
|-----------|-------------|--------|
| defaultParams | Same as FPMM params | setDefaultParams() |
| oracleAdapter | non-zero | setOracleAdapter() |
| proxyAdmin | non-zero | setProxyAdmin() |

## TradingLimitsV2.sol (Per-token)

| Parameter | Type | Description |
|-----------|------|-------------|
| limit0 | int120 | 5-min window limit |
| limit1 | int120 | 1-day window limit |
| decimals | uint8 | Token decimals (1-18) |

Constants: TIMESTEP0 = 5 min, TIMESTEP1 = 1 day

## LiquidityStrategy.sol (Per-pool, base class)

| Parameter | Constraints | Description |
|-----------|-------------|-------------|
| cooldown | uint64 | Min time between rebalances |
| liquiditySourceIncentiveBpsExpansion | combined <= 10000 | LP incentive (expansion) |
| protocolIncentiveBpsExpansion | combined <= 10000 | Protocol incentive (expansion) |
| liquiditySourceIncentiveBpsContraction | combined <= 10000 | LP incentive (contraction) |
| protocolIncentiveBpsContraction | combined <= 10000 | Protocol incentive (contraction) |
| protocolFeeRecipient | non-zero if incentives > 0 | Fee recipient |

## ReserveLiquidityStrategy.sol (Extends LiquidityStrategy)

| Parameter | Setter | Description |
|-----------|--------|-------------|
| reserve | setReserve() | Mento Reserve address |

Inherits all LiquidityStrategy pool config params. Uses Reserve for mint/burn.

## CDPLiquidityStrategy.sol (Extends LiquidityStrategy)

| Parameter | Constraints | Description |
|-----------|-------------|-------------|
| stabilityPool | non-zero | SP for collateral swaps |
| collateralRegistry | non-zero | For redemptions |
| stabilityPoolPercentage | 0 < x < 10000 | SP % for rebalancing |
| maxIterations | uint16 | Max redemption loops |
| REDEMPTION_SHORTFALL_TOLERANCE | immutable | Max shortfall allowed |

---

## Contracts Without Economic Params

- **Router.sol** - Routing only (immutable factory refs)
- **FactoryRegistry.sol** - Factory approval registry
- **ReserveV2.sol** - Asset/spender registries
- **StableTokenV3.sol** - Role management
- **OracleAdapter.sol** - Price feed infrastructure

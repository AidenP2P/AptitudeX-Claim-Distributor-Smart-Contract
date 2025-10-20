# AptitudeX-Claim-Distributor-Smart-Contract
Smart contract to distribute APX rewards via daily and weekly claims with streak tracking and progressive bonuses. Includes admin provisioning, config toggles, pausing and emergency withdraw. Gasless-ready.

# ClaimDistributor — APX Reward Claiming with Streak Bonuses

This contract distributes APX tokens through **daily** and **weekly** claims.  
It includes a **streak-based bonus system**, query helpers, and admin controls.  
It is also compatible with gasless meta-transactions.

---

## Features

- Daily and weekly reward claiming
- Progressive streak bonuses with grace period
- View functions to preview rewards and claim windows
- Admin functions for provisioning, config update, pause toggle, emergency withdraw
- Secured with Ownable and ReentrancyGuard

---

## How It Works

### Daily & Weekly Claims
Users can:
- Call `claimDaily()` once every 24 hours
- Call `claimWeekly()` once every 7 days

If the claim is made within a **grace period**, the streak increases.  
If missed, the streak resets to 1.

### Streak Bonuses
Multipliers are defined in basis points. Example (daily):
- 7 consecutive days → +20%
- 30 consecutive days → +50%
- 100 consecutive days → +100%

Final reward = `baseAmount * multiplier / 10000`.

---

## Admin Controls

| Function | Purpose |
|---------|----------|
| `provision()` | Fund the contract with APX |
| `updateConfig()` | Update base amounts and enable/disable claims |
| `toggleClaims()` | Pause/resume claims |
| `emergencyWithdraw()` | Recover funds if needed |

Only the contract owner can call these functions.

---

## View Helper Functions

| Function | Description |
|---------|-------------|
| `canClaimDaily/Weekly` | Check if a user can claim now |
| `getNextClaimTimes` | Returns timestamps of next eligible claims |
| `getRewardAmounts` | Predict the next daily/weekly reward |
| `getBonusPercentages` | Returns the current applicable bonus |
| `getStreakMultipliers` | Returns configured streak tiers |

---

## Deployment

```solidity
constructor(address _apxToken)

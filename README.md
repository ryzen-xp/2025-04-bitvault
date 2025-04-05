# BitVault audit details
- Total Prize Pool: $15,000 in USDC
  - HM awards: up to $10,500 USDC 
    - If no valid Highs or Mediums are found, the HM pool is $0 
  - Judge awards: $2,500 in USDC
  - Validator awards: $1,500 USDC 
  - Scout awards: $500 in USDC
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts April 2, 2025 20:00 UTC
- Ends April 11, 2025 20:00 UTC 

**Note re: risk level upgrades/downgrades**

Two important notes about judging phase risk adjustments: 
- High- or Medium-risk submissions downgraded to Low-risk (QA) will be ineligible for awards.
- Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.

As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2025-04-bitvault/blob/main/4naly3er-report.md).

_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

### Out-of-Scope Considerations

- The owner's keys could get compromised. Any key management is **out of scope**.
- The Chainlink oracle could be compromised or faulty, which would also be **out of scope**.


### Publicly Known Issues

Any issues that have been marked as acknowledged in the original forked repository of `Popcorn-Limited/bvusd` as well as `liquity/bold` should be considered out-of-scope. Specifically:

- Any public issue in the [Liquity repository](https://github.com/liquity/bold/issues), including [`wontfix` issues](https://github.com/liquity/bold/issues?q=label%3Awontfix+)
- [Any known issue in the `bvusd` repository](https://github.com/Popcorn-Limited/bvusd/blob/main/README.md#known-issues-and-mitigations)


If the impact of a previously acknowledged issue has been escalated adequately due to the delta introduced by the BitVault team, it may be considered in-scope for the contest.

# Overview

The code of the BitVault project is a Liquity V2 fork introducing the following features:

- Dynamic Collateral Registry
- Whitelist Enforcement
- Configurable Collateral Ratios & Liquidation Configurations
- Shutdown Capability for Protocol Token Owner

## Links

- **Previous audits:**  
-- [ChainSecurity Audit Report](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FE2A1Xrcj7XasxOiotWky%2Fuploads%2F7ELJ5yuvXnUtgd9NQPHk%2FChainSecurity_Liquity_Bold_audit.pdf?alt=media&token=eb681c56-e650-499b-aaca-7099823e08c4)
-- [Coinspect Audit Report](https://www.coinspect.com/doc/Coinspect%20-%20Smart%20Contract%20Audit%20-%20Liquity%20-%20Bold%20-%20v241231.pdf)
-- [Dedaub Audit Report Round I](https://dedaub.com/audits/liquity/liquity-v2-aug-28-2024/)
-- [Dedaub Audit Report Round II](https://dedaub.com/audits/liquity/liquity-v2-second-audit-nov-11-2024/)
- **Documentation:** https://github.com/Popcorn-Limited/bvusd/blob/main/README.md
- **Website:** https://www.bitvault.finance/
- **X/Twitter:** https://x.com/BitVaultFinance

---

# Scope

### Files in scope

*See [scope.txt](https://github.com/code-423n4/2025-04-bitvault/blob/main/scope.txt)*

| File   | nSLOC | 
| ------ | ----- |
| [contracts/src/CollateralRegistry.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/CollateralRegistry.sol) | 202 |
| [contracts/src/StabilityPool.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/StabilityPool.sol) | 308 |
| [contracts/src/BorrowerOperations.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/BorrowerOperations.sol) |  1102 |
| [contracts/src/AddressesRegistry.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/AddressesRegistry.sol) |  193 |
| [contracts/src/TroveManager.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/TroveManager.sol) | 1397 | 
| [contracts/src/Dependencies/LiquityBase.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/LiquityBase.sol) | 67 | 
| **Totals** |  **3269** |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2025-04-bitvault/blob/main/out_of_scope.txt)*

| File / Path        |
| ------------ |
| [contracts/src/ActivePool.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/ActivePool.sol) |
| [contracts/src/BoldToken.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/BoldToken.sol) |
| [contracts/src/CollSurplusPool.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/CollSurplusPool.sol) |
| [contracts/src/DefaultPool.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/DefaultPool.sol) |
| [contracts/src/MultiTroveGetter.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/MultiTroveGetter.sol) |
| [contracts/src/GasPool.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/GasPool.sol) |
| [contracts/src/HintHelpers.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/HintHelpers.sol) |
| [contracts/src/SortedTroves.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/SortedTroves.sol) |
| [contracts/src/TroveNFT.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/TroveNFT.sol) |
| [contracts/src/Dependencies/AddRemoveManagers.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/AddRemoveManagers.sol) |
| [contracts/src/Dependencies/AggregatorV3Interface.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/AggregatorV3Interface.sol) |
| [contracts/src/Dependencies/Constants.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/Constants.sol) |
| [contracts/src/Dependencies/IOsTokenVaultController.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/IOsTokenVaultController.sol) |
| [contracts/src/Dependencies/IStaderOracle.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/IStaderOracle.sol) |
| [contracts/src/Dependencies/LiquityMath.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/LiquityMath.sol) |
| [contracts/src/Dependencies/Ownable.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/Ownable.sol) |
| [contracts/src/Dependencies/Owned.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/Owned.sol) |
| [contracts/src/Dependencies/TokenWrapper.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/TokenWrapper.sol) |
| [contracts/src/Dependencies/Whitelist.sol](https://github.com/code-423n4/2025-04-bitvault/blob/main/contracts/src/Dependencies/Whitelist.sol) |
| [contracts/certora/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/certora) |
| [contracts/script/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/script) |
| [contracts/src/Interfaces/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/src/Interfaces)|
| [contracts/src/NFTMetadata/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/src/NFTMetadata) |
| [contracts/src/PriceFeeds/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/src/PriceFeeds) |
| [contracts/src/Types/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/src/Types) |
| [contracts/src/Zappers/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/src/Zappers) |
| [contracts/test/\*\*.\*\*](https://github.com/code-423n4/2025-04-bitvault/tree/main/contracts/test) |

## Scoping Q &amp; A

| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| ERC20 used by the protocol              |      WBTC, WETH             |
| Test coverage                           | 99% (% Lines), 98.5% (% Functions)                          |
| ERC721 used  by the protocol            |            None              |
| ERC777 used by the protocol             |           None                |
| ERC1155 used by the protocol            |              None            |
| Chains the protocol will be deployed on | Arbitrum, Ethereum, Optimism |

### ERC20 token behaviors in scope

| Question                                                                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| [Missing return values](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#missing-return-values)                                                      |  No  |
| [Fee on transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer)                                                                  |  No |
| [Balance changes outside of transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#balance-modifications-outside-of-transfers-rebasingairdrops) |  No  |
| [Upgradeability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#upgradable-tokens)                                                                 |  No  |
| [Flash minting](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#flash-mintable-tokens)                                                              |  No  |
| [Pausability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens)                                                                      |  No  |
| [Approval race protections](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#approval-race-protections)                                              |  No  |
| [Revert on approval to zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-approval-to-zero-address)                            | No   |
| [Revert on zero value approvals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-approvals)                                    |  No  |
| [Revert on zero value transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                    |  No  |
| [Revert on transfer to the zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-transfer-to-the-zero-address)                    |  No  |
| [Revert on large approvals and/or transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers)                  |  No  |
| [Doesn't revert on failure](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#no-revert-on-failure)                                                   |  No  |
| [Multiple token addresses](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                          |  No  |
| [Low decimals ( < 6)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#low-decimals)                                                                 |   No |
| [High decimals ( > 18)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#high-decimals)                                                              |  No  |
| [Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists)                                                                |  No  |

### External integrations (e.g., Uniswap) behavior in scope:


| Question                                                  | Answer |
| --------------------------------------------------------- | ------ |
| Enabling/disabling fees (e.g. Blur disables/enables fees) | No   |
| Pausability (e.g. Uniswap pool gets paused)               |  No   |
| Upgradeability (e.g. Uniswap gets upgraded)               |   No  |




# Additional context

## Main invariants

Any invariants outlined in the original `Popcorn-Limited/bvusd` and `liquity/bold` are considered to be inherited by the BitVault implementation.

## Attack ideas (where to focus for bugs)

The main questions that are of concern are: 

  - Can whitelists be circumvented somehow? 
  - Could whitelist additions brick the original logic in any way?

We would also like to know if changing configurational values after deployment could cause any issues. In detail, we are not interested in economic issues due to a misconfiguration but rather actual code / state issues such as the code not being able to handle a variable update.

## All trusted roles in the protocol

| Role          | Description           |
|--------------|----------------------|
| Owner        | Will be isolated in a 7/8 multisig |


## Describe any novel or unique curve logic or mathematical models implemented in the contracts:

N/A

## Running tests

To setup the project, make sure you have `foundry` installed and then execute:

```bash 
git clone https://github.com/code-423n4/2025-04-bitvault
cd 2025-04-bitvault/contracts
forge install
```

To run tests:

```bash 
forge test
```

To run code coverage:

```bash
sudo apt-get install lcov

forge coverage --report lcov
lcov --remove lcov.info 'test/*' 'script/*' -o lcov_filtered.info

lcov --extract lcov_filtered.info \
  "src/CollateralRegistry.sol" \
  "src/StabilityPool.sol" \
  "src/BorrowerOperations.sol" \
  "src/AddressesRegistry.sol" \
  "src/Dependencies/LiquityBase.sol" \
  "src/TroveManager.sol" \
  -o lcov_scope.info

lcov --list lcov_scope.info
```

### Coverage Report

| Filename                           | Lines   | Functions |
|-------------------------------------|---------|-----------|
| AddressesRegistry.sol               | 96.0% (101) | 100% (7)   | 
| BorrowerOperations.sol              | 98.4% (621) | 97.3% (74) |
| CollateralRegistry.sol              | 99.2% (126) | 95.0% (20) |
| Dependencies/LiquityBase.sol        | 100% (36)  | 100% (9)   | 
| StabilityPool.sol                   | 99.5% (196) | 100% (28)  | 
| TroveManager.sol                    | 99.7% (672) | 100% (63)  |
| **Total:**                          | **99.0% (1752)** | **98.5% (201)** |

## Miscellaneous
Employees of BitVault and employees' family members are ineligible to participate in this audit.

Code4rena's rules cannot be overridden by the contents of this README. In case of doubt, please check with C4 staff.

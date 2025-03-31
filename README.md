# ✨ So you want to run an audit

This `README.md` contains a set of checklists for our audit collaboration. This is your audit repo, which is used for scoping your audit and for providing information to wardens

Some of the checklists in this doc are for our scouts and some of them are for **you as the audit sponsor (⭐️)**.

---

# Repo setup

## ⭐️ Sponsor: Add code to this repo

- [ ] Create a PR to this repo with the below changes:
- [ ] Confirm that this repo is a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 48 business hours prior to audit start time.**
- [ ] Be prepared for a 🚨code freeze🚨 for the duration of the audit — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the audit. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)

## ⭐️ Sponsor: Repo checklist

- [ ] Modify the [Overview](#overview) section of this `README.md` file. Describe how your code is supposed to work with links to any relevant documentation and any other criteria/details that the auditors should keep in mind when reviewing. (Here are two well-constructed examples: [Ajna Protocol](https://github.com/code-423n4/2023-05-ajna) and [Maia DAO Ecosystem](https://github.com/code-423n4/2023-05-maia))
- [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] Review and confirm the details created by the Scout (technical reviewer) who was assigned to your contest. *Note: any files not listed as "in scope" will be considered out of scope for the purposes of judging, even if the file will be part of the deployed contracts.*  

---

# BitVault audit details
- Total Prize Pool: $15,000 in USDC
  - HM awards: up to $10,500 USDC 
    - If no valid Highs or Mediums are found, the HM pool is $0 
  - Judge awards: $2,500 in USDC
  - Validator awards: $1,500 USDC (Notion: Triage fee - final)
  - Scout awards: $500 in USDC
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts April 1, 2025 20:00 UTC
- Ends April 8, 2025 20:00 UTC 

**Note re: risk level upgrades/downgrades**

Two important notes about judging phase risk adjustments: 
- High- or Medium-risk submissions downgraded to Low-risk (QA) will be ineligible for awards.
- Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.

As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2025-04-bitvault/blob/main/4naly3er-report.md).



_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

The owners keys could get compromised. Any key management is out of scope.
Chainlink oracle could be compromised / faulty which would also be out of scope

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

# Overview

[ ⭐️ SPONSORS: add info here ]

## Links

- **Previous audits:**  
  - ✅ SCOUTS: If there are multiple report links, please format them in a list.
- **Documentation:** https://github.com/Popcorn-Limited/bvusd/blob/main/README.md
- **Website:** 🐺 CA: add a link to the sponsor's website
- **X/Twitter:** 🐺 CA: add a link to the sponsor's Twitter
- **Discord:** 🐺 CA: add a link to the sponsor's Discord

---

# Scope

[ ✅ SCOUTS: add scoping and technical details here ]

### Files in scope
- ✅ This should be completed using the `metrics.md` file
- ✅ Last row of the table should be Total: SLOC
- ✅ SCOUTS: Have the sponsor review and and confirm in text the details in the section titled "Scoping Q amp; A"

*For sponsors that don't use the scoping tool: list all files in scope in the table below (along with hyperlinks) -- and feel free to add notes to emphasize areas of focus.*

| Contract | SLOC | Purpose | Libraries used |  
| ----------- | ----------- | ----------- | ----------- |
| [contracts/folder/sample.sol](https://github.com/code-423n4/repo-name/blob/contracts/folder/sample.sol) | 123 | This contract does XYZ | [`@openzeppelin/*`](https://openzeppelin.com/contracts/) |

### Files out of scope
✅ SCOUTS: List files/directories out of scope

## Scoping Q &amp; A

### General questions
### Are there any ERC20's in scope?: Yes

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".

Specific tokens (please specify)
WBTC, WETH

### Are there any ERC777's in scope?: No

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".



### Are there any ERC721's in scope?: No

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".



### Are there any ERC1155's in scope?: No

✅ SCOUTS: If the answer above 👆 is "Yes", please add the tokens below 👇 to the table. Otherwise, update the column with "None".



✅ SCOUTS: Once done populating the table below, please remove all the Q/A data above.

| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| ERC20 used by the protocol              |       🖊️             |
| Test coverage                           | ✅ SCOUTS: Please populate this after running the test coverage command                          |
| ERC721 used  by the protocol            |            🖊️              |
| ERC777 used by the protocol             |           🖊️                |
| ERC1155 used by the protocol            |              🖊️            |
| Chains the protocol will be deployed on | Arbitrum,Ethereum,Optimism |

### ERC20 token behaviors in scope

| Question                                                                                                                                                   | Answer |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| [Missing return values](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#missing-return-values)                                                      |    |
| [Fee on transfer](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#fee-on-transfer)                                                                  |   |
| [Balance changes outside of transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#balance-modifications-outside-of-transfers-rebasingairdrops) |    |
| [Upgradeability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#upgradable-tokens)                                                                 |    |
| [Flash minting](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#flash-mintable-tokens)                                                              |    |
| [Pausability](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#pausable-tokens)                                                                      |    |
| [Approval race protections](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#approval-race-protections)                                              |    |
| [Revert on approval to zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-approval-to-zero-address)                            |    |
| [Revert on zero value approvals](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-approvals)                                    |    |
| [Revert on zero value transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                    |    |
| [Revert on transfer to the zero address](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-transfer-to-the-zero-address)                    |    |
| [Revert on large approvals and/or transfers](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-large-approvals--transfers)                  |    |
| [Doesn't revert on failure](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#no-revert-on-failure)                                                   |    |
| [Multiple token addresses](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers)                                          |    |
| [Low decimals ( < 6)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#low-decimals)                                                                 |    |
| [High decimals ( > 18)](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#high-decimals)                                                              |    |
| [Blocklists](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#tokens-with-blocklists)                                                                |    |

### External integrations (e.g., Uniswap) behavior in scope:


| Question                                                  | Answer |
| --------------------------------------------------------- | ------ |
| Enabling/disabling fees (e.g. Blur disables/enables fees) | No   |
| Pausability (e.g. Uniswap pool gets paused)               |  No   |
| Upgradeability (e.g. Uniswap gets upgraded)               |   No  |


### EIP compliance checklist
N/A

✅ SCOUTS: Please format the response above 👆 using the template below👇

| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| src/Token.sol                           | ERC20, ERC721                |
| src/NFT.sol                             | ERC721                       |


# Additional context

## Main invariants

N/A

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

## Attack ideas (where to focus for bugs)
The biggest questions are if whitelists can be circumvented somehow or if whitelist additions could brick the original logic.
We would also like to know if changing values after deployment could case any issues (not economic issues but actual code / state issues)

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

## All trusted roles in the protocol

We have an owner which will be isolated 7/8 multisigs.

✅ SCOUTS: Please format the response above 👆 using the template below👇

| Role                                | Description                       |
| --------------------------------------- | ---------------------------- |
| Owner                          | Has superpowers                |
| Administrator                             | Can change fees                       |

## Describe any novel or unique curve logic or mathematical models implemented in the contracts:

N/A

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

## Running tests

foundryup
forge install
forge test

✅ SCOUTS: Please format the response above 👆 using the template below👇

```bash
git clone https://github.com/code-423n4/2023-08-arbitrum
git submodule update --init --recursive
cd governance
foundryup
make install
make build
make sc-election-test
```
To run code coverage
```bash
make coverage
```
To run gas benchmarks
```bash
make gas
```

✅ SCOUTS: Add a screenshot of your terminal showing the gas report
✅ SCOUTS: Add a screenshot of your terminal showing the test coverage


# Scope

*See [scope.txt](https://github.com/code-423n4/2025-04-bitvault/blob/main/scope.txt)*

### Files in scope


| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| /contracts/src/CollateralRegistry.sol | 1| **** | 202 | |openzeppelin-contracts/contracts/token/ERC20/extensions/IERC20Metadata.sol|
| /contracts/src/StabilityPool.sol | 1| **** | 308 | |openzeppelin-contracts/contracts/token/ERC20/utils/SafeERC20.sol|
| /contracts/src/BorrowerOperations.sol | 1| **** | 1102 | |openzeppelin-contracts/contracts/token/ERC20/utils/SafeERC20.sol|
| /contracts/src/AddressesRegistry.sol | 1| **** | 193 | ||
| /contracts/src/Dependencies/LiquityBase.sol | 1| **** | 67 | ||
| /contracts/src/TroveManager.sol | 1| **** | 1397 | ||
| **Totals** | **6** | **** | **3269** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2025-04-bitvault/blob/main/out_of_scope.txt)*

| File         |
| ------------ |
| ./contracts/certora/harnesses/ERC20Like/DummyERC20A.sol |
| ./contracts/certora/harnesses/ERC20Like/DummyERC20B.sol |
| ./contracts/certora/harnesses/ERC20Like/DummyWeth.sol |
| ./contracts/certora/harnesses/TroveManagerHarness.sol |
| ./contracts/certora/harnesses/Utilities.sol |
| ./contracts/script/Dependencies/GovernanceProxy.sol |
| ./contracts/script/DeployGovernance.s.sol |
| ./contracts/script/DeployOnlyExchangeHelpers.s.sol |
| ./contracts/script/DeploySomeCurvePools.s.sol |
| ./contracts/script/GenerateStakingRewards.s.sol |
| ./contracts/script/Interfaces/Balancer/IVault.sol |
| ./contracts/script/Interfaces/Balancer/IWeightedPool.sol |
| ./contracts/script/LiquidateTrove.s.sol |
| ./contracts/script/OpenTroves.s.sol |
| ./contracts/script/ProvideCurveLiquidity.s.sol |
| ./contracts/script/ProvideUniV3Liquidity.s.sol |
| ./contracts/script/RedeemCollateral.s.sol |
| ./contracts/script/RedeployWETHZappers.s.sol |
| ./contracts/src/ActivePool.sol |
| ./contracts/src/BoldToken.sol |
| ./contracts/src/CollSurplusPool.sol |
| ./contracts/src/DefaultPool.sol |
| ./contracts/src/Dependencies/AddRemoveManagers.sol |
| ./contracts/src/Dependencies/AggregatorV3Interface.sol |
| ./contracts/src/Dependencies/Constants.sol |
| ./contracts/src/Dependencies/IOsTokenVaultController.sol |
| ./contracts/src/Dependencies/IStaderOracle.sol |
| ./contracts/src/Dependencies/LiquityMath.sol |
| ./contracts/src/Dependencies/Ownable.sol |
| ./contracts/src/Dependencies/Owned.sol |
| ./contracts/src/Dependencies/TokenWrapper.sol |
| ./contracts/src/Dependencies/Whitelist.sol |
| ./contracts/src/GasPool.sol |
| ./contracts/src/HintHelpers.sol |
| ./contracts/src/Interfaces/IActivePool.sol |
| ./contracts/src/Interfaces/IAddRemoveManagers.sol |
| ./contracts/src/Interfaces/IAddressesRegistry.sol |
| ./contracts/src/Interfaces/IAddressesRegistryWhitelist.sol |
| ./contracts/src/Interfaces/IBoldRewardsReceiver.sol |
| ./contracts/src/Interfaces/IBoldToken.sol |
| ./contracts/src/Interfaces/IBorrowerOperations.sol |
| ./contracts/src/Interfaces/ICollSurplusPool.sol |
| ./contracts/src/Interfaces/ICollateralRegistry.sol |
| ./contracts/src/Interfaces/ICommunityIssuance.sol |
| ./contracts/src/Interfaces/IDefaultPool.sol |
| ./contracts/src/Interfaces/IHintHelpers.sol |
| ./contracts/src/Interfaces/IInterestRouter.sol |
| ./contracts/src/Interfaces/ILQTYStaking.sol |
| ./contracts/src/Interfaces/ILQTYToken.sol |
| ./contracts/src/Interfaces/ILiquityBase.sol |
| ./contracts/src/Interfaces/IMainnetPriceFeed.sol |
| ./contracts/src/Interfaces/IMultiTroveGetter.sol |
| ./contracts/src/Interfaces/IOwned.sol |
| ./contracts/src/Interfaces/IPriceFeed.sol |
| ./contracts/src/Interfaces/IRETHPriceFeed.sol |
| ./contracts/src/Interfaces/IRETHToken.sol |
| ./contracts/src/Interfaces/ISortedTroves.sol |
| ./contracts/src/Interfaces/IStabilityPool.sol |
| ./contracts/src/Interfaces/IStabilityPoolEvents.sol |
| ./contracts/src/Interfaces/ITokenWrapper.sol |
| ./contracts/src/Interfaces/ITroveEvents.sol |
| ./contracts/src/Interfaces/ITroveManager.sol |
| ./contracts/src/Interfaces/ITroveNFT.sol |
| ./contracts/src/Interfaces/IWETH.sol |
| ./contracts/src/Interfaces/IWSTETH.sol |
| ./contracts/src/Interfaces/IWSTETHPriceFeed.sol |
| ./contracts/src/Interfaces/IWhitelist.sol |
| ./contracts/src/MultiTroveGetter.sol |
| ./contracts/src/NFTMetadata/MetadataNFT.sol |
| ./contracts/src/NFTMetadata/utils/FixedAssets.sol |
| ./contracts/src/NFTMetadata/utils/JSON.sol |
| ./contracts/src/NFTMetadata/utils/SVG.sol |
| ./contracts/src/NFTMetadata/utils/Utils.sol |
| ./contracts/src/NFTMetadata/utils/baseSVG.sol |
| ./contracts/src/NFTMetadata/utils/bauhaus.sol |
| ./contracts/src/PriceFeeds/CompositePriceFeed.sol |
| ./contracts/src/PriceFeeds/MainnetPriceFeedBase.sol |
| ./contracts/src/PriceFeeds/RETHPriceFeed.sol |
| ./contracts/src/PriceFeeds/WETHPriceFeed.sol |
| ./contracts/src/PriceFeeds/WSTETHPriceFeed.sol |
| ./contracts/src/SortedTroves.sol |
| ./contracts/src/TroveNFT.sol |
| ./contracts/src/Types/BatchId.sol |
| ./contracts/src/Types/LatestBatchData.sol |
| ./contracts/src/Types/LatestTroveData.sol |
| ./contracts/src/Types/TroveChange.sol |
| ./contracts/src/Types/TroveId.sol |
| ./contracts/src/Zappers/BaseTokenZapper.sol |
| ./contracts/src/Zappers/BaseZapper.sol |
| ./contracts/src/Zappers/GasCompZapper.sol |
| ./contracts/src/Zappers/Interfaces/IExchange.sol |
| ./contracts/src/Zappers/Interfaces/IExchangeHelpers.sol |
| ./contracts/src/Zappers/Interfaces/IFlashLoanProvider.sol |
| ./contracts/src/Zappers/Interfaces/IFlashLoanReceiver.sol |
| ./contracts/src/Zappers/Interfaces/ILeverageZapper.sol |
| ./contracts/src/Zappers/Interfaces/ITokenZapper.sol |
| ./contracts/src/Zappers/Interfaces/IZapper.sol |
| ./contracts/src/Zappers/LeftoversSweep.sol |
| ./contracts/src/Zappers/LeverageLSTZapper.sol |
| ./contracts/src/Zappers/LeverageWETHZapper.sol |
| ./contracts/src/Zappers/Modules/Exchanges/Curve/ICurveFactory.sol |
| ./contracts/src/Zappers/Modules/Exchanges/Curve/ICurvePool.sol |
| ./contracts/src/Zappers/Modules/Exchanges/Curve/ICurveStableswapNGFactory.sol |
| ./contracts/src/Zappers/Modules/Exchanges/Curve/ICurveStableswapNGPool.sol |
| ./contracts/src/Zappers/Modules/Exchanges/CurveExchange.sol |
| ./contracts/src/Zappers/Modules/Exchanges/HybridCurveUniV3Exchange.sol |
| ./contracts/src/Zappers/Modules/Exchanges/HybridCurveUniV3ExchangeHelpers.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniV3Exchange.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/INonfungiblePositionManager.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/IPoolInitializer.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/IQuoterV2.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/ISwapRouter.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/IUniswapV3Factory.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/IUniswapV3Pool.sol |
| ./contracts/src/Zappers/Modules/Exchanges/UniswapV3/UniPriceConverter.sol |
| ./contracts/src/Zappers/Modules/FlashLoans/Balancer/vault/IFlashLoanRecipient.sol |
| ./contracts/src/Zappers/Modules/FlashLoans/Balancer/vault/IVault.sol |
| ./contracts/src/Zappers/Modules/FlashLoans/BalancerFlashLoan.sol |
| ./contracts/src/Zappers/TokenZapper.sol |
| ./contracts/src/Zappers/WETHZapper.sol |
| ./contracts/test/AddressesRegistry.t.sol |
| ./contracts/test/AnchoredInvariantsTest.t.sol |
| ./contracts/test/AnchoredSPInvariantsTest.t.sol |
| ./contracts/test/BoldToken.t.sol |
| ./contracts/test/E2E.t.sol |
| ./contracts/test/HintHelpers.t.sol |
| ./contracts/test/Interfaces/Curve/ICurveStableSwapFactoryNG.sol |
| ./contracts/test/Interfaces/Curve/ICurveStableSwapNG.sol |
| ./contracts/test/Interfaces/Curve/ILiquidityGaugeV6.sol |
| ./contracts/test/Interfaces/LiquityV1/IBorrowerOperationsV1.sol |
| ./contracts/test/Interfaces/LiquityV1/IPriceFeedV1.sol |
| ./contracts/test/Interfaces/LiquityV1/ISortedTrovesV1.sol |
| ./contracts/test/Interfaces/LiquityV1/ITroveManagerV1.sol |
| ./contracts/test/Invariants.t.sol |
| ./contracts/test/OracleMainnet.t.sol |
| ./contracts/test/SPInvariants.t.sol |
| ./contracts/test/SortedTroves.t.sol |
| ./contracts/test/TestContracts/Accounts.sol |
| ./contracts/test/TestContracts/AddRemoveManagersTester.sol |
| ./contracts/test/TestContracts/Assertions.sol |
| ./contracts/test/TestContracts/BaseHandler.sol |
| ./contracts/test/TestContracts/BaseInvariantTest.sol |
| ./contracts/test/TestContracts/BaseMultiCollateralTest.sol |
| ./contracts/test/TestContracts/BaseTest.sol |
| ./contracts/test/TestContracts/BoldTokenTester.sol |
| ./contracts/test/TestContracts/BorrowerOperationsTester.t.sol |
| ./contracts/test/TestContracts/ChainlinkOracleMock.sol |
| ./contracts/test/TestContracts/CollateralRegistryTester.sol |
| ./contracts/test/TestContracts/CommunityIssuanceMock.sol |
| ./contracts/test/TestContracts/Deployment.t.sol |
| ./contracts/test/TestContracts/DevTestSetup.sol |
| ./contracts/test/TestContracts/ERC20Faucet.sol |
| ./contracts/test/TestContracts/ERC20MinterMock.sol |
| ./contracts/test/TestContracts/GasGuzzlerOracle.sol |
| ./contracts/test/TestContracts/GasGuzzlerToken.sol |
| ./contracts/test/TestContracts/Interfaces/IBorrowerOperationsTester.sol |
| ./contracts/test/TestContracts/Interfaces/IPriceFeedMock.sol |
| ./contracts/test/TestContracts/Interfaces/IPriceFeedTestnet.sol |
| ./contracts/test/TestContracts/Interfaces/ITroveManagerTester.sol |
| ./contracts/test/TestContracts/InvariantsTestHandler.t.sol |
| ./contracts/test/TestContracts/LQTYStakingMock.sol |
| ./contracts/test/TestContracts/LQTYTokenMock.sol |
| ./contracts/test/TestContracts/LiquityMathTester.sol |
| ./contracts/test/TestContracts/MetadataDeployment.sol |
| ./contracts/test/TestContracts/MockInterestRouter.sol |
| ./contracts/test/TestContracts/NonPayableSwitch.sol |
| ./contracts/test/TestContracts/PriceFeedMock.sol |
| ./contracts/test/TestContracts/PriceFeedTestnet.sol |
| ./contracts/test/TestContracts/RETHTokenMock.sol |
| ./contracts/test/TestContracts/SPInvariantsTestHandler.t.sol |
| ./contracts/test/TestContracts/SortedTrovesTester.sol |
| ./contracts/test/TestContracts/TroveManagerTester.t.sol |
| ./contracts/test/TestContracts/WETH.sol |
| ./contracts/test/TestContracts/WETHTester.sol |
| ./contracts/test/TestContracts/WSTETHTokenMock.sol |
| ./contracts/test/TestContracts/WhitelistTestSetup.sol |
| ./contracts/test/TokenWrapper.t.sol |
| ./contracts/test/Utils/BatchIdSet.sol |
| ./contracts/test/Utils/EnumerableSet.sol |
| ./contracts/test/Utils/Logging.sol |
| ./contracts/test/Utils/Math.sol |
| ./contracts/test/Utils/StringEquality.sol |
| ./contracts/test/Utils/StringFormatting.sol |
| ./contracts/test/Utils/Trove.sol |
| ./contracts/test/Utils/TroveId.sol |
| ./contracts/test/Utils/UniPriceConverterLog.sol |
| ./contracts/test/Utils/UseDeployment.sol |
| ./contracts/test/basicOps.t.sol |
| ./contracts/test/basicOpsWhitelist.t.sol |
| ./contracts/test/batchManagementFee.t.sol |
| ./contracts/test/borrowerOperations.t.sol |
| ./contracts/test/borrowerOperationsOnBehalfTroveManagament.t.sol |
| ./contracts/test/collateralRegistry.t.sol |
| ./contracts/test/criticalThreshold.t.sol |
| ./contracts/test/deployment.t.sol |
| ./contracts/test/events.t.sol |
| ./contracts/test/interestBatchManagement.t.sol |
| ./contracts/test/interestIndividualDelegation.t.sol |
| ./contracts/test/interestRateAggregate.t.sol |
| ./contracts/test/interestRateBasic.t.sol |
| ./contracts/test/liquidationCosts.t.sol |
| ./contracts/test/liquidations.t.sol |
| ./contracts/test/liquidationsLST.t.sol |
| ./contracts/test/multiCollateralWhitelist.t.sol |
| ./contracts/test/multicollateral.t.sol |
| ./contracts/test/rebasingBatchShares.t.sol |
| ./contracts/test/redemptions.t.sol |
| ./contracts/test/shutdown.t.sol |
| ./contracts/test/stabilityPool.t.sol |
| ./contracts/test/tokenZapper.t.sol |
| ./contracts/test/troveManager.t.sol |
| ./contracts/test/troveNFT.t.sol |
| ./contracts/test/whitelist.t.sol |
| ./contracts/test/whitelistRedemptions.t.sol |
| ./contracts/test/zapperGasComp.t.sol |
| ./contracts/test/zapperLeverage.t.sol |
| ./contracts/test/zapperWETH.t.sol |
| Totals: 217 |


## Miscellaneous
Employees of BitVault and employees' family members are ineligible to participate in this audit.

Code4rena's rules cannot be overridden by the contents of this README. In case of doubt, please check with C4 staff.




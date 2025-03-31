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
- Total Prize Pool: $15000 in USDC
  - HM awards: up to XXX XXX USDC (Notion: HM (main) pool)
    - If no valid Highs or Mediums are found, the HM pool is $0 
 
  - Judge awards: $2500 in USDC
  - Validator awards: XXX XXX USDC (Notion: Triage fee - final)
  - Scout awards: $500 in USDC
  - (this line can be removed if there is no mitigation) Mitigation Review: XXX XXX USDC
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts XXX XXX XX 20:00 UTC (ex. `Starts March 22, 2023 20:00 UTC`)
- Ends XXX XXX XX 20:00 UTC (ex. `Ends March 30, 2023 20:00 UTC`)

**Note re: risk level upgrades/downgrades**

Two important notes about judging phase risk adjustments: 
- High- or Medium-risk submissions downgraded to Low-risk (QA) will be ineligible for awards.
- Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.

As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2025-04-bitvault/blob/main/4naly3er-report.md).



_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._
## 🐺 C4: Begin Gist paste here (and delete this line)





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


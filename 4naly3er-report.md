# Report


## Gas Optimizations


| |Issue|Instances|
|-|:-|:-:|
| [GAS-1](#GAS-1) | Using bools for storage incurs overhead | 1 |
| [GAS-2](#GAS-2) | Cache array length outside of loop | 2 |
| [GAS-3](#GAS-3) | For Operations that will not overflow, you could use unchecked | 357 |
| [GAS-4](#GAS-4) | Use Custom Errors | 21 |
| [GAS-5](#GAS-5) | Don't initialize variables with default value | 6 |
| [GAS-6](#GAS-6) | Long revert strings | 8 |
| [GAS-7](#GAS-7) | Functions guaranteed to revert when called by normal users can be marked `payable` | 5 |
| [GAS-8](#GAS-8) | `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too) | 7 |
| [GAS-9](#GAS-9) | Using `private` rather than `public` for constants, saves gas | 5 |
| [GAS-10](#GAS-10) | Splitting require() statements that use && saves gas | 2 |
| [GAS-11](#GAS-11) | Use != 0 instead of > 0 for unsigned integer comparison | 46 |
### <a name="GAS-1"></a>[GAS-1] Using bools for storage incurs overhead
Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from ‘false’ to ‘true’, after having been ‘true’ in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).

*Instances (1)*:
```solidity
File: BorrowerOperations.sol

45:     bool public hasBeenShutDown;

```

### <a name="GAS-2"></a>[GAS-2] Cache array length outside of loop
If not cached, the solidity compiler will always read the length of the array during each iteration. That is, if it is a storage array, this is an extra sload operation (100 additional extra gas for each iteration except for the first) and if it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).

*Instances (2)*:
```solidity
File: TroveManager.sol

518:         for (uint256 i = 0; i < _troveArray.length; i++) {

920:         for (uint256 i = 0; i < _troveIds.length; i++) {

```

### <a name="GAS-3"></a>[GAS-3] For Operations that will not overflow, you could use unchecked

*Instances (357)*:
```solidity
File: AddressesRegistry.sol

5: import "./Dependencies/Owned.sol";

6: import {MIN_LIQUIDATION_PENALTY_SP, MAX_LIQUIDATION_PENALTY_REDISTRIBUTION} from "./Dependencies/Constants.sol";

7: import "./Interfaces/IAddressesRegistry.sol";

202:         require(proposedCR.timestamp + 3 days <= block.timestamp && proposedCR.timestamp != 0, "Invalid");

244:             proposedLiquidationValues.timestamp + 3 days <= block.timestamp && proposedLiquidationValues.timestamp != 0,

```

```solidity
File: BorrowerOperations.sol

5: import "openzeppelin-contracts/contracts/token/ERC20/utils/SafeERC20.sol";

7: import "./Interfaces/IBorrowerOperations.sol";

8: import "./Interfaces/IAddressesRegistry.sol";

9: import "./Interfaces/ITroveManager.sol";

10: import "./Interfaces/IBoldToken.sol";

11: import "./Interfaces/ICollSurplusPool.sol";

12: import "./Interfaces/ISortedTroves.sol";

13: import "./Dependencies/LiquityBase.sol";

14: import "./Dependencies/AddRemoveManagers.sol";

15: import "./Types/LatestTroveData.sol";

16: import "./Types/LatestBatchData.sol";

68:     "CompilerError: Stack too deep". */

358:         _change.newWeightedRecordedDebt = (_batchEntireDebt + _change.debtIncrease) * _annualInterestRate;

364:         vars.entireDebt = _change.debtIncrease + _change.upfrontFee;

371:             _change.newWeightedRecordedDebt = vars.entireDebt * _annualInterestRate;

377:             _change.newWeightedRecordedDebt = (_batchEntireDebt + vars.entireDebt) * _annualInterestRate;

379:                 (_batchEntireDebt + vars.entireDebt) *

420:             0 // _maxUpfrontFee

436:             0 // _maxUpfrontFee

462:             0 // _maxUpfrontFee

562:         troveChange.newWeightedRecordedDebt = newDebt * _newAnnualInterestRate;

566:         if (block.timestamp < trove.lastInterestRateAdjTime + INTEREST_RATE_ADJ_COOLDOWN) {

571:         troveChange.newWeightedRecordedDebt = newDebt * _newAnnualInterestRate;

608:         address receiver = owner; // If it’s a withdrawal, and manager has receive privilege, manager would be the receiver

622:             uint256 maxRepayment = vars.trove.entireDebt > MIN_DEBT ? vars.trove.entireDebt - MIN_DEBT : 0;

636:         vars.newColl = vars.trove.entireColl + _troveChange.collIncrease - _troveChange.collDecrease;

637:         vars.newDebt = vars.trove.entireDebt + _troveChange.debtIncrease - _troveChange.debtDecrease;

647:                 batch.entireDebtWithoutRedistribution +

648:                 vars.trove.redistBoldDebtGain +

649:                 _troveChange.debtIncrease -

656:             _troveChange.newWeightedRecordedDebt = batchFutureDebt * batch.annualInterestRate;

658:             _troveChange.newWeightedRecordedBatchManagementFee = batchFutureDebt * batch.annualManagementFee;

663:             _troveChange.newWeightedRecordedDebt = vars.newDebt * vars.trove.annualInterestRate;

672:             vars.newDebt += _troveChange.upfrontFee;

674:                 batchFutureDebt += _troveChange.upfrontFee;

676:                 _troveChange.newWeightedRecordedDebt = batchFutureDebt * batch.annualInterestRate;

677:                 _troveChange.newWeightedRecordedBatchManagementFee = batchFutureDebt * batch.annualManagementFee;

680:                 _troveChange.newWeightedRecordedDebt = vars.newDebt * vars.trove.annualInterestRate;

739:             uint256 batchFutureDebt = batch.entireDebtWithoutRedistribution -

740:                 (trove.entireDebt - trove.redistBoldDebtGain);

743:             troveChange.newWeightedRecordedDebt = batchFutureDebt * batch.annualInterestRate;

745:             troveChange.newWeightedRecordedBatchManagementFee = batchFutureDebt * batch.annualManagementFee;

801:             change.newWeightedRecordedDebt = trove.entireDebt * trove.annualInterestRate;

807:                 (batch.entireDebtWithoutRedistribution + trove.redistBoldDebtGain) *

811:                 (batch.entireDebtWithoutRedistribution + trove.redistBoldDebtGain) *

944:         batchChange.newWeightedRecordedDebt = batch.entireDebtWithoutRedistribution * batch.annualInterestRate;

947:             batch.entireDebtWithoutRedistribution *

976:         batchChange.newWeightedRecordedDebt = newDebt * _newAnnualInterestRate;

978:         batchChange.newWeightedRecordedBatchManagementFee = newDebt * batch.annualManagementFee;

983:             block.timestamp < batch.lastInterestRateAdjTime + INTEREST_RATE_ADJ_COOLDOWN

991:             newDebt += batchChange.upfrontFee;

994:             batchChange.newWeightedRecordedDebt = newDebt * _newAnnualInterestRate;

995:             batchChange.newWeightedRecordedBatchManagementFee = newDebt * batch.annualManagementFee;

1051:             vars.newBatch.weightedRecordedDebt +

1054:             (vars.newBatch.entireDebtWithoutRedistribution + vars.trove.entireDebt) *

1070:             (vars.newBatch.entireDebtWithoutRedistribution + vars.trove.entireDebt) *

1076:             (vars.newBatch.entireDebtWithoutRedistribution + vars.trove.entireDebt) *

1130:         uint256 batchFutureDebt = vars.batch.entireDebtWithoutRedistribution -

1131:             (vars.trove.entireDebt - vars.trove.redistBoldDebtGain);

1139:             batchFutureDebt *

1140:             vars.batch.annualInterestRate +

1141:             vars.trove.entireDebt *

1147:             block.timestamp < vars.trove.lastInterestRateAdjTime + INTEREST_RATE_ADJ_COOLDOWN

1160:             batchFutureDebt *

1161:             vars.batch.annualInterestRate +

1162:             vars.trove.entireDebt *

1166:         batchChange.newWeightedRecordedBatchManagementFee = batchFutureDebt * vars.batch.annualManagementFee;

1213:         _troveEntireDebt += _troveChange.upfrontFee;

1232:         return _calcInterest(_debt * _avgInterestRate, UPFRONT_INTEREST_PERIOD);

1499:         if (_newICR < MCR + BCR) {

1511:         if ((_troveChange.debtDecrease * DECIMAL_PRECISION < _troveChange.collDecrease * _price)) {

1593:         if (block.timestamp < _lastInterestRateAdjTime + uint256(interestBatchManager.minInterestRateChangePeriod)) {

1602:         if (block.timestamp < _lastInterestRateAdjTime + _minInterestRateChangePeriod) {

1656:         totalColl += _troveChange.collIncrease;

1657:         totalColl -= _troveChange.collDecrease;

1660:         totalDebt += _troveChange.debtIncrease;

1661:         totalDebt += _troveChange.upfrontFee;

1662:         totalDebt -= _troveChange.debtDecrease;

```

```solidity
File: CollateralRegistry.sol

5: import "openzeppelin-contracts/contracts/token/ERC20/extensions/IERC20Metadata.sol";

7: import "./Dependencies/Constants.sol";

8: import "./Dependencies/LiquityMath.sol";

9: import "./Dependencies/Owned.sol";

11: import "./Interfaces/ITroveManager.sol";

12: import "./Interfaces/IBoldToken.sol";

13: import "./Interfaces/ICollateralRegistry.sol";

14: import "./Interfaces/IWhitelist.sol";

49:         for (uint8 i; i < numTokens; i++) {

68:         require(totalCollaterals + numTokens <= 10, "Max collaterals");

71:         for (uint8 i = 0; i < numTokens; i++) {

85:         totalCollaterals += numTokens;

105:         uint256 swapIndex = totalCollaterals - 1;

119:         totalCollaterals--;

152:         for (uint256 index = 0; index < totals.numCollaterals; index++) {

158:                 totals.unbacked += unbackedPortion;

167:             for (uint256 index = 0; index < totals.numCollaterals; index++) {

172:                     totals.unbacked += unbackedPortion;

179:         for (uint256 index = 0; index < totals.numCollaterals; index++) {

182:                 uint256 redeemAmount = (_boldAmount * unbackedPortions[index]) / totals.unbacked;

192:                     totals.redeemedAmount += redeemedAmount;

212:             lastFeeOperationTime += ONE_MINUTE * minutesPassed;

218:         return (block.timestamp - lastFeeOperationTime) / ONE_MINUTE;

248:         uint256 redeemedBoldFraction = (_redeemAmount * DECIMAL_PRECISION) / _totalBoldSupply;

250:         uint256 newBaseRate = decayedBaseRate + redeemedBoldFraction / REDEMPTION_BETA;

251:         newBaseRate = LiquityMath._min(newBaseRate, DECIMAL_PRECISION); // cap baseRate at a maximum of 100%

260:         return (baseRate * decayFactor) / DECIMAL_PRECISION;

266:                 REDEMPTION_FEE_FLOOR + _baseRate,

267:                 DECIMAL_PRECISION // cap at a maximum of 100%

272:         uint256 redemptionFee = (_redemptionRate * _amount) / DECIMAL_PRECISION;

```

```solidity
File: LiquityBase.sol

5: import "./Constants.sol";

6: import "./LiquityMath.sol";

7: import "../Interfaces/IAddressesRegistry.sol";

8: import "../Interfaces/IActivePool.sol";

9: import "../Interfaces/IDefaultPool.sol";

10: import "../Interfaces/IPriceFeed.sol";

11: import "../Interfaces/ILiquityBase.sol";

48:         return activeColl + liquidatedColl;

55:         return activeDebt + closedDebt;

74:         return (_weightedDebt * _period) / ONE_YEAR / DECIMAL_PRECISION;

```

```solidity
File: StabilityPool.sol

5: import "openzeppelin-contracts/contracts/token/ERC20/utils/SafeERC20.sol";

7: import "./Interfaces/IStabilityPool.sol";

8: import "./Interfaces/IAddressesRegistry.sol";

9: import "./Interfaces/IStabilityPoolEvents.sol";

10: import "./Interfaces/ITroveManager.sol";

11: import "./Interfaces/IBoldToken.sol";

12: import "./Dependencies/LiquityBase.sol";

127:     uint256 internal collBalance; // deposited coll tracker

146:         uint256 S; // Coll reward sum liqs

148:         uint256 B; // Bold reward sum from minted interest

152:     mapping(address => Deposit) public deposits; // depositor address -> Deposit struct

153:     mapping(address => Snapshots) public depositSnapshots; // depositor address -> snapshots struct

243:         uint256 newDeposit = compoundedBoldDeposit + _topUp + keptYieldGain;

253:             initialDeposit - compoundedBoldDeposit,

263:         _updateTotalBoldDeposits(_topUp + keptYieldGain, 0);

305:         uint256 newDeposit = compoundedBoldDeposit - boldToWithdraw + keptYieldGain;

315:             initialDeposit - compoundedBoldDeposit,

316:             -int256(boldToWithdraw),

326:         _sendBoldtoDepositor(msg.sender, boldToWithdraw + yieldGainToSend);

339:             collToSend = stashedColl[_depositor] + _currentCollGain;

341:             newStashedColl = stashedColl[_depositor] + _currentCollGain;

370:         uint256 accumulatedYieldGains = yieldGainsPending + _newYield;

380:         yieldGainsOwed += accumulatedYieldGains;

383:         scaleToB[currentScale] += (P * accumulatedYieldGains) / totalBoldDeposits;

397:         scaleToS[currentScale] += (P * _collToAdd) / totalBoldDeposits;

400:         uint256 numerator = P * (totalBoldDeposits - _debtToOffset);

401:         uint256 newP = numerator / totalBoldDeposits;

417:         while (newP < P_PRECISION / SCALE_FACTOR) {

418:             numerator *= SCALE_FACTOR;

419:             newP = numerator / totalBoldDeposits;

420:             currentScale += 1;

438:         uint256 newCollBalance = collBalance + _collToAdd;

449:         uint256 newTotalBoldDeposits = totalBoldDeposits + _depositIncrease - _depositDecrease;

458:         uint256 newYieldGainsOwed = yieldGainsOwed - _amount;

471:         uint256 normalizedGains = scaleToS[snapshots.scale] - snapshots.S;

474:         for (uint256 i = 1; i <= SCALE_SPAN; ++i) {

475:             normalizedGains += scaleToS[snapshots.scale + i] / SCALE_FACTOR ** i;

478:         return LiquityMath._min((initialDeposit * normalizedGains) / snapshots.P, collBalance);

488:         uint256 normalizedGains = scaleToB[snapshots.scale] - snapshots.B;

491:         for (uint256 i = 1; i <= SCALE_SPAN; ++i) {

492:             normalizedGains += scaleToB[snapshots.scale + i] / SCALE_FACTOR ** i;

495:         return LiquityMath._min((initialDeposit * normalizedGains) / snapshots.P, yieldGainsOwed);

508:         uint256 normalizedGains = scaleToB[snapshots.scale] - snapshots.B;

511:         for (uint256 i = 1; i <= SCALE_SPAN; ++i) {

512:             normalizedGains += scaleToB[snapshots.scale + i] / SCALE_FACTOR ** i;

517:         newYieldGainsOwed += pendingSPYield;

519:         if (currentScale <= snapshots.scale + SCALE_SPAN) {

520:             normalizedGains +=

521:                 (P * pendingSPYield) /

522:                 totalBoldDeposits /

523:                 SCALE_FACTOR ** (currentScale - snapshots.scale);

526:         return LiquityMath._min((initialDeposit * normalizedGains) / snapshots.P, newYieldGainsOwed);

537:         uint256 scaleDiff = currentScale - snapshots.scale;

544:             compoundedDeposit = (initialDeposit * P) / snapshots.P / SCALE_FACTOR ** scaleDiff;

555:         uint256 newCollBalance = collBalance - _collAmount;

605:         require(_initialDeposit > 0, "StabilityPool: User must have a non-zero deposit");

614:         require(_amount > 0, "StabilityPool: Amount must be non-zero");

```

```solidity
File: TroveManager.sol

5: import "./Interfaces/ITroveManager.sol";

6: import "./Interfaces/IStabilityPool.sol";

7: import "./Interfaces/ICollSurplusPool.sol";

8: import "./Interfaces/IBoldToken.sol";

9: import "./Interfaces/ISortedTroves.sol";

10: import "./Interfaces/ITroveEvents.sol";

11: import "./Interfaces/ITroveNFT.sol";

12: import "./Interfaces/ICollateralRegistry.sol";

13: import "./Interfaces/IWETH.sol";

14: import "./Interfaces/IWhitelist.sol";

15: import "./Interfaces/IAddressesRegistry.sol";

16: import "./Dependencies/LiquityBase.sol";

270:         uint256 collToLiquidate = trove.entireColl - singleLiquidation.collGasCompensation;

296:                 batch.weightedRecordedDebt +

297:                 (trove.entireDebt - trove.redistBoldDebtGain) *

300:                 batch.entireDebtWithoutRedistribution *

305:                 batch.weightedRecordedBatchManagementFee +

306:                 (trove.entireDebt - trove.redistBoldDebtGain) *

309:                 batch.entireDebtWithoutRedistribution *

340:             _debtChangeFromOperation: -int256(trove.entireDebt),

342:             _collChangeFromOperation: -int256(trove.entireColl)

361:         return LiquityMath._min(_entireColl / COLL_GAS_COMPENSATION_DIVISOR, COLL_GAS_COMPENSATION_CAP);

369:         uint256 _collToLiquidate, // gas compensation is already subtracted

396:             collSPPortion = (_collToLiquidate * debtToOffset) / _entireTroveDebt;

406:         debtToRedistribute = _entireTroveDebt - debtToOffset;

408:             uint256 collRedistributionPortion = _collToLiquidate - collSPPortion;

411:                     collRedistributionPortion + collSurplus, // Coll surplus from offset can be eaten up by red. penalty

413:                     LIQUIDATION_PENALTY_REDISTRIBUTION, // _penaltyRatio

427:         uint256 maxSeizedColl = (_debtToLiquidate * (DECIMAL_PRECISION + _penaltyRatio)) / _price;

430:             collSurplus = _collToLiquidate - maxSeizedColl;

458:         uint256 boldInSPForOffsets = totalBoldDeposits - boldToLeaveInSP;

518:         for (uint256 i = 0; i < _troveArray.length; i++) {

531:                 remainingBoldInSPForOffsets -= singleLiquidation.debtToOffset;

549:         totals.collGasCompensation += _singleLiquidation.collGasCompensation;

550:         totals.ETHGasCompensation += ETH_GAS_COMPENSATION;

551:         troveChange.debtDecrease += _trove.entireDebt;

552:         troveChange.collDecrease += _trove.entireColl;

553:         troveChange.appliedRedistBoldDebtGain += _trove.redistBoldDebtGain;

554:         troveChange.oldWeightedRecordedDebt += _singleLiquidation.oldWeightedRecordedDebt;

555:         troveChange.newWeightedRecordedDebt += _singleLiquidation.newWeightedRecordedDebt;

556:         totals.debtToOffset += _singleLiquidation.debtToOffset;

557:         totals.collToSendToSP += _singleLiquidation.collToSendToSP;

558:         totals.debtToRedistribute += _singleLiquidation.debtToRedistribute;

559:         totals.collToRedistribute += _singleLiquidation.collToRedistribute;

560:         totals.collSurplus += _singleLiquidation.collSurplus;

592:         uint256 newDebt = _singleRedemption.trove.entireDebt - _singleRedemption.boldLot;

593:         uint256 newColl = _singleRedemption.trove.entireColl - _singleRedemption.collLot;

600:             uint256 newAmountForWeightedDebt = _singleRedemption.batch.entireDebtWithoutRedistribution +

601:                 _singleRedemption.trove.redistBoldDebtGain -

605:                 newAmountForWeightedDebt *

618:                 newAmountForWeightedDebt *

634:                 false // _checkBatchSharesRatio

638:             _singleRedemption.newWeightedRecordedDebt = newDebt * _singleRedemption.trove.annualInterestRate;

680:             _debtChangeFromOperation: -int256(_singleRedemption.boldLot),

682:             _collChangeFromOperation: -int256(_singleRedemption.collLot)

717:         uint256 correspondingColl = (_singleRedemption.boldLot * DECIMAL_PRECISION) / _price;

719:         _singleRedemption.collFee = (correspondingColl * _redemptionRate) / DECIMAL_PRECISION;

721:         _singleRedemption.collLot = correspondingColl - _singleRedemption.collFee;

757:         batchTroveChange.newWeightedRecordedDebt = batch.entireDebtWithoutRedistribution * batch.annualInterestRate;

761:             batch.entireDebtWithoutRedistribution *

810:             _maxIterations--;

838:             totalsTroveChange.collDecrease += singleRedemption.collLot;

839:             totalsTroveChange.debtDecrease += singleRedemption.boldLot;

840:             totalsTroveChange.appliedRedistBoldDebtGain += singleRedemption.appliedRedistBoldDebtGain;

844:             totalsTroveChange.newWeightedRecordedDebt += singleRedemption.newWeightedRecordedDebt;

845:             totalsTroveChange.oldWeightedRecordedDebt += singleRedemption.oldWeightedRecordedDebt;

846:             totalCollFee += singleRedemption.collFee;

848:             remainingBold -= singleRedemption.boldLot;

885:             (_singleRedemption.boldLot * (DECIMAL_PRECISION + URGENT_REDEMPTION_BONUS)) /

891:                 (_singleRedemption.trove.entireColl * _price) /

892:                 (DECIMAL_PRECISION + URGENT_REDEMPTION_BONUS);

920:         for (uint256 i = 0; i < _troveIds.length; i++) {

940:             totalsTroveChange.collDecrease += singleRedemption.collLot;

941:             totalsTroveChange.debtDecrease += singleRedemption.boldLot;

942:             totalsTroveChange.appliedRedistBoldDebtGain += singleRedemption.appliedRedistBoldDebtGain;

946:             totalsTroveChange.newWeightedRecordedDebt += singleRedemption.newWeightedRecordedDebt;

947:             totalsTroveChange.oldWeightedRecordedDebt += singleRedemption.oldWeightedRecordedDebt;

949:             remainingBold -= singleRedemption.boldLot;

1000:         trove.redistBoldDebtGain = (stake * (L_boldDebt - rewardSnapshots[_troveId].boldDebt)) / DECIMAL_PRECISION;

1001:         trove.redistCollGain = (stake * (L_coll - rewardSnapshots[_troveId].coll)) / DECIMAL_PRECISION;

1005:         trove.weightedRecordedDebt = trove.recordedDebt * trove.annualInterestRate;

1010:         trove.entireDebt = trove.recordedDebt + trove.redistBoldDebtGain + trove.accruedInterest;

1011:         trove.entireColl = Troves[_troveId].coll + trove.redistCollGain;

1027:             (stake * (L_boldDebt - rewardSnapshots[_troveId].boldDebt)) /

1029:         _latestTroveData.redistCollGain = (stake * (L_coll - rewardSnapshots[_troveId].coll)) / DECIMAL_PRECISION;

1032:             _latestTroveData.recordedDebt = (_latestBatchData.recordedDebt * batchDebtShares) / totalDebtShares;

1033:             _latestTroveData.weightedRecordedDebt = _latestTroveData.recordedDebt * _latestBatchData.annualInterestRate;

1034:             _latestTroveData.accruedInterest = (_latestBatchData.accruedInterest * batchDebtShares) / totalDebtShares;

1036:                 (_latestBatchData.accruedManagementFee * batchDebtShares) /

1043:             _latestTroveData.recordedDebt +

1044:             _latestTroveData.redistBoldDebtGain +

1045:             _latestTroveData.accruedInterest +

1047:         _latestTroveData.entireColl = trove.coll + _latestTroveData.redistCollGain;

1081:         latestBatchData.weightedRecordedDebt = latestBatchData.recordedDebt * latestBatchData.annualInterestRate;

1086:             latestBatchData.recordedDebt *

1094:             latestBatchData.recordedDebt +

1095:             latestBatchData.accruedInterest +

1112:         totalStakes = totalStakes - oldStake + newStake;

1128:             stake = (_coll * totalStakesSnapshot) / totalCollateralSnapshot;

1139:         if (_debtToRedistribute == 0) return; // Otherwise _collToRedistribute > 0 too

1152:         uint256 collNumerator = _collToRedistribute * DECIMAL_PRECISION + lastCollError_Redistribution;

1153:         uint256 boldDebtNumerator = _debtToRedistribute * DECIMAL_PRECISION + lastBoldDebtError_Redistribution;

1156:         uint256 collRewardPerUnitStaked = collNumerator / totalStakes;

1157:         uint256 boldDebtRewardPerUnitStaked = boldDebtNumerator / totalStakes;

1159:         lastCollError_Redistribution = collNumerator - collRewardPerUnitStaked * totalStakes;

1160:         lastBoldDebtError_Redistribution = boldDebtNumerator - boldDebtRewardPerUnitStaked * totalStakes;

1163:         L_coll = L_coll + collRewardPerUnitStaked;

1164:         L_boldDebt = L_boldDebt + boldDebtRewardPerUnitStaked;

1179:         totalCollateralSnapshot = activeColl - _collRemainder + liquidatedColl;

1188:         uint256 idxLast = TroveIdsArrayLength - 1;

1217:             return block.timestamp - _lastDebtUpdateTime;

1220:             return shutdownTime - _lastDebtUpdateTime;

1276:         uint256 unbackedPortion = totalDebt > spSize ? totalDebt - spSize : 0;

1298:         Troves[_troveId].debt = _troveChange.debtIncrease + _troveChange.upfrontFee;

1310:         uint256 newTotalStakes = totalStakes + newStake;

1320:             _debt: _troveChange.debtIncrease + _troveChange.upfrontFee,

1366:         assert(_troveChange.debtIncrease > 0); // TODO: remove before deployment

1377:         uint256 newTotalStakes = totalStakes + newStake;

1508:             _debtChangeFromOperation: int256(_troveChange.debtIncrease) - int256(_troveChange.debtDecrease),

1510:             _collChangeFromOperation: int256(_troveChange.collIncrease) - int256(_troveChange.collDecrease)

1516:         TroveChange memory _troveChange, // decrease vars: entire, with interest, batch fee and redistribution

1519:         uint256 _newBatchDebt // entire, with interest and batch fee

1545:             _debtChangeFromOperation: int256(_troveChange.debtIncrease) - int256(_troveChange.debtDecrease),

1547:             _collChangeFromOperation: int256(_troveChange.collIncrease) - int256(_troveChange.collDecrease)

1566:         TroveChange memory _troveChange, // decrease vars: entire, with interest, batch fee and redistribution

1569:         uint256 _newBatchDebt, // entire, with interest and batch fee

1606:         uint256 newTotalStakes = totalStakes - trove.stake;

1622:         uint256 _newTroveColl, // entire, with redistribution and trove change

1623:         uint256 _newTroveDebt, // entire, with redistribution and trove change

1626:         uint256 _newBatchColl, // without trove change

1627:         uint256 _newBatchDebt // entire (with interest, batch fee), but without trove change nor upfront fee nor redistribution

1637:         assert(_newTroveDebt > 0); // TODO: remove before deployment

1662:             _debtChangeFromOperation: int256(_troveChange.debtIncrease) - int256(_troveChange.debtDecrease),

1664:             _collChangeFromOperation: int256(_troveChange.collIncrease) - int256(_troveChange.collDecrease)

1695:             assert(_newTroveDebt > 0); // TODO: remove before deployment

1745:             _debtChangeFromOperation: int256(_troveChange.debtIncrease) - int256(_troveChange.debtDecrease),

1747:             _collChangeFromOperation: int256(_troveChange.collIncrease) - int256(_troveChange.collDecrease)

1846:         _troveChange.collIncrease = _params.troveColl - _troveChange.appliedRedistCollGain;

1848:             _params.troveDebt -

1849:             _troveChange.appliedRedistBoldDebtGain -

1851:         assert(_params.troveDebt > 0); // TODO: remove before deployment

1908:         uint256 _newTroveDebt, // entire, with interest, batch fee and redistribution

1909:         uint256 _batchColl, // without trove change

1910:         uint256 _batchDebt, // entire (with interest, batch fee), but without trove change, nor upfront fee nor redist

1911:         bool _checkBatchSharesRatio // whether we do the check on the resulting ratio inside the func call

1916:         uint256 debtIncrease = _troveChange.debtIncrease +

1917:             _troveChange.upfrontFee +

1921:             debtIncrease -= _troveChange.debtDecrease;

1923:             debtDecrease = _troveChange.debtDecrease - debtIncrease;

1938:                     batchDebtSharesDelta = (currentBatchDebtShares * debtIncrease) / _batchDebt;

1941:                 Troves[_troveId].batchDebtShares += batchDebtSharesDelta;

1942:                 batches[_batchAddress].debt = _batchDebt + debtIncrease;

1943:                 batches[_batchAddress].totalDebtShares = currentBatchDebtShares + batchDebtSharesDelta;

1950:                     batches[_batchAddress].debt = _batchDebt - debtDecrease;

1951:                     batches[_batchAddress].totalDebtShares = currentBatchDebtShares - Troves[_troveId].batchDebtShares;

1954:                     batchDebtSharesDelta = (currentBatchDebtShares * debtDecrease) / _batchDebt;

1956:                     Troves[_troveId].batchDebtShares -= batchDebtSharesDelta;

1957:                     batches[_batchAddress].debt = _batchDebt - debtDecrease;

1958:                     batches[_batchAddress].totalDebtShares = currentBatchDebtShares - batchDebtSharesDelta;

1966:         uint256 collIncrease = _troveChange.collIncrease + _troveChange.appliedRedistCollGain;

1969:             collIncrease -= _troveChange.collDecrease;

1971:             collDecrease = _troveChange.collDecrease - collIncrease;

1980:                 batches[_batchAddress].coll = _batchColl + collIncrease;

1983:                 batches[_batchAddress].coll = _batchColl - collDecrease;

1998:         if (_currentBatchDebtShares * MAX_BATCH_SHARES_RATIO < _batchDebt && _checkBatchSharesRatio) {

2005:         uint256 _newTroveColl, // entire, with redistribution

2006:         uint256 _newTroveDebt, // entire, with interest, batch fee and redistribution

2010:         uint256 _newBatchDebt, // entire, with interest and batch fee

2078:         uint256 _newTroveColl, // entire, with redistribution

2079:         uint256 _newTroveDebt, // entire, with interest, batch fee and redistribution

2082:         uint256 _newBatchColl, // without trove change

2083:         uint256 _newBatchDebt // entire (with interest and batch fee), but without trove change

2092:         uint256 batchDebtDecrease = _newTroveDebt - _troveChange.upfrontFee - _troveChange.appliedRedistBoldDebtGain;

2093:         uint256 batchCollDecrease = _newTroveColl - _troveChange.appliedRedistCollGain;

2095:         batches[_batchAddress].totalDebtShares -= trove.batchDebtShares;

2096:         batches[_batchAddress].debt = _newBatchDebt - batchDebtDecrease;

2097:         batches[_batchAddress].coll = _newBatchColl - batchCollDecrease;

```

### <a name="GAS-4"></a>[GAS-4] Use Custom Errors
[Source](https://blog.soliditylang.org/2021/04/21/custom-errors/)
Instead of using error strings, to reduce deployment and runtime cost, you should use Custom Errors. This would save both deployment and runtime cost.

*Instances (21)*:
```solidity
File: AddressesRegistry.sol

202:         require(proposedCR.timestamp + 3 days <= block.timestamp && proposedCR.timestamp != 0, "Invalid");

```

```solidity
File: CollateralRegistry.sol

43:         require(numTokens > 0, "Collateral list cannot be empty");

44:         require(numTokens <= 10, "Collateral list too long");

66:         require(numTokens > 0 && numTokens == _tokens.length && numTokens == _troveManagers.length, "Invalid input");

68:         require(totalCollaterals + numTokens <= 10, "Max collaterals");

75:             require(index <= 9, "Invalid index");

76:             require(address(collateralTokens[index]) == address(0), "Collateral already initialised");

94:         require(index <= 9, "Invalid index");

95:         require(address(collateralTokens[index]) != address(0), "Branch not initialised");

100:         require(troveManager.shutdownTime() != 0, "Branch is not shutdown");

147:         require(redemptionRate <= _maxFeePercentage, "CR: Fee exceeded provided maximum");

305:         require(_index < 10, "Invalid index");

311:         require(_index < 10, "Invalid index");

325:         require(_amount > 0, "CollateralRegistry: Amount must be greater than zero");

```

```solidity
File: StabilityPool.sol

329:         require(newTotalBoldDeposits >= MIN_BOLD_IN_SP, "Withdrawal must leave totalBoldDeposits >= MIN_BOLD_IN_SP");

410:         require(newP > 0, "P must never decrease to 0");

597:         require(msg.sender == address(activePool), "StabilityPool: Caller is not ActivePool");

601:         require(msg.sender == address(troveManager), "StabilityPool: Caller is not TroveManager");

605:         require(_initialDeposit > 0, "StabilityPool: User must have a non-zero deposit");

610:         require(initialDeposit == 0, "StabilityPool: User must have no deposit");

614:         require(_amount > 0, "StabilityPool: Amount must be non-zero");

```

### <a name="GAS-5"></a>[GAS-5] Don't initialize variables with default value

*Instances (6)*:
```solidity
File: CollateralRegistry.sol

71:         for (uint8 i = 0; i < numTokens; i++) {

152:         for (uint256 index = 0; index < totals.numCollaterals; index++) {

167:             for (uint256 index = 0; index < totals.numCollaterals; index++) {

179:         for (uint256 index = 0; index < totals.numCollaterals; index++) {

```

```solidity
File: TroveManager.sol

518:         for (uint256 i = 0; i < _troveArray.length; i++) {

920:         for (uint256 i = 0; i < _troveIds.length; i++) {

```

### <a name="GAS-6"></a>[GAS-6] Long revert strings

*Instances (8)*:
```solidity
File: CollateralRegistry.sol

147:         require(redemptionRate <= _maxFeePercentage, "CR: Fee exceeded provided maximum");

325:         require(_amount > 0, "CollateralRegistry: Amount must be greater than zero");

```

```solidity
File: StabilityPool.sol

329:         require(newTotalBoldDeposits >= MIN_BOLD_IN_SP, "Withdrawal must leave totalBoldDeposits >= MIN_BOLD_IN_SP");

597:         require(msg.sender == address(activePool), "StabilityPool: Caller is not ActivePool");

601:         require(msg.sender == address(troveManager), "StabilityPool: Caller is not TroveManager");

605:         require(_initialDeposit > 0, "StabilityPool: User must have a non-zero deposit");

610:         require(initialDeposit == 0, "StabilityPool: User must have no deposit");

614:         require(_amount > 0, "StabilityPool: Amount must be non-zero");

```

### <a name="GAS-7"></a>[GAS-7] Functions guaranteed to revert when called by normal users can be marked `payable`
If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

*Instances (5)*:
```solidity
File: AddressesRegistry.sol

119:     function setAddresses(AddressVars memory _vars) external onlyOwner {

167:     function setWhitelist(IWhitelist _newWhitelist) external override onlyOwner {

201:     function acceptNewCollateralValues() external override onlyOwner {

242:     function acceptNewLiquidationValues() external override onlyOwner {

```

```solidity
File: CollateralRegistry.sol

92:     function removeCollateral(uint256 index) external override onlyOwner {

```

### <a name="GAS-8"></a>[GAS-8] `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too)
*Saves 5 gas per loop*

*Instances (7)*:
```solidity
File: CollateralRegistry.sol

49:         for (uint8 i; i < numTokens; i++) {

71:         for (uint8 i = 0; i < numTokens; i++) {

152:         for (uint256 index = 0; index < totals.numCollaterals; index++) {

167:             for (uint256 index = 0; index < totals.numCollaterals; index++) {

179:         for (uint256 index = 0; index < totals.numCollaterals; index++) {

```

```solidity
File: TroveManager.sol

518:         for (uint256 i = 0; i < _troveArray.length; i++) {

920:         for (uint256 i = 0; i < _troveIds.length; i++) {

```

### <a name="GAS-9"></a>[GAS-9] Using `private` rather than `public` for constants, saves gas
If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table

*Instances (5)*:
```solidity
File: StabilityPool.sol

121:     string public constant NAME = "StabilityPool";

164:     uint256 public constant P_PRECISION = 1e36;

167:     uint256 public constant SCALE_FACTOR = 1e9;

170:     uint256 public constant MAX_SCALE_FACTOR_EXPONENT = 8;

173:     uint256 public constant SCALE_SPAN = 2;

```

### <a name="GAS-10"></a>[GAS-10] Splitting require() statements that use && saves gas

*Instances (2)*:
```solidity
File: AddressesRegistry.sol

202:         require(proposedCR.timestamp + 3 days <= block.timestamp && proposedCR.timestamp != 0, "Invalid");

```

```solidity
File: CollateralRegistry.sol

66:         require(numTokens > 0 && numTokens == _tokens.length && numTokens == _troveManagers.length, "Invalid input");

```

### <a name="GAS-11"></a>[GAS-11] Use != 0 instead of > 0 for unsigned integer comparison

*Instances (46)*:
```solidity
File: BorrowerOperations.sol

170:         assert(MIN_DEBT > 0);

610:         if (_troveChange.collDecrease > 0 || _troveChange.debtIncrease > 0) {

614:         if (_troveChange.collIncrease > 0 || _troveChange.debtDecrease > 0) {

621:         if (_troveChange.debtDecrease > 0) {

632:         if (_troveChange.collDecrease > 0) {

667:         if (_troveChange.debtIncrease > 0) {

1326:         if (_troveChange.debtIncrease > 0) {

1328:         } else if (_troveChange.debtDecrease > 0) {

1332:         if (_troveChange.collIncrease > 0) {

1335:         } else if (_troveChange.collDecrease > 0) {

1349:         return interestBatchManagers[_batchManager].maxInterestRate > 0;

1505:         if (_debtIncrease > 0 && _newTCR < CCR) {

1614:         if (interestBatchManagers[_interestBatchManagerAddress].maxInterestRate > 0) {

```

```solidity
File: CollateralRegistry.sol

43:         require(numTokens > 0, "Collateral list cannot be empty");

66:         require(numTokens > 0 && numTokens == _tokens.length && numTokens == _troveManagers.length, "Invalid input");

181:             if (unbackedPortions[index] > 0) {

183:                 if (redeemAmount > 0) {

200:         if (totals.redeemedAmount > 0) {

211:         if (minutesPassed > 0) {

325:         require(_amount > 0, "CollateralRegistry: Amount must be greater than zero");

```

```solidity
File: StabilityPool.sol

410:         require(newP > 0, "P must never decrease to 0");

605:         require(_initialDeposit > 0, "StabilityPool: User must have a non-zero deposit");

614:         require(_amount > 0, "StabilityPool: Amount must be non-zero");

```

```solidity
File: TroveManager.sol

317:         if (singleLiquidation.collSurplus > 0) {

394:         if (_boldInSPForOffsets > 0) {

407:         if (debtToRedistribute > 0) {

409:             if (collRedistributionPortion > 0) {

470:         if (totals.debtToOffset > 0 || totals.collToSendToSP > 0) {

480:         if (totals.collSurplus > 0) {

564:         if (_eth > 0) {

568:         if (_coll > 0) {

575:         if (_bold > 0) {

579:         if (_coll > 0) {

736:                 if (newDebt > 0) {

809:         while (singleRedemption.troveId != 0 && remainingBold > 0 && _maxIterations > 0) {

1031:         if (totalDebtShares > 0) {

1139:         if (_debtToRedistribute == 0) return; // Otherwise _collToRedistribute > 0 too

1218:         } else if (shutdownTime > 0 && _lastDebtUpdateTime < shutdownTime) {

1366:         assert(_troveChange.debtIncrease > 0); // TODO: remove before deployment

1637:         assert(_newTroveDebt > 0); // TODO: remove before deployment

1695:             assert(_newTroveDebt > 0); // TODO: remove before deployment

1851:         assert(_params.troveDebt > 0); // TODO: remove before deployment

1930:             if (debtIncrease > 0) {

1944:             } else if (debtDecrease > 0) {

1978:             if (collIncrease > 0) {

1981:             } else if (collDecrease > 0) {

```


## Non Critical Issues


| |Issue|Instances|
|-|:-|:-:|
| [NC-1](#NC-1) | TODO Left in the code | 4 |
### <a name="NC-1"></a>[NC-1] TODO Left in the code
TODOs may signal that a feature is missing or not ready for audit, consider resolving the issue and removing the TODO comment

*Instances (4)*:
```solidity
File: TroveManager.sol

1366:         assert(_troveChange.debtIncrease > 0); // TODO: remove before deployment

1637:         assert(_newTroveDebt > 0); // TODO: remove before deployment

1695:             assert(_newTroveDebt > 0); // TODO: remove before deployment

1851:         assert(_params.troveDebt > 0); // TODO: remove before deployment

```


## Low Issues


| |Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | Unsafe ERC20 operation(s) | 4 |
### <a name="L-1"></a>[L-1] Unsafe ERC20 operation(s)

*Instances (4)*:
```solidity
File: BorrowerOperations.sol

194:         collToken.approve(address(activePool), type(uint256).max);

403:         WETH.transferFrom(msg.sender, gasPoolAddress, ETH_GAS_COMPENSATION);

772:         WETH.transferFrom(gasPoolAddress, receiver, ETH_GAS_COMPENSATION);

```

```solidity
File: TroveManager.sol

565:             WETH.transferFrom(gasPoolAddress, _liquidator, _eth);

```


## Medium Issues


| |Issue|Instances|
|-|:-|:-:|
| [M-1](#M-1) | Centralization Risk for trusted owners | 12 |
### <a name="M-1"></a>[M-1] Centralization Risk for trusted owners

#### Impact:
Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

*Instances (12)*:
```solidity
File: AddressesRegistry.sol

9: contract AddressesRegistry is Owned, IAddressesRegistry {

97:     ) Owned(_owner) {

119:     function setAddresses(AddressVars memory _vars) external onlyOwner {

167:     function setWhitelist(IWhitelist _newWhitelist) external override onlyOwner {

186:     ) external override onlyOwner {

201:     function acceptNewCollateralValues() external override onlyOwner {

226:     ) external override onlyOwner {

242:     function acceptNewLiquidationValues() external override onlyOwner {

```

```solidity
File: CollateralRegistry.sol

16: contract CollateralRegistry is Owned, ICollateralRegistry {

41:     ) Owned(_owner) {

64:     ) external override onlyOwner {

92:     function removeCollateral(uint256 index) external override onlyOwner {

```
